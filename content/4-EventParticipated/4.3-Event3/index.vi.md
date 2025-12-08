---
title: "Event 3"
date: 2024-12-06
weight: 1
chapter: false
pre: " <b> 4.3. </b> "
---


# Bài Thu Hoạch: "Vòng đời phát triển theo hướng AI: Tái định hình kỹ thuật phần mềm"

### Thông Tin Sự Kiện

**Ngày:** Thứ Sáu, 3 tháng 10, 2025  
**Địa điểm:** AWS Event Hall, L26 Bitexco Tower, TP. Hồ Chí Minh  
**Đơn vị tổ chức:** AWS Idolize Team  
**Số lượng tham gia:** Hơn 300 người đăng ký  
**Hình thức:** Offline - Trực tiếp tại Bitexco Tower

### Chương Trình Nghị Sự

- **14:00 - 14:15:** Đón tiếp
- **14:15 - 15:30:** Tổng quan về Vòng đời Phát triển theo AI và trình diễn Amazon Q Developer (do Toàn Huỳnh biên soạn)
- **15:30 - 15:45:** Nghỉ giải lao
- **15:45 - 16:30:** Trình diễn Kiro (do My Nguyen thực hiện)

### Bối Cảnh Sự Kiện

Sự trỗi dậy của **AI tạo sinh** đánh dấu một bước chuyển mình mang tính cách mạng trong phát triển phần mềm. AI tạo sinh tái định hình cách các nhà phát triển và tổ chức học hỏi, lập kế hoạch, tạo, triển khai và quản lý ứng dụng một cách an toàn.

Bằng cách tích hợp AI vào **vòng đời phát triển phần mềm** - từ kiến trúc đến phát triển, thử nghiệm, triển khai và bảo trì, các nhà phát triển có thể tự động hóa các tác vụ nặng không phân biệt. Việc tự động hóa này giúp tăng năng suất và cho phép các nhà phát triển tập trung vào các tác vụ sáng tạo, có giá trị cao hơn.

### Mục Đích Của Sự Kiện

- Khám phá **Phát triển theo hướng AI** bằng cách sử dụng Amazon Q Developer và Kiro
- Giới thiệu phương pháp luận AI-powered Software Development Lifecycle (AIDOC)
- Trình diễn ứng dụng thực tế của AI trong phát triển phần mềm
- Giới thiệu khả năng của Amazon Q Developer
- Trình diễn công cụ Kiro để tăng năng suất developer
- Chia sẻ best practices khi tích hợp AI vào quy trình phát triển

### Danh Sách Diễn Giả

- **Toàn Huỳnh** – Senior Solutions Architect, AWS
- **Mỹ Nguyễn** – Senior Prototyping Engineer, AWS

### Điều Phối Viên

- **Diễm My** – AWS Team
- **Đại Trường** – AWS Team
- **Đinh Nguyên** – AWS Team

### Nội Dung Nổi Bật

#### Tại Sao Cần AI Trong Phát Triển Phần Mềm

Nhiều developer đang sử dụng AI để tăng năng suất, nhưng vẫn còn những thách thức:

- **Các task đơn giản hoạt động tốt**, nhưng các dự án phức tạp gặp vấn đề
- **Thiếu phương pháp luận** để tích hợp AI vào toàn bộ vòng đời phát triển
- **Lo ngại về chất lượng** khi AI sinh ra lượng lớn code
- **Vấn đề quản lý context** với giới hạn token trong các dự án lớn

#### Phương Pháp Luận AI Development Lifecycle (AIDOC)

AIDOC không chỉ là một công cụ—đó là một **phương pháp luận toàn diện** giúp developer làm việc hiệu quả với AI trong suốt quá trình phát triển phần mềm.

**Nguyên Tắc Cốt Lõi:**

1. **Cộng tác Người-AI**: AI hỗ trợ, nhưng con người validate, ra quyết định và giám sát
2. **Giải quyết vấn đề đa bước**: Chia nhỏ task phức tạp thay vì prompt một lần
3. **Validation ở mỗi giai đoạn**: Review output của AI trước khi chuyển bước tiếp theo
4. **Developer làm chủ**: Developer chịu trách nhiệm cho chất lượng code

#### Ba Mức Độ Tích Hợp AI

1. **AI Assistant (2023)**: Gợi ý code từng dòng và auto-completion
2. **AI Assistant+ (2024)**: Giải quyết các task lớn hơn, cung cấp nhiều lựa chọn giải pháp
3. **AI Agents (2025)**: Tự lập kế hoạch, reasoning và sinh nhiều file

#### Các Thách Thức Khi Sử Dụng AI

1. **Hạn chế của single-shot**: Prompt chung chung cho kết quả chung chung
2. **Token overflow**: Giới hạn context khi làm việc với dự án lớn
3. **Tích hợp vào codebase có sẵn**: Khó implement feature vào project đang chạy
4. **Đảm bảo chất lượng**: Đảm bảo code AI sinh ra đạt chuẩn
5. **Ra quyết định**: Xác định AI nên xử lý gì vs con người phải làm gì
6. **Quản lý context**: Cung cấp thông tin phù hợp cho AI
7. **Phức tạp trong validation**: Review và approve output của AI

#### Quy Trình AIDOC

Thay vì yêu cầu AI hoàn thành toàn bộ feature một lần, AIDOC theo cách tiếp cận có cấu trúc:

1. **Hiểu rõ**: AI giúp phân tích user story và requirements
2. **Lập kế hoạch**: AI tạo implementation plan để developer review
3. **Thiết kế**: Tạo logical design và xác định các layer bị ảnh hưởng
4. **Triển khai**: AI implement plan đã được approve từng bước
5. **Kiểm thử**: Validate output ở mỗi giai đoạn
6. **Review**: Con người giám sát đảm bảo chất lượng và tính đúng đắn

#### Trình Diễn Amazon Q Developer

Toàn Huỳnh đã demo cách Amazon Q Developer tích hợp vào quy trình phát triển:

- **Intelligent code completion** với khả năng hiểu context
- **Sinh code đa file** cho các feature phức tạp
- **Hướng dẫn kiến trúc** để thiết kế solution
- **Quét bảo mật** và đề xuất best practices
- **Tương tác bằng ngôn ngữ tự nhiên** để giải quyết vấn đề

#### Trách Nhiệm Của Developer Trong Phát Triển Có AI

- **Validation**: Xác minh code và thiết kế do AI sinh ra
- **Ra quyết định**: Chọn giữa các option AI đề xuất
- **Giám sát**: Duy trì quyền kiểm soát quá trình phát triển
- **Đảm bảo chất lượng**: Đảm bảo code đạt chuẩn
- **Quyền tác giả**: Làm chủ toàn bộ code được deliver

### Bài Học Rút Ra

1. **AI sẽ không thay thế developer**, nhưng developer dùng AI hiệu quả sẽ vượt trội hơn những người không dùng
2. **Phương pháp luận quan trọng**: Có cách tiếp cận có cấu trúc (như AIDOC) là then chốt thành công
3. **Giám sát của con người là thiết yếu**: Developer phải validate, quyết định và giám sát mọi output của AI
4. **Tăng năng suất là thật**: Developer có thể tăng từ 50 lên 70+ user story mỗi tháng
5. **Cách tiếp cận đa bước tốt nhất**: Chia task phức tạp thành các bước quản lý được
6. **Context rất quan trọng**: Cung cấp thông tin phù hợp cho AI để có kết quả tốt hơn
7. **Chất lượng vẫn là trách nhiệm con người**: Developer là tác giả của code của họ

### Góc Nhìn Cá Nhân

Workshop này làm nổi bật cách AI đang chuyển đổi phát triển phần mềm từ góc độ công cụ sang một sự thay đổi phương pháp luận. Việc nhấn mạnh vào sự cộng tác người-AI thay vì thay thế đặc biệt quan trọng. Framework AIDOC cung cấp cách tiếp cận thực tế để tích hợp AI trong khi vẫn duy trì chất lượng và quyền kiểm soát của developer.

Các demo về Amazon Q Developer và Kiro cho thấy các công cụ AI đã trưởng thành đáng kể, từ code completion đơn giản đến sinh nhiều file phức tạp và hướng dẫn kiến trúc. Tuy nhiên, thông điệp chính vẫn là: developer phải hiểu, validate và làm chủ code của họ bất kể nó được sinh ra như thế nào.

### Các Sự Kiện AWS Sắp Tới

- **Gen AI Game Day** (Tháng tới): Cuộc thi thực hành sử dụng công cụ Gen AI
- **Cuộc thi tháng 12**: Trình bày sản phẩm Gen AI (10-15 phút presentation)

### Ứng Dụng Vào Công Việc

- **Áp dụng phương pháp AIDOC**: Cấu trúc tương tác AI theo quy trình đa bước
- **Sử dụng Amazon Q Developer**: Tích hợp vào công việc hàng ngày để tăng năng suất
- **Triển khai validation checkpoints**: Review output AI ở mỗi giai đoạn phát triển
- **Chia nhỏ task phức tạp**: Phân chia feature lớn thành các bước có thể quản lý với sự hỗ trợ của AI
- **Duy trì quyền sở hữu code**: Đảm bảo hiểu và chất lượng của mọi code AI sinh ra
- **Thử nghiệm AI agents**: Khám phá sinh code tự động cho các use case phù hợp

### Trải Nghiệm Sự Kiện

Tham dự workshop **"AI Software Development Lifecycle"** vô cùng giá trị, cung cấp cái nhìn toàn diện về thực hành phát triển hiện đại với AI. Các trải nghiệm chính bao gồm:

#### Học Hỏi Từ Chuyên Gia

- Các kỹ sư cấp cao AWS chia sẻ kinh nghiệm thực tế sử dụng AI trong dự án doanh nghiệp
- Demo thực tế cho thấy cả khả năng và hạn chế của công cụ AI hiện tại
- Hiểu được sự tiến hóa từ AI assistant đơn giản đến AI agent tự động

#### Kiến Thức Kỹ Thuật Thực Hành

- Chứng kiến demo trực tiếp Amazon Q Developer giải quyết thách thức coding phức tạp
- Học phương pháp AIDOC để cấu trúc phát triển có hỗ trợ AI
- Hiểu cách quản lý context và giới hạn token trong dự án lớn
- Khám phá kỹ thuật chia nhỏ user story để AI implement

#### Chuyển Đổi Tư Duy

- Nhận ra AI là cộng tác viên, không phải thay thế developer
- Hiểu tầm quan trọng của validation và ownership trong code AI sinh ra
- Học cách suy nghĩ theo hướng giải quyết vấn đề đa bước thay vì prompt đơn
- Nhận ra giá trị của phương pháp luận hơn là chỉ công cụ

#### Kết Nối Và Cộng Đồng

- Kết nối với 300+ developer quan tâm đến phát triển có AI
- Trao đổi ý tưởng về thách thức và giải pháp tích hợp AI
- Tìm hiểu về các sự kiện và cuộc thi AWS cộng đồng sắp tới

#### Công Cụ Và Kỹ Thuật Thực Tế

- Amazon Q Developer cho code completion và generation thông minh
- Công cụ Kiro để tăng năng suất
- Chiến lược prompting đa bước cho phản hồi AI tốt hơn
- Kỹ thuật quản lý context cho codebase lớn

#### Một số hình ảnh sự kiện

_Thêm hình ảnh sự kiện của bạn tại đây_

> Nhìn chung, sự kiện không chỉ cung cấp kiến thức kỹ thuật mà còn định hình lại cách hiểu của tôi về việc AI có thể nâng cao vòng đời phát triển phần mềm như thế nào. Việc nhấn mạnh vào giám sát và validation của con người đảm bảo rằng AI phục vụ như một công cụ mạnh mẽ để khuếch đại năng lực developer thay vì thay thế họ.

### Kết Luận

AI Software Development Lifecycle đại diện cho một sự thay đổi cơ bản trong cách chúng ta tiếp cận phát triển phần mềm. Bằng cách kết hợp khả năng của AI với chuyên môn con người thông qua các phương pháp luận có cấu trúc như AIDOC, developer có thể đạt được mức tăng năng suất đáng kể trong khi vẫn duy trì chất lượng và kiểm soát. Điều quan trọng là hiểu rằng AI là một cộng tác viên mạnh mẽ cần có sự hướng dẫn, validation và giám sát phù hợp để mang lại kết quả tối ưu.