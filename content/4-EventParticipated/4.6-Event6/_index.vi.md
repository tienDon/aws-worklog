---
title: "Event 6"
date: "2025-11-17"
weight: 6
chapter: false
pre: " <b> 4.6. </b> "
---

# Báo cáo Tóm tắt: “Cloud Mastery Series #3: Security on AWS”

## Mục tiêu Sự kiện

### Cung cấp Kiến thức Nền tảng về các Trụ cột Bảo mật của AWS

- Giới thiệu năm trụ cột của Khung Bảo mật Kiến trúc Tốt của AWS và giải thích vai trò của Trụ cột Bảo mật trong việc thiết kế kiến ​​trúc đám mây an toàn và bền vững.

### Tăng cường Kỹ năng Bảo mật Điện toán đám mây

- Trang bị cho người tham dự kiến ​​thức thiết yếu để xác định rủi ro, xây dựng lớp bảo vệ đa tầng và triển khai các biện pháp bảo mật tiêu chuẩn ngành trên AWS.

### Nâng cao Hiểu biết Thực tiễn thông qua Trình diễn

- Giúp người tham dự có được nhận thức thực tiễn thông qua các bản demo như mô phỏng chính sách IAM, các kịch bản phát hiện mối đe dọa, quy trình xử lý sự cố và các kỹ thuật bảo vệ tài nguyên.

### Thúc đẩy Kết nối và Chia sẻ Kiến thức

- Khuyến khích sự hợp tác và trao đổi kiến ​​thức trong cộng đồng kỹ sư AWS tại Việt Nam.

### Diễn giả

- **Kha Van (AWS)** – Người dẫn chương trình/Điều phối viên

- **Trần Đức Anh**: Thực tập sinh Kỹ sư An ninh đám mây, Đội trưởng Câu lạc bộ Đám mây AWS SGU

- **Nguyên Tuấn Thịnh**: Thực tập sinh Kỹ sư Đám mây

- **Nguyên Đỗ Thanh Đạt**: Thực tập sinh Kỹ sư Đám mây

- **Thịnh Lâm**: FCJer

- **Việt Nguyên**: FCJer

---

## Điểm nổi bật

### Mô hình Trách nhiệm Chia sẻ & Nền tảng An ninh

- Làm rõ sự phân chia trách nhiệm giữa AWS và khách hàng.

- Giới thiệu các nguyên tắc an ninh cốt lõi: _Quyền hạn tối thiểu_, _Không tin tưởng_ và _Phòng thủ theo chiều sâu_.

- Thảo luận về các lỗ hổng đám mây phổ biến và các mô hình đe dọa được quan sát thấy ở Việt Nam.

### Quản lý Danh tính & Truy cập (IAM)

- Bao gồm Người dùng IAM, Vai trò, Chính sách và các thực tiễn tốt nhất về bảo mật của AWS.

- Trình bày AWS IAM Identity Center (SSO), bộ quyền và quản lý danh tính tập trung.

- Tập trung vào việc thực thi xác thực đa yếu tố (MFA), xoay vòng thông tin xác thực và xác thực chính sách quản trị danh tính (IAM) bằng các công cụ mô phỏng.

### Phát hiện & Giám sát

- CloudTrail ở cấp độ Tổ chức để ghi nhật ký thống nhất.

- GuardDuty để thu thập thông tin tình báo về mối đe dọa và phát hiện các bất thường về hành vi.

- Security Hub để kiểm tra tư thế bảo mật tập trung dựa trên các thực tiễn tốt nhất của CIS và AWS.

- EventBridge được sử dụng để tự động hóa các hành động cảnh báo và khắc phục.

### Bảo vệ Cơ sở hạ tầng

- Bảo mật VPC: phân đoạn, cách ly mạng con, Nhóm bảo mật so với NACL.

- Sử dụng AWS WAF, AWS Shield và AWS Network Firewall.

- Bảo vệ khối lượng công việc: tăng cường bảo mật EC2, quét ảnh container và phát hiện mối đe dọa trong thời gian chạy.

### Bảo vệ Dữ liệu

- Mã hóa dữ liệu khi lưu trữ và khi truyền tải cho S3, EBS, RDS và các dịch vụ AWS khác.

- AWS KMS: chính sách khóa, xoay vòng khóa, cấp quyền và ranh giới quyền hạn.

- Secrets Manager và Parameter Store để quản lý vòng đời bí mật an toàn.
- Phân loại dữ liệu, các rào cản truy cập và các biện pháp kiểm soát quản trị.

### Ứng phó sự cố

- Giải thích vòng đời ứng phó sự cố AWS và các thực tiễn tốt nhất.

- Xem xét nhiều kịch bản thực tế:

- Thông tin đăng nhập IAM bị xâm phạm

- Các bucket S3 bị lộ công khai

- Phát hiện phần mềm độc hại trong khối lượng công việc trên đám mây

- Trình bày các quy trình làm việc để chụp ảnh nhanh, cách ly, thu thập nhật ký và khôi phục khối lượng công việc.

- Minh họa việc khắc phục tự động bằng Lambda và Step Functions.

---

## Những điểm chính cần ghi nhớ

### Tư duy bảo mật

- Bảo mật là một quá trình liên tục, không phải là thiết lập một lần.

- Áp dụng nguyên tắc _quyền hạn tối thiểu_ một cách nhất quán và thực thi quyền truy cập dựa trên vai trò.

- Xây dựng bảo mật ngay từ giai đoạn thiết kế, không phải sau khi triển khai.

### Các thực tiễn tốt nhất về bảo mật đám mây

- Bật ghi nhật ký bắt buộc: CloudTrail Organization, GuardDuty.

- Ưu tiên sử dụng vai trò IAM hơn là khóa truy cập dài hạn.

- Thực thi mã hóa mặc định trên tất cả các dịch vụ.
- Thực hiện phát hiện sai lệch cấu hình để duy trì tính nhất quán.

### Khả năng quan sát & Phát hiện mối đe dọa

- Kết hợp CloudWatch, Security Hub và GuardDuty để có khả năng quan sát chuyên sâu.

- Sử dụng cảnh báo dựa trên mức độ nghiêm trọng được tích hợp với Slack hoặc email.

- Triển khai theo dõi phân tán với X-Ray để khắc phục sự cố microservices.

### Chuẩn bị ứng phó sự cố

- Chuẩn hóa các kịch bản và hướng dẫn xử lý sự cố.

- Tự động hóa các phản hồi bảo mật cho các sự kiện có rủi ro cao.

- Tổ chức các ngày diễn tập bảo mật định kỳ để thực hành các tình huống thực tế.

### Áp dụng vào công việc

- Đánh giá lại các môi trường hiện tại để tuân thủ Well-Architected.

- Thiết lập bảo mật cơ bản cho IAM, ghi nhật ký, mạng và mã hóa.

- Triển khai Security Hub và GuardDuty trên các môi trường đa tài khoản.

- Tích hợp quét vào quy trình CI/CD và container.

- Tìm hiểu chứng chỉ AWS Security Specialty.

---

## Trải nghiệm sự kiện

- **Học hỏi từ các chuyên gia AWS:**

Người tham dự được hưởng lợi từ những hiểu biết thực tế, các phương pháp hay nhất và các bản demo thực tiễn do các kỹ sư AWS và các nhà xây dựng cộng đồng trình bày.

- **Học tập thực hành:**

Người tham dự được quan sát các mô phỏng trực tiếp về kiểm tra quyền truy cập IAM, thiết lập ghi nhật ký toàn tổ chức, phát hiện mối đe dọa của GuardDuty và quy trình phản ứng sự cố.

- **Sử dụng hiệu quả các công cụ bảo mật AWS:**

Các công cụ như CloudTrail, GuardDuty, Security Hub, KMS và WAF đã chứng minh cách xây dựng khả năng bảo vệ và giám sát liên tục.

- **Kết nối và tương tác cộng đồng:**
- Các phiên hỏi đáp và thảo luận nhóm cho phép người tham gia chia sẻ kinh nghiệm, thu được những hiểu biết về nghề nghiệp và điều chỉnh các quyết định kỹ thuật phù hợp với mục tiêu kinh doanh.

### Bài học kinh nghiệm

- Bảo mật đa lớp đảm bảo khả năng phục hồi ngay cả khi một lớp bị lỗi.

- Ghi nhật ký và giám sát là thiết yếu, không phải là tùy chọn.

- Tự động hóa giảm thiểu lỗi do con người và tăng tốc thời gian phản hồi.

- Phân tích sự cố không đổ lỗi và giao tiếp cởi mở giúp các nhóm liên tục cải thiện.
