---
title: "Blog 1"
date: "2025-12-09"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Hiện đại hóa ứng dụng không khó khăn: di chuyển sang Amazon EKS với cấu hình NLB hiện có

**Tác giả:**

- Henrique Santana, Chuyên gia Container, AWS
- Luis Felipe, Kiến trúc sư Giải pháp Chính, AWS

_Ngày: 25 tháng 3, 2025_

<style> 
body {
    font-family: "Times New Roman", Times, serif;
    font-size: 13px;
}

h1 {
    font-size: 24px;
}

h2 {
    font-size: 18px;
}

h3 {
    font-size: 16px;
}
</style>

## Giới thiệu

Nhiều tổ chức đã xây dựng cơ sở hạ tầng của họ sử dụng [Amazon Elastic Compute Cloud (Amazon EC2)](https://aws.amazon.com/ec2/) và [Network Load Balancer (NLB)](https://aws.amazon.com/elasticloadbalancing/network-load-balancer/), thường với các chính sách bảo mật được xây dựng xung quanh địa chỉ IP tĩnh của NLB. Khi các tổ chức này áp dụng container hóa và chuyển sang [Amazon Elastic Kubernetes Service (Amazon EKS)](https://aws.amazon.com/eks/) cho các ứng dụng hiện đại của họ, họ phải đối mặt với thách thức đáng kể trong việc duy trì cấu hình endpoint hiện có của họ. Điều này có thể làm cho việc hiện đại hóa trở nên phức tạp và rủi ro, vì việc thay đổi cấu hình cân bằng tải có thể làm gián đoạn kết nối của khách hàng hoặc đòi hỏi những thay đổi DNS lớn.

Tin tốt là quá trình chuyển đổi này không nhất thiết phải là một nỗ lực tất cả hoặc không có gì. Trong bài đăng này, chúng tôi khám phá một [mẫu triển khai hybrid](https://aws.amazon.com/blogs/containers/patterns-for-targetgroupbinding-with-aws-load-balancer-controller/) cung cấp một con đường di chuyển mượt mà, ít rủi ro từ Amazon EC2 sang Amazon EKS.

## Triển khai hybrid

Tương tự như mẫu [triển khai blue/green](https://docs.aws.amazon.com/whitepapers/latest/overview-deployment-options/bluegreen-deployments.html), cách tiếp cận triển khai hybrid của chúng tôi hỗ trợ chạy ứng dụng đồng thời trên Amazon EKS và Amazon EC2 trong quá trình di chuyển. Chìa khóa cho chiến lược này là khả năng định tuyến lưu lượng thông qua bộ cân bằng tải hiện có của bạn đến cả hai triển khai bằng cách sử dụng TargetGroupBinding, dẫn đến một quá trình di chuyển có kiểm soát.

### Kiến trúc

![Hình 1: Sơ đồ luồng lưu lượng thể hiện việc di chuyển từ Amazon EC2 (màu xanh lá cây) sang Amazon EKS (màu xanh dương)](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2025/03/18/Picture1-8.png)

_Hình 1: Sơ đồ luồng lưu lượng thể hiện việc di chuyển từ Amazon EC2 (màu xanh lá cây) sang Amazon EKS (màu xanh dương)_

## Ưu điểm khi sử dụng cách tiếp cận triển khai hybrid {: style="font-size: 18px;"}

Cách tiếp cận triển khai hybrid mang lại những ưu điểm sau:

• **Di chuyển có kiểm soát:** Định tuyến lưu lượng dần dần đến workload EKS trong khi vẫn duy trì dịch vụ thông qua cơ sở hạ tầng EC2 hiện có của bạn, giảm đáng kể rủi ro di chuyển.

• **Rollback đơn giản:** Nhanh chóng chuyển hướng lưu lượng trở lại các instance EC2 nếu phát sinh vấn đề, cung cấp khả năng rollback đáng tin cậy trong quá trình di chuyển.

• **A/B testing:** So sánh hiệu suất giữa triển khai EC2 và EKS trong điều kiện thực tế, cung cấp quyết định dựa trên dữ liệu về cấu hình và phân bổ tài nguyên hiệu quả nhất.

• **Tính linh hoạt:** Sử dụng điểm mạnh của cả hai môi trường triển khai trong quá trình chuyển đổi, giúp tối ưu hóa việc đặt workload dựa trên yêu cầu cụ thể.

• **Giảm thiểu gián đoạn dịch vụ:** Giảm rủi ro downtime bằng cách vận hành đồng thời cả hai môi trường trong quá trình di chuyển.

• **Giảm thiểu rủi ro:** Xác thực triển khai container hóa với lưu lượng thực trong khi duy trì tùy chọn fallback, cung cấp tính liên tục kinh doanh.

## Điều kiện tiên quyết cho việc di chuyển

Bài đăng này được viết với giả định rằng bạn có hiểu biết cơ bản về container hóa Docker và các khái niệm Kubernetes (pods, events, namespaces, và deployments, v.v.).

Trước khi bắt đầu quá trình di chuyển, hãy đảm bảo bạn có sẵn các thành phần sau:

• **Cơ sở hạ tầng hiện có:** Trong ví dụ của chúng tôi, một [ứng dụng mẫu Retail Store](https://github.com/aws-containers/retail-store-sample-app) đang chạy trên Amazon EC2.

• **Yêu cầu về container:** Một ứng dụng đã được kiểm thử và container hóa, với container image được đẩy lên registry container, như [Amazon Elastic Container Registry (Amazon ECR)](https://aws.amazon.com/ecr/).

• **Môi trường Amazon EKS:** [Cluster EKS với phiên bản Kubernetes được hỗ trợ](https://docs.aws.amazon.com/eks/latest/userguide/kubernetes-versions.html#available-versions) trên nhiều [Availability Zones (AZs)](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/).

• **Công cụ:**
◦ [kubectl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html) đã được cài đặt và cấu hình để tương tác với cluster Amazon EKS.
◦ [AWS Command Line Interface (AWS CLI)](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) đã được cài đặt và cấu hình với [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/) phù hợp.
◦ [AWS Load Balancer Controller](https://docs.aws.amazon.com/eks/latest/userguide/lbc-helm.html) đã được cài đặt trên cluster Amazon EKS.

## Di chuyển ứng dụng của bạn sử dụng triển khai hybrid với NLB {: style="font-size: 18px;"}

### Các bước di chuyển chi tiết {: style="font-size: 16px;"}

Bước đầu tiên là tạo một target group mới:

```bash
TARGET_GROUP_ARN=$(aws elbv2 create-target-group \
    --name eks-green \
    --protocol TCP \
    --port 80 \
    --target-type ip \
    --vpc-id <VPCID> \
    --query 'TargetGroups[0].TargetGroupArn' \
    --output text)
```

ARN (Amazon Resource Name) của target group được lưu vào biến TARGET_GROUP_ARN. Sau đó, xác minh rằng cả hai target group (Amazon EC2 và Amazon EKS) được cấu hình với `Terminate connections on deregistration` là true.

```bash
aws elbv2 describe-target-group-attributes \
    --target-group-arn $TARGET_GROUP_ARN \
    --query 'Attributes[*]' --output text | \
    grep deregistration_delay.connection_termination.enabled
```

Quan sát output sau:

`deregistration_delay.connection_termination.enabled true`

Nếu output của lệnh trả về thuộc tính `false`, điều đó có nghĩa là tính năng này chưa được kích hoạt. Để kích hoạt, sử dụng lệnh sau:

```bash
aws elbv2 modify-target-group-attributes \
    --target-group-arn $TARGET_GROUP_ARN \
    --attributes 'Key=deregistration_delay.connection_termination.enabled,Value=true' \
    --query 'Attributes[*]' --output text | \
    grep deregistration_delay.connection_termination.enabled
```

Ở giai đoạn này, lưu lượng vẫn được hướng đến ứng dụng đang chạy trên Amazon EC2. Bây giờ bạn có thể triển khai ứng dụng đã container hóa trên cluster Amazon EKS:

```bash
kubectl create deployment myapp \
    --image public.ecr.aws/aws-containers/retail-store-sample-ui:0.8.1 \
    --replicas 2 --port=8080
```

Chúng ta có thể expose ứng dụng bằng cách tạo một service. Đây là file YAML cho service:

```yaml
cat << EOF > service.yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: myapp
  name: ui-service
  namespace: default
spec:
  ports:
  - port: 80
    targetPort: 8080
  selector:
    app: myapp
  type: ClusterIP
EOF
```

Chúng ta có thể apply nó:

```bash
kubectl apply -f service.yaml
```

Với ứng dụng đang chạy và được expose như một Kubernetes service, tạo một listener mới cho NLB hiện có:

```bash
aws elbv2 create-listener \
    --load-balancer-arn <NLB-ARN> \
    --protocol TCP --port 81 \
    --default-actions Type=forward,TargetGroupArn=$TARGET_GROUP_ARN
```

Hiện tại bạn có một listener trên cổng 80. Listener này tiếp tục chuyển tiếp lưu lượng đến target group được liên kết với các instance EC2. Listener mới được tạo chuyển tiếp lưu lượng đến target group được liên kết với Amazon EKS. Nó không có bất kỳ target nào cho đến khi bạn sử dụng TargetGroupBinding để liên kết service với target group mới. Chúng ta có thể tạo nó:

```yaml
cat << EOF > tg-binding.yaml
apiVersion: elbv2.k8s.aws/v1beta1
kind: TargetGroupBinding
metadata:
  name: ui-tgbinding
spec:
  serviceRef:
    name: ui-service # Tên service
    port: 80 # Cổng service
  targetGroupARN: $TARGET_GROUP_ARN
EOF
```

Apply manifest:

```bash
kubectl apply -f tg-binding.yaml
```

Bạn có thể xác minh rằng các target được đăng ký đúng cách vào target group Amazon EKS. Cho các target đủ thời gian để vượt qua kiểm tra sức khỏe, sau đó xác minh rằng các target mới có thể phục vụ lưu lượng thành công. Nếu kiểm tra sức khỏe thất bại, hãy xác minh rằng Security Group của node Amazon EKS cho phép lưu lượng cần thiết. Để xác nhận chức năng phù hợp, hãy thử truy cập ứng dụng thông qua listener mới để đảm bảo nó đang được phục vụ như dự định trước khi tiến hành thêm.

Trước khi bắt đầu di chuyển, bạn cần tạo một listener khác trỏ đến target group EC2 hiện có:

```bash
aws elbv2 create-listener \
    --load-balancer-arn <NLB-ARN> \
    --protocol TCP --port 82 \
    --default-actions Type=forward,TargetGroupArn=<EC2-TARGET-GROUP-ARN>
```

Sau bước này, NLB có ba listener (cổng 80, 81 và 82), nơi bạn đã tạo thêm hai listener để thực hiện hoạt động di chuyển lưu lượng mượt mà. Số cổng được sử dụng trong bài đăng này là ví dụ, và bạn có thể chọn số cổng để phản ánh nhu cầu ứng dụng của bạn. Chúng tôi khuyên bạn nên kiểm tra xem lưu lượng đến các target group hiện có có được phục vụ trên listener mới hay không. Điều này đảm bảo rằng cấu hình NLB đã sẵn sàng để tiến hành các bước tiếp theo.

### Di chuyển lưu lượng từ Amazon EC2 sang target group Amazon EKS {: style="font-size: 16px;"}

Cả hai target group đều khỏe mạnh, và tất cả các listener đều sẵn sàng xử lý lưu lượng, vì vậy đã đến lúc di chuyển lưu lượng. Đầu tiên, cấu hình listener hiện có trên cổng 80 để gửi lưu lượng đến target group `eks-green`:

```bash
aws elbv2 modify-listener \
    --listener-arn <NLB-Listen-80> \
    --default-actions Type=forward,TargetGroupArn=$TARGET_GROUP_ARN
```

Thay đổi cấu hình này đảm bảo rằng tất cả các luồng mới được chuyển hướng đến target group mới. Vì các target đã vượt qua kiểm tra sức khỏe của họ khi được liên kết với listener trên cổng 81, điều này giúp tăng tốc quá trình này.

Thay đổi listener này có thể mất vài phút để lan truyền. Do đó, chúng tôi đề xuất bạn theo dõi lưu lượng đi đến các target trong target group mới trước khi tiến hành các bước tiếp theo. Trong thời gian này, điều quan trọng là phải theo dõi hành vi và số liệu hiệu suất của ứng dụng của bạn. Bạn có thể theo dõi trạng thái sức khỏe của target bằng cách sử dụng:

```bash
aws elbv2 describe-target-health \
    --target-group-arn $TARGET_GROUP_ARN
```

Mặc dù các kết nối hiện có sẽ không bị ảnh hưởng, các kết nối mới sẽ ngừng định tuyến đến target group cũ sau khi hoàn thành di chuyển lưu lượng. Sau khi xác nhận rằng các target mới đang xử lý lưu lượng thành công và các target tồn tại trước đó không còn phục vụ lưu lượng nữa, lấy danh sách các target từ target group EC2 tồn tại trước đó để chuẩn bị hủy đăng ký:

```bash
aws elbv2 describe-target-health \
    --target-group-arn <EC2-TARGET-GROUP-ARN> \
    --query 'TargetHealthDescriptions[*].Target.Id' \
    --output text
```

Lệnh này xuất ra danh sách các ID instance. Đối với mỗi ID instance, chạy lệnh `deregister-targets`:

```bash
aws elbv2 deregister-targets \
    --target-group-arn <EC2-TARGET-GROUP-ARN> \
    --targets Id=<InstanceID>
```

Bước hủy đăng ký rất quan trọng vì target group EC2 vẫn được liên kết với NLB thông qua listener cổng 82. Khi được thực hiện, lệnh gọi deregister-targets thực thi `Connection termination on deregistration`, điều này kết thúc các kết nối hiện có đến các target cũ. Khi khách hàng kết nối lại, họ được định tuyến đến các target của target group Amazon EKS mới.

### Quy trình rollback về target group ban đầu (Nếu cần) {: style="font-size: 16px;"}

Nếu bạn cần rollback về target group EC2 ban đầu, hãy làm theo các bước sau:

1. Đăng ký lại tất cả các target ban đầu vào target group EC2:

```bash
aws elbv2 register-targets \
    --target-group-arn <EC2-TARGET-GROUP-ARN> \
    --targets Id=<InstanceID1> Id=<InstanceID2>
```

2. Đợi các target vượt qua kiểm tra sức khỏe. Theo dõi trạng thái sức khỏe của họ:

```bash
aws elbv2 describe-target-health \
    --target-group-arn <EC2-TARGET-GROUP-ARN>
```

3. Cấu hình lại listener trên cổng 80 trên NLB để gửi lưu lượng đến target group EC2:

```bash
aws elbv2 modify-listener \
    --listener-arn <NLB-Listen-80> \
    --default-actions Type=forward,TargetGroupArn=<EC2-TARGET-GROUP-ARN>
```

### Dọn dẹp sau di chuyển {: style="font-size: 16px;"}

Nếu việc di chuyển đã thành công (không cần rollback), thì bạn có thể tiến hành các hoạt động dọn dẹp. Điều này bao gồm việc xóa hai listener bổ sung mà bạn đã tạo trên cổng 81 và 82, vì chúng chỉ cần thiết cho quá trình di chuyển. Cuối cùng, bạn có thể xóa an toàn target group EC2, vì nó không còn nhận bất kỳ lưu lượng nào nữa.

```bash
aws elbv2 delete-listener \
     --listener-arn <Listen-Port81-ARN>

aws elbv2 delete-listener \
     --listener-arn <Listen-Port82-ARN>

aws elbv2 delete-target-group \
    --target-group-arn <EC2-TG-ARN>
```

## Kết luận {: style="font-size: 18px;"}

Mẫu triển khai hybrid sử dụng NLB và TargetGroupBinding cung cấp một cách tiếp cận thực tế, ít rủi ro để di chuyển ứng dụng sang Amazon EKS từ nhiều nguồn khác nhau, bao gồm Amazon EC2, cơ sở hạ tầng on-premises, hoặc các giải pháp điều phối container khác. Duy trì cấu hình NLB hiện có, trong khi dần dần chuyển lưu lượng sang workload được container hóa, cho phép phương pháp này hỗ trợ chuyển đổi mượt mà và cung cấp khả năng rollback tích hợp. Mặc dù chúng tôi đã tập trung vào việc di chuyển từ Amazon EC2 sang Amazon EKS, tính linh hoạt của mẫu này mở rộng cho nhiều kịch bản khác nhau, bao gồm chuyển đổi từ cơ sở hạ tầng on-premises hoặc các giải pháp điều phối container khác.

Những cải tiến gần đây cho AWS Load Balancer Controller, đặc biệt là việc giới thiệu [target group MultiCluster](https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/guide/use_cases/multi_cluster/), mở rộng thêm các khả năng này. Các tổ chức giờ đây có thể quản lý workload trên nhiều cluster Kubernetes và tích hợp với các tài nguyên không thuộc cluster, tạo điều kiện cho các chiến lược di chuyển phức tạp hơn và kiến trúc ứng dụng phân tán. Cách tiếp cận hybrid này đóng vai trò như một bản thiết kế đáng tin cậy cho việc hiện đại hóa, cung cấp các công cụ cần thiết để duy trì tính liên tục kinh doanh và giảm thiểu rủi ro đồng thời cung cấp tính linh hoạt để thích ứng với các yêu cầu cơ sở hạ tầng đang phát triển.

Để tiếp tục hành trình di chuyển của bạn, chúng tôi khuyên bạn nên đọc bài đăng đồng hành của chúng tôi: [Di chuyển từ Kubernetes tự quản lý sang Amazon EKS: Đây là một số cân nhắc chính](https://aws.amazon.com/blogs/containers/migrating-from-self-managed-kubernetes-to-amazon-eks-here-are-some-key-considerations/). Bài đăng này cung cấp thêm những hiểu biết sâu sắc và thực hành tốt nhất bổ sung cho chiến lược triển khai hybrid được thảo luận ở đây, đặc biệt nếu bạn đang di chuyển từ môi trường Kubernetes tự quản lý sang Amazon EKS.

**TAGS:** [EKS](https://aws.amazon.com/blogs/containers/tag/eks/), [elb](https://aws.amazon.com/blogs/containers/tag/elb/), [nlb](https://aws.amazon.com/blogs/containers/tag/nlb/)
