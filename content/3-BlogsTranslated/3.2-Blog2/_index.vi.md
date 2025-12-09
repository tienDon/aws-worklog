---
title: "Blog 2"
date: "2025-12-09"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Nâng cao khả năng quan sát LLM với Amazon Bedrock và Dynatrace

**Tác giả:**

- Kristof Muhi, Principal Product Manager – Dynatrace
- Varun Jasti, Solutions Architect – AWS
- Shashiraj Jeripotula, Principal Partner Solutions Architect – AWS

_Ngày: 27 tháng 3, 2025_

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

Các tổ chức tận dụng [Amazon Bedrock](https://aws.amazon.com/bedrock/) cho các ứng dụng AI tạo sinh của họ cần đảm bảo hoạt động AI đáng tin cậy, bảo mật và có trách nhiệm ở quy mô lớn. Khi những ứng dụng này trở thành một phần không thể thiếu của các quy trình kinh doanh, việc triển khai khả năng quan sát Large Language Model (LLM) toàn diện trở nên thiết yếu. Giám sát hiệu suất mô hình, phát hiện ảo giác, tấn công prompt injection, ngôn ngữ độc hại và rò rỉ PII trong khi cũng theo dõi độ trễ, drift, dòng dữ liệu và duy trì kiểm soát chi phí là một số trường hợp sử dụng quan trọng. Bằng cách triển khai các thực hành quan sát mạnh mẽ, các nhóm có thể có được hiểu biết sâu sắc về hành vi ứng dụng LLM của họ, tối ưu hóa việc sử dụng tài nguyên, đảm bảo chất lượng phản hồi nhất quán và duy trì tuân thủ các yêu cầu quản trị.

[Dynatrace](https://www.dynatrace.com/) là một nền tảng quan sát tất cả trong một tự động thu thập thông tin sản xuất, truy vết, nhật ký, metrics và dữ liệu ứng dụng thời gian thực ở quy mô lớn. Với công cụ AI mạnh mẽ ([Davis AI](https://www.dynatrace.com/platform/artificial-intelligence/)), Dynatrace cảnh báo nhóm về các vấn đề cấp độ sản xuất trước khi chúng làm gián đoạn người dùng, giúp dự đoán việc sử dụng tài nguyên và chi phí, vấn đề hiệu suất, và cung cấp các rào cản bảo vệ dữ liệu và duy trì tuân thủ.

Trong bài đăng này, chúng tôi giải thích cách Dynatrace cung cấp giám sát end-to-end và khả năng hiển thị vào các ứng dụng AI tạo sinh sử dụng các mô hình Amazon Bedrock cho phép khả năng quan sát LLM toàn diện.

## Các trường hợp sử dụng quan sát LLM

Dynatrace giúp với các trường hợp sử dụng quan sát LLM và AI tạo sinh sau đây ở quy mô lớn.

### Độ phức tạp của việc truy vết đa mô hình

Truy vết đa mô hình đưa ra những phức tạp ẩn khi các tương tác giữa các mô hình với kiến trúc khác nhau, định dạng đầu ra và hồ sơ độ trễ phải được tương quan một cách mạch lạc trên toàn bộ chuỗi. Khi các mô hình đa dạng hoạt động theo chuỗi, lỗi có thể lan truyền âm thầm qua các hệ thống không đồng nhất này, làm cho phân tích nguyên nhân gốc trở nên đặc biệt thách thức mà không có telemetry được tiêu chuẩn hóa có thể hiệu quả kết nối các điểm giữa các đầu vào và đầu ra khác nhau.

Dynatrace cho phép truy vết end-to-end trên các mô hình khác nhau, kết nối các thành phần frontend và backend của stack ứng dụng.

Truy vết đa mô hình này cung cấp khả năng hiển thị và truy vết hoàn chỉnh các sự kiện, cho phép bạn hiểu điều gì đã xảy ra khi một vấn đề xảy ra hoặc khi một phản hồi không hợp lệ được gửi đến khách hàng trong toàn bộ chuỗi mô hình.

### Hoạt động dự đoán của khối lượng công việc AI – chi phí và hiệu suất

Hoạt động dự đoán tận dụng phân tích nâng cao và machine learning để dự đoán và tối ưu hóa hành vi khối lượng công việc AI trước khi các vấn đề tác động đến hoạt động kinh doanh được hỗ trợ bởi Davis AI. Cách tiếp cận chủ động này biến đổi giám sát truyền thống thành thông tin hoạt động hướng tương lai cho các hệ thống AI.

• **Dự báo và tối ưu hóa chi phí:** Dự báo việc sử dụng token, cuộc gọi API và chi phí liên quan trong Amazon Bedrock để cho phép lập kế hoạch ngân sách tốt hơn và phân bổ tài nguyên cho tương lai. Lập kế hoạch ngân sách hiệu quả với dự báo chi phí chính xác, giúp giảm chi phí vận hành thông qua lập kế hoạch tài nguyên và phân bổ tốt hơn.

• **Dự đoán suy giảm hiệu suất:** Xác định các dấu hiệu cảnh báo sớm về các vấn đề hiệu suất mô hình tiềm năng thông qua nhận dạng mẫu.

• **Phát hiện bất thường và vấn đề:** Sử dụng Davis AI dự đoán của Dynatrace để phát hiện các mẫu bất thường trong hành vi mô hình có thể chỉ ra các vấn đề mới nổi, mức sử dụng cao điểm trong kiến trúc. Điều này sẽ giảm thiểu thời gian ngừng hoạt động dịch vụ và ứng dụng bằng cách giải quyết các vấn đề tiềm năng trước khi chúng trở nên nghiêm trọng.

### Phân tích rào cản

Phân tích rào cản tập trung vào việc giám sát và thực thi các ranh giới an toàn xung quanh hệ thống AI để đảm bảo chúng hoạt động trong các tham số đạo đức, bảo mật và hiệu suất được xác định. Khả năng quan trọng này giúp các tổ chức duy trì kiểm soát đối với ứng dụng AI của họ trong khi bảo vệ chống lại các rủi ro tiềm năng và lạm dụng.

• Các thành phần chính như phát hiện thời gian thực các nỗ lực tấn công prompt injection và lỗ hổng bảo mật để bảo vệ doanh nghiệp và dữ liệu khách hàng của bạn. Điều này cho phép các tổ chức theo dõi việc lộ PII trái phép và rò rỉ dữ liệu nhạy cảm.

• Rào cản cho phép bạn giám sát ngôn ngữ độc hại và không phù hợp, nội dung có hại và phản hồi thiên vị với phát hiện mối đe dọa sớm. Cho phép cải thiện độ tin cậy mô hình thông qua thực thi ranh giới nhất quán và tuân thủ dễ dàng.

• Phân tích rào cản bảo vệ ứng dụng AI bằng cách bảo vệ danh tiếng thương hiệu bằng cách ngăn chặn các phản hồi và truy vấn không phù hợp.

### Quản trị dữ liệu, tuân thủ và kiểm toán

Trong bối cảnh các ứng dụng được xây dựng bằng LLM trên Amazon Bedrock, các khả năng quản trị, tuân thủ và kiểm toán thông qua khả năng quan sát đảm bảo các tổ chức duy trì kiểm soát, minh bạch và trách nhiệm giải trình cho các ứng dụng AI tạo sinh của họ trong khi đáp ứng các yêu cầu quy định và tiêu chuẩn ngành.

Dynatrace giúp theo dõi mọi đầu vào và đầu ra để có một trail kiểm toán đầy đủ. Nó cho phép bạn truy vấn tất cả dữ liệu trong thời gian thực và lưu trữ nó để tham khảo trong tương lai. Nó dễ dàng thiết lập và duy trì dòng dữ liệu đầy đủ từ prompt đến phản hồi trên toàn bộ pipeline và thu thập tất cả bằng chứng cho các thực hành AI có trách nhiệm và báo cáo quy định như [FIPS](https://www.nist.gov/standardsgov/compliance-faqs-federal-information-processing-standards-fips), [FedRAMP](https://www.fedramp.gov/) và [EU AI Act](https://artificialintelligenceact.eu/).

Khả năng dấu vân tay mô hình của Dynatrace tạo ra các định danh duy nhất cho các phiên bản LLM dựa trên kiến trúc, dữ liệu training và tham số, cho phép theo dõi phiên bản chính xác để tuân thủ quy định và kiểm toán. Việc theo dõi chính xác các phiên bản mô hình thông qua dấu vân tay mô hình để đáp ứng các yêu cầu quy định và kiểm toán.

### Dynatrace + Các lớp quan sát LLM

Quan sát LLM đòi hỏi một cách tiếp cận mở rộng trải rộng trên nhiều lớp, từ ứng dụng hướng người dùng đến cơ sở hạ tầng cơ bản. Mỗi lớp đóng một vai trò quan trọng trong việc hiểu hiệu suất LLM, xác định bottleneck, đảm bảo hoạt động đáng tin cậy và phát hiện các rủi ro bảo mật tiềm năng. Dynatrace cung cấp một nền tảng quan sát end-to-end thống nhất có thể giúp các tổ chức có được hiểu biết sâu sắc về từng lớp này cho phép họ hiệu quả giám sát, tối ưu hóa, khắc phục sự cố và bảo mật các ứng dụng được hỗ trợ bởi LLM của họ.

![Hình 1: Pipeline quan sát Bedrock của ứng dụng du lịch chạy trên Kubernetes sử dụng Dynatrace](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2025/03/27/Picture1-17.png)

_Hình 1: Pipeline quan sát Bedrock của ứng dụng du lịch chạy trên Kubernetes sử dụng Dynatrace_

Trong ví dụ của chúng tôi, ứng dụng chạy trong một cluster Kubernetes. [OpenLLMetry](https://github.com/traceloop/openllmetry) của [Traceloop](https://www.traceloop.com/) tăng cường khả năng quan sát LLM cho các mô hình Amazon Bedrock bằng cách thu thập các KPI cụ thể về AI quan trọng. Nó làm phong phú dữ liệu [OpenTelemetry](https://opentelemetry.io/) và tích hợp liền mạch với Dynatrace. Điều này cung cấp một cái nhìn toàn diện về hiệu suất ứng dụng LLM trong môi trường sản xuất. Cuối cùng, nó trao quyền cho doanh nghiệp tối ưu hóa và mở rộng các triển khai AI của họ một cách hiệu quả.

![Hình 2: Tổng quan cấp cao về các lớp khác nhau của việc thiết bị đo đạc ứng dụng AI tạo sinh cho khả năng quan sát](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2025/03/26/bedrock-highscale-1.png)

_Hình 2: Tổng quan cấp cao về các lớp khác nhau của việc thiết bị đo đạc ứng dụng AI tạo sinh cho khả năng quan sát_

Từ sơ đồ trên (Hình 2), Dynatrace cung cấp khả năng hiển thị end-to-end của các ứng dụng AI thông qua toàn bộ stack công nghệ.

• **Lớp ứng dụng:** Dynatrace giám sát các ứng dụng hướng người dùng tương tác với LLM, theo dõi metrics hiệu suất, trải nghiệm người dùng và các mẫu sử dụng. Thu thập dữ liệu liên tục cho toàn bộ kiến trúc (frontend, backend, stack AI tạo sinh) tiết lộ hành vi ứng dụng thời gian thực, trong khi logging thu thập các tương tác người dùng và lỗi cụ thể ứng dụng để debugging. Các công cụ trực quan hóa cung cấp dashboard có thể tùy chỉnh để theo dõi các metrics ứng dụng chính và xác định xu hướng hoặc bất thường liên quan đến tích hợp LLM.

• **Lớp điều phối – Giám sát hiệu suất framework điều phối:** Các framework này (ví dụ: [LangChain](https://www.langchain.com/), [LlamaIndex](https://www.llamaindex.ai/)) quản lý workflow prompt và tích hợp pipeline. Dynatrace quan sát các workflow này, cung cấp metrics về hiệu quả prompt engineering, hiệu suất chuỗi và caching. Khả năng phát hiện bất thường của nó cảnh báo nhóm về các vấn đề tiềm năng, bottleneck, đảm bảo hoạt động mượt mà của các quy trình được điều khiển bởi AI.

• **Lớp semantic và cơ sở dữ liệu vector:** Phân tích ý nghĩa và nội dung của đầu vào và đầu ra LLM. Điều này liên quan đến việc hiểu các mối quan hệ giữa các khái niệm, theo dõi sentiment và xác định các thiên vị tiềm năng, sự không chính xác hoặc bất thường cùng với bottleneck hiệu suất trong kiến trúc Retrieval Augmented Generation (RAG) sử dụng cơ sở dữ liệu vector (ví dụ: Pinecone, Milvus, Weaviate, Qdrant, Chroma). Tính mở rộng của Dynatrace cho phép tích hợp với các công cụ phân tích semantic. Bằng cách thu thập dữ liệu từ cơ sở dữ liệu vector, Dynatrace có thể cung cấp một cái nhìn thống nhất về đầu ra LLM, bao gồm phân tích sentiment, mô hình hóa chủ đề và phát hiện thiên vị. Dữ liệu này sau đó có thể được trực quan hóa và phân tích bằng cách sử dụng khả năng Phân tích Metrics & Hiệu suất và Trực quan hóa của Dynatrace.

• **Lớp mô hình – Quan sát các nhà cung cấp mô hình và nhà cung cấp nền tảng:** Dynatrace giám sát việc sử dụng token, tính ổn định, độ trễ, throughput, tiêu thụ tài nguyên và drift mô hình trong Amazon Bedrock. Phân tích Metrics & Hiệu suất cho phép đi sâu vào hiệu suất mô hình, theo dõi các metrics như độ trễ, throughput và tiêu thụ tài nguyên. Dấu vân tay mô hình hỗ trợ theo dõi phiên bản chi tiết, trong khi phát hiện bất thường đánh dấu các thay đổi đáng kể trong hiệu suất hoặc chất lượng đầu ra—giúp nhóm hiểu và tối ưu hóa hành vi mô hình.

• **Lớp cơ sở hạ tầng:** Khả năng quan sát full-stack của Dynatrace mở rộng đến tài nguyên tính toán (ví dụ: Amazon EC2, NVIDIA GPU) và mạng. Nó tự động thu thập utilization CPU/GPU, sử dụng bộ nhớ và các thống kê quan trọng khác. Phát hiện bất thường thời gian thực với Davis AI giúp nhóm nhanh chóng giải quyết các bottleneck phần cứng có thể tác động đến hiệu suất LLM.

_"Từ đánh giá mô hình ban đầu đến triển khai sản xuất, giám sát toàn diện là rất quan trọng đối với các hệ thống AI tạo sinh. Việc tích hợp giữa Dynatrace và Amazon Bedrock cho phép các tổ chức dễ dàng theo dõi các chỉ số hiệu suất chính và dữ liệu truy vết, đảm bảo các ứng dụng AI của họ vẫn được tối ưu hóa và hoạt động đáng tin cậy."_ – Denis Batalov, Tech Leader, ML & AI, AWS.

_"AI tạo sinh đang nhanh chóng trở thành tiêu chuẩn cho trải nghiệm khách hàng, thúc đẩy các công ty cung cấp các tương tác AI-native với tốc độ cao. Đồng thời, chúng ta đang chứng kiến ​​một sự phát triển được tăng tốc của các hệ thống AI, dẫn đến khả năng tăng theo cấp số nhân. Tuy nhiên, việc triển khai các stack ứng dụng AI phức tạp cao này trong sản xuất đưa ra những thách thức đáng kể. Khả năng quan sát AI đóng vai trò quan trọng trong việc đảm bảo hiệu suất đáng tin cậy, tăng cường sự hài lòng của khách hàng và thúc đẩy ROI có thể đo lường được cho doanh nghiệp."_ – Alois Reitbauer VP Chief Technology Strategist, Dynatrace

## Tóm tắt

Trong bài đăng blog này, chúng tôi đã thảo luận về cách Dynatrace có thể cung cấp khả năng hiển thị nâng cao vào các ứng dụng AI tạo sinh tận dụng Amazon Bedrock.

Tận dụng các khả năng của Dynatrace, bạn có thể:

• **Duy trì hiệu quả hoạt động:** Giám sát độ trễ, sử dụng tài nguyên và chi phí để tối ưu hóa hiệu suất và kiểm soát chi phí.

• **Tăng tốc con đường đến sản xuất:** Triển khai các ứng dụng AI đáng tin cậy và bảo mật nhanh hơn với sự tự tin.

• **Đưa ra quyết định dựa trên dữ liệu:** Tận dụng dữ liệu toàn diện để thông báo cho việc lựa chọn mô hình, fine-tuning và các chiến lược giảm thiểu rủi ro.

• **Cải thiện độ tin cậy ứng dụng:** Chủ động xác định và giải quyết bottleneck hiệu suất và các vấn đề khác trước khi chúng tác động đến người dùng.

• **Tăng cường tình trạng bảo mật:** Phát hiện và giảm thiểu rủi ro bảo mật trong thời gian thực, bảo vệ dữ liệu và danh tiếng của bạn.

• **Tăng cường quản trị và tuân thủ:** Duy trì dòng dữ liệu rõ ràng và đảm bảo các thực hành AI có trách nhiệm, đáp ứng các yêu cầu quy định và tiêu chuẩn đạo đức.

Để biết hướng dẫn về cách thiết lập giải pháp thiết bị đo đạc end-to-end của Dynatrace với Amazon Bedrock, vui lòng tham khảo [blog](https://www.dynatrace.com/news/blog/deliver-secure-safe-and-trustworthy-genai-applications-with-amazon-bedrock-and-dynatrace/) Dynatrace sau.

## Dynatrace – AWS Partner Spotlight

Dynatrace là AWS Advanced Technology Partner và AWS Competency Partner cung cấp phần mềm thông minh để đơn giản hóa độ phức tạp cloud và tăng tốc chuyển đổi số. Với khả năng quan sát nâng cao, AI và tự động hóa hoàn toàn, nền tảng tất cả trong một của chúng tôi cung cấp câu trả lời, không chỉ dữ liệu, về hiệu suất của ứng dụng, cơ sở hạ tầng cơ bản và trải nghiệm của tất cả người dùng.

[Liên hệ Dynatrace](https://partnercentral.awspartner.com/PartnerConnect?id=001E000000texmiIAA&source=Blog&campaign=) | [Tổng quan đối tác](https://partners.amazonaws.com/partners/001E000000texmiIAA/Dynatrace) | [AWS Marketplace](https://aws.amazon.com/marketplace/seller-profile?id=1422b3b0-b081-4af9-9d2b-34e6eb924f05)

**TAGS:** [Amazon Bedrock](https://aws.amazon.com/blogs/apn/tag/amazon-bedrock/), [Artificial Intelligence](https://aws.amazon.com/blogs/apn/tag/artificial-intelligence/), [Machine Learning](https://aws.amazon.com/blogs/apn/tag/machine-learning/), [Observability](https://aws.amazon.com/blogs/apn/tag/observability/)
