# Individual reflection — Nguyễn Tuấn Kiệt (2A202600233)

## 1. Role
- Group Manager + UI/UX Tester

## 2. Đóng góp cụ thể
- Day 5 
  - Điều hướng nghĩ ý tưởng của cả nhóm
  - Thăm dò các nhóm khác để học phân tích và đánh giá các ý tưởng đang có
  - Phân công việc cho spec
- Day 6
  - Đưa ra user story + implementation plan gồm 3 feature chính: tìm địa điểm xung quanh, user chọn lộ trình, agent book chuyến đi
  - Phân công công việc dựa trên feature set, tách team ra nhiều hướng thử nghiệm cùng lúc (dùng Google AI Studio vs. Vercel v0 cho UI)
  - Sửa lỗi UI v2 (Tailwind, React) và code có vấn đề từ vibe coding
  - Đọc lại code do AI viết để document lại logic cho demo showcase
  - Sửa `System Prompt ` để tăng việc gọi tool chính xác hơn

## 3. SPEC mạnh/yếu
- **Mạnh nhất:**  Ứng dụng là bổ sung trực tiếp tính năng mới trên app mobile hiện có của Xanh SM, với mục tiêu pain point và user demographic rõ (khách du lịch, đi nhiếu chuyến trong cùng ngày - day trip). Dữ liệu hiện có thể tiếp cận được (v.d Google Maps API) có thể ứng dụng để làm nền cho recommendation ban đầu
- **Yếu nhất:** Chưa có Failure Mode library rõ ràng (v.d yêu cầu không rõ, agent cần hỏi lại) và chưa rõ về UX cho các tình huống có thể gặp (user muốn số lượng điểm khác, muốn edit lộ trình). System prompt cần phát triển thêm để xử lý các vấn đề như thế.


## 4. Đóng góp khác
- Loại ra các ý tưởng trước trong day 5 (VinMec - AI phỏng vấn bệnh nhân lấy report cho buổi hẹn khám đầu) về tính khả thi cho prototype 1 ngày
- Đưa ra ý tưởng ban đầu cho UI/User Story trên giấy cho team thống nhất ý tưởng trước khi bắt đầu code day 6

## 5. Điều học được
- Các loại quy trình thì không cần agent, đa số case dùng rule-based là ok
- Chatbot/agent tốt nhất là apply ở các loại interaction mở, khi failure không có tác hại lớn
- Cần failure mode library rộng hơn so với software thông thường
- Code do AI viết rất khó debug, đặc biệt là frontend (hôm nay đã học thêm cách tìm source code lỗi nhanh)
- System prompt quan trọng, hoàn toàn quyết định có gọi tool hay không, không thể chắc chắn về behavior
- Đa số vấn đề với việc áp dụng AI là các tool cho user không có interface cho AI (call Google Maps, GMail etc)
- 

## 6. Nếu làm lại
- Không dùng v0 làm UI, và nếu vẫn dùng phải specify không dùng React + Tailwind + TypeScript (combo phổ biến, rất khó debug). Dùng stack đơn giản hơn, lọc bớt UI (mapview) nếu tốn vào thời gian shape user flow/failure
- Bắt đầu với tool interface trước, define từ đầu các hoạt động agent được phép làm, xong mới viết system prompt hướng theo đó
- Tìm hiểu trước Agent có thể làm thay đổi trên UI như thế nào user thấy được (v.d tự động tạo lộ trình, hiện luôn cho user)
-

## 7. AI giúp gì / AI sai gì
- **Giúp:** AI Studio/v0 cho ý tưởng frontend, Gemini/ChatGPT cho brainstorm ý tưởng trong Day 5
- **Sai/mislead:** UI của v0 cho ra có vấn đề phải sửa thủ công (Tailwind), mất thời gian đọc để hiểu flow project. Brainstorm ra rất nhiều ý tưởng với nhiều assumption sai, chung chung, không có value khi phân tích kĩ hơn.
