---
title: "Blog 4"
date: "2025-12-09"
weight: 1
chapter: false
pre: " <b> 3.4. </b> "
---

# Lựa Chọn Phương Thức Thực Thi Phù Hợp Cho Sản Phẩm SaaS Của Bạn Trên AWS Marketplace

**Tác giả:**

Pawan Kumar, Quản Lý Tài Khoản Kỹ Thuật tại Amazon Web Services

_Ngày: 28 tháng 3 năm 2025_

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

[AWS Marketplace](https://aws.amazon.com/marketplace/), các nhà cung cấp phần mềm độc lập (ISV) và các đối tác tư vấn (CP) cần cung cấp các phương thức thực thi khi ra mắt sản phẩm phần mềm dưới dạng dịch vụ (SaaS) trên AWS Marketplace. Việc lựa chọn phương thức thực thi phù hợp là rất quan trọng. Lựa chọn này ảnh hưởng đến cách khách hàng truy cập sản phẩm của bạn và thực sự có thể tác động đến trải nghiệm của họ. Hãy cùng khám phá các tùy chọn thực thi có sẵn để giúp bạn đưa ra lựa chọn sáng suốt cho dịch vụ SaaS của mình.

## Điều kiện tiên quyết

Trước khi chọn một tùy chọn thực thi, bạn phải đăng ký làm người bán trên AWS Marketplace. Để biết thêm thông tin, hãy xem [Đăng ký làm người bán trên AWS Marketplace](https://docs.aws.amazon.com/marketplace/latest/userguide/seller-registration-process.html) trong Hướng dẫn dành cho người bán trên AWS Marketplace.

## Các tùy chọn thực thi

AWS Marketplace cho phép bạn chọn từ hai tùy chọn thực thi khi niêm yết sản phẩm SaaS. Tùy chọn thực thi xác định trải nghiệm mà khách hàng của bạn có sau khi đăng ký sản phẩm của bạn trên AWS Marketplace.

1. **URL thực thi mặc định:** Tùy chọn này cho phép bạn thiết kế và quản lý toàn bộ trải nghiệm đăng ký. Nó hoạt động tốt cho các sản phẩm SaaS không yêu cầu thêm tài nguyên trong tài khoản AWS của khách hàng. Các chi tiết chính là:

• Khách hàng được chuyển hướng đến trang đăng ký sản phẩm của bạn sau khi đăng ký.

• Với tư cách là nhà cung cấp, bạn kiểm soát toàn bộ trải nghiệm đăng ký và cung cấp cho khách hàng các bước để truy cập sản phẩm.

2. **Khởi chạy nhanh SaaS:** Tùy chọn này hoạt động tốt nếu sản phẩm SaaS của bạn yêu cầu các tài nguyên AWS được triển khai trong tài khoản của khách hàng. Ví dụ, các nhà cung cấp triển khai [vai trò Quản lý danh tính và truy cập AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html), cơ sở dữ liệu hoặc tác nhân trong tài khoản AWS của khách hàng có thể đơn giản hóa trải nghiệm đăng ký cho khách hàng của họ. Các chi tiết chính là:

• Khởi chạy nhanh SaaS sử dụng các tích hợp để tạo ngăn xếp [AWS CloudFormation](https://aws.amazon.com/cloudformation/) nhằm triển khai tài nguyên với ít thao tác chuyển đổi ngữ cảnh hơn cho khách hàng.

• Các bí mật triển khai có thể được lưu trữ trong [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/) của khách hàng và được AWS CloudFormation sử dụng trong quá trình triển khai. Điều này giúp khách hàng không cần phải sao chép và dán các tham số triển khai.

• Nó cung cấp hướng dẫn từng bước, bao gồm cả cơ chế xác minh ủy quyền tích hợp để đảm bảo khách hàng có thông tin đăng nhập AWS cần thiết.

• Các sản phẩm có SaaS Quick Launch sẽ hiển thị thẻ Quick Launch trong phần mô tả.

Để biết thêm thông tin, hãy xem [Kích hoạt SaaS Quick Launch](https://catalog.workshops.aws/mpseller/en-US/saas/quick-launch-integration).

## Kết luận và các bước tiếp theo

Trong bài viết này, chúng ta đã đề cập đến hai tùy chọn thực thi dành cho các sản phẩm SaaS trên AWS Marketplace. Sau khi chọn tùy chọn thực thi phù hợp nhất với nhu cầu của mình, bạn có thể tiến hành niêm yết sản phẩm SaaS của mình trên AWS Marketplace. Bạn có thể thấy các tài nguyên sau đây hữu ích khi bắt đầu quá trình niêm yết.

• [Bài tập thực hành: Tạo trang thông tin sản phẩm SaaS](https://catalog.workshops.aws/mpseller/en-US/saas/create-listing)

• [Bài tập thực hành: Tích hợp sản phẩm SaaS của bạn](https://catalog.workshops.aws/mpseller/en-US/saas/integration)

• [Bài tập thực hành: Kích hoạt tính năng Khởi chạy nhanh sản phẩm SaaS](https://catalog.workshops.aws/mpseller/en-US/saas/quick-launch-integration)

• [Kiểm tra thành công trang thông tin sản phẩm SaaS của bạn trên AWS Marketplace](https://aws.amazon.com/blogs/awsmarketplace/successfully-testing-your-saas-listing-in-aws-marketplace/)

• [Cập nhật khả năng hiển thị sản phẩm] [Sản phẩm](https://docs.aws.amazon.com/marketplace/latest/userguide/saas-product-settings.html#saas-update-visibility)

## Giới thiệu về tác giả

Pawan Kumar là Quản lý Tài khoản Kỹ thuật tại Amazon Web Services, chuyên về các giải pháp AWS Marketplace và kiến ​​trúc điện toán phi máy chủ. Anh ấy phát triển các chiến lược sáng tạo để giải quyết các thách thức phức tạp của khách hàng. Mục tiêu của anh ấy là thúc đẩy việc áp dụng điện toán đám mây trong mọi ngành công nghiệp. Ngoài công việc, Pawan thích chơi cricket và theo dõi các giải đấu quốc tế.

**THẺ:** [AWS Marketplace](https://aws.amazon.com/blogs/awsmarketplace/category/software/aws-marketplace/), [Thực tiễn tốt nhất](https://aws.amazon.com/blogs/awsmarketplace/category/post-types/best-practices/), [Cơ bản (100)](https://aws.amazon.com/blogs/awsmarketplace/category/learning-levels/foundational-100/), [SaaS](https://aws.amazon.com/blogs/awsmarketplace/category/saas/), [Phần mềm](https://aws.amazon.com/blogs/awsmarketplace/category/software/)
