---
title: "Event 5"
date: 2025-11-29T08:30:00+07:00
weight: 1
chapter: false
pre: " <b> 4.5. </b> "
---

# Summary Report: “Cloud Mastery Series #2: DevOps on AWS”

## Mục tiêu sự kiện

### Nâng cao kiến ​​thức về DevOps và Kỹ thuật đám mây

- Cung cấp cho người tham gia hiểu biết sâu sắc về các thực tiễn DevOps và cơ sở hạ tầng đám mây sử dụng các công cụ và dịch vụ của AWS.

- Giúp thu hẹp khoảng cách giữa quy trình phát triển truyền thống và văn hóa DevOps hiện đại, bao gồm tự động hóa, CI/CD, container hóa và cơ sở hạ tầng dưới dạng mã.

### Trải nghiệm thực tế với các công cụ DevOps của AWS

- Trình bày các dịch vụ DevOps thực tế của AWS: đường dẫn CI/CD, dịch vụ container, Cơ sở hạ tầng dưới dạng mã (IaC), giám sát và khả năng quan sát.

- Cho phép người tham gia trải nghiệm các bản demo trực tiếp và quy trình làm việc từ lập trình đến triển khai và vận hành trên AWS.

### Trao quyền cho kỹ sư xây dựng hệ thống có khả năng mở rộng và đáng tin cậy

- Trang bị cho người tham gia kiến ​​thức và các thực tiễn tốt nhất cần thiết để thiết kế, triển khai và duy trì các hệ thống có khả năng mở rộng, dễ bảo trì và dễ quan sát trong môi trường sản xuất.

- Giúp người tham gia áp dụng tư duy và thực tiễn DevOps, việc triển khai giúp cải thiện tần suất, tính ổn định, khả năng mở rộng và sự hợp tác nhóm.

### Hỗ trợ phát triển sự nghiệp và nâng cao năng lực về điện toán đám mây

- Hỗ trợ hành trình trở thành kỹ sư điện toán đám mây hoặc chuyên viên DevOps giỏi hơn của người tham gia.

- Cung cấp thông tin rõ ràng về lộ trình chứng nhận AWS và con đường sự nghiệp DevOps trong môi trường điện toán đám mây.

## Diễn giả

-

## Điểm nổi bật

### Thách thức khi quản lý hạ tầng thủ công (“ClickOps”)

- Quá trình triển khai tốn thời gian, gây trì hoãn.
- Dễ phát sinh lỗi thủ công và cấu hình không đồng nhất giữa các môi trường.
- Khó khăn trong hợp tác nhóm và duy trì cấu hình có thể tái tạo.

### Giới thiệu Infrastructure as Code (IaC)

- Quản lý tài nguyên đám mây thông qua mã thay vì thao tác thủ công trên giao diện.
- Lợi ích: tự động hóa, khả năng mở rộng, tái tạo và giảm thiểu lỗi trong provisioning.

### AWS CloudFormation

- Dịch vụ IaC gốc của AWS, dùng YAML hoặc JSON để định nghĩa và triển khai stack tài nguyên.
- Tự động tạo, cập nhật và xóa các tài nguyên theo nhóm.
- Hỗ trợ phát hiện drift để nhận biết và xử lý các sai lệch so với template.

### AWS Cloud Development Kit (CDK)

- Framework cho phép định nghĩa IaC bằng các ngôn ngữ lập trình quen thuộc như Python, TypeScript, Java.
- Các construct ở nhiều cấp độ: L1 (mapping trực tiếp CloudFormation), L2 (mặc định thân thiện với dev), L3 (pattern có sẵn).
- CLI hỗ trợ khởi tạo dự án, tổng hợp template, triển khai stack và kiểm tra drift.

### Lựa chọn công cụ IaC

- Xem xét môi trường đơn hay đa đám mây, trình độ nhóm (dev hay ops), và tính tương thích của hệ sinh thái.
- So sánh với Terraform (sử dụng HCL, hỗ trợ đa nhà cung cấp).

### Docker và container

- Container là đơn vị nhẹ, dễ di chuyển, chứa ứng dụng và các phụ thuộc.
- Dockerfile để xây dựng image, đảm bảo tính nhất quán giữa dev, test và production.
- Amazon ECR để lưu trữ, quét và quản lý image an toàn.

### Dịch vụ điều phối container AWS

- **Amazon ECS**: quản lý container Docker, hỗ trợ EC2 hoặc Fargate.
- **Amazon EKS**: chạy Kubernetes cluster với auto-scaling và cập nhật tự động.
- **AWS App Runner**: triển khai web app serverless từ code hoặc image.
- So sánh: ECS đơn giản, tích hợp AWS; EKS linh hoạt, theo chuẩn Kubernetes.

### CI/CD trên AWS

- Quản lý mã nguồn với **CodeCommit**, sử dụng GitFlow hoặc trunk-based development.
- Build & test với **CodeBuild**, triển khai với **CodeDeploy** (blue/green, canary, rolling).
- Orchestration bằng **CodePipeline** để tự động hóa toàn bộ quá trình.
- Demo pipeline hoàn chỉnh từ commit đến triển khai production.

### Giám sát và quan sát hệ thống

- **AWS CloudWatch**: thu thập metrics, logs, tạo dashboard & alert.
- **AWS X-Ray**: theo dõi request, phát hiện bottleneck hiệu suất.
- Thực hành tốt: alert, on-call, visibility toàn stack.

### Thực hành DevOps & case study

- Chiến lược nâng cao: feature flags, A/B testing, tích hợp automated testing.
- Quản lý sự cố: postmortem không đổ lỗi, học hỏi từ startup & enterprise.

## Những điểm rút ra

### Tư duy DevOps

- Hợp tác dev & ops để tăng tốc triển khai.
- Tập trung vào các chỉ số DORA để đo lường tốc độ & độ tin cậy.
- Văn hóa cải tiến liên tục dựa trên nhu cầu kinh doanh.

### Thực hành kỹ thuật

- Sử dụng IaC để quản lý hạ tầng tự động, version-controlled.
- Dùng CDK construct để tái sử dụng pattern, phù hợp setup phức tạp.
- Triển khai container với ECS/EKS dựa trên workload & kỹ năng nhóm.
- Xây dựng CI/CD pipeline mạnh để release thường xuyên, rủi ro thấp.

### Quan sát & độ tin cậy

- Tích hợp CloudWatch & X-Ray để giám sát chủ động, xử lý sự cố nhanh.
- Dùng chiến lược triển khai canary để giảm downtime.
- Kiểm tra drift định kỳ, áp dụng lifecycle policy cho container.

### Tiếp cận hiện đại

- Đánh giá setup hiện tại trước khi chuyển sang microservices hoặc container.
- Triển khai theo giai đoạn, thử nghiệm App Runner cho kết quả nhanh.
- Đo lường hiệu quả qua tiết kiệm chi phí, tốc độ lặp nhanh, cải thiện agility.

### Ứng dụng vào công việc

- Tích hợp Git & CodePipeline vào workflow hiện tại để tự động hóa.
- Thử nghiệm CDK trong pilot project để nâng cao năng suất dev.
- Thiết lập dashboard quan sát để cải thiện thời gian phản ứng sự cố.
- Tổ chức event storming để mô hình kiến trúc container.
- Theo đuổi chứng chỉ AWS DevOps để phát triển sự nghiệp.

## Trải nghiệm sự kiện

- **Học hỏi từ chuyên gia:** Các AWS Community Builder chia sẻ kiến thức thực tiễn, demo sinh động và ví dụ deployment microservices.
- **Học kỹ thuật thực hành:** Thực hành pipeline CI/CD, IaC và container, đánh giá trade-off giữa ECS & EKS, phát hiện drift, thiết lập monitoring.
- **Sử dụng công cụ AWS hiệu quả:** CDK đơn giản hóa IaC với code, App Runner hỗ trợ triển khai nhanh, tích hợp công cụ quan sát tối ưu hiệu suất ứng dụng.
- **Kết nối & tương tác:** Q&A, thảo luận nhóm giúp trao đổi ý tưởng về lựa chọn công cụ, phát triển nghề nghiệp, gắn công nghệ với mục tiêu kinh doanh.

### Bài học rút ra

- Từ thủ công sang tự động hóa IaC & CI/CD giúp giảm rủi ro, tăng hiệu quả.
- Cân bằng orchestrator container để mở rộng mà không quá phức tạp.
- Áp dụng observability & postmortem thúc đẩy văn hóa DevOps bền vững.
