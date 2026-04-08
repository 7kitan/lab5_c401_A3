Dưới đây là bản SPEC đầy đủ và chi tiết cho dự án **Xanh SM AI Booking Assistant**, được trình bày đúng theo form yêu cầu của bạn nhưng đi sâu vào từng mục nội dung để bạn có thể nộp bài ngay.

---

## Track: XanhSM

## Problem statement
Hiện tại Xanh SM đang sử dụng chatbot **rule-based** (dựa trên menu cứng và từ khóa). Khách hàng gặp khó khăn khi muốn đặt xe nhanh bằng ngôn ngữ tự nhiên (ví dụ: "Đặt cho mình một xe Xanh SM Taxi từ Vinhomes Ocean Park đi Nội Bài lúc 5h sáng mai"). Bot hiện tại không hiểu ngữ cảnh, bắt khách phải bấm nhiều bước, dẫn đến tỷ lệ bỏ cuộc cao và làm tăng áp lực lên tổng đài viên (3-5 phút chờ đợi).

**Giải pháp:** Chuyển sang **AI-based Chatbot** sử dụng LLM để tự động trích xuất thông tin (điểm đi, điểm đến, loại xe, thời gian) và đặt xe ngay trong một câu lệnh duy nhất.

---

## Canvas draft

| | Value | Trust | Feasibility |
| :--- | :--- | :--- | :--- |
| **Trả lời** | **User:** Đặt xe chỉ với 1 câu chat (giảm 80% thao tác). **Doanh nghiệp:** Giảm chi phí vận hành tổng đài, tăng tỷ lệ chuyển đổi đơn hàng. | Minh bạch giá cước và lộ trình ngay khi chat. Luôn có nút **"Kết nối tổng đài viên"** đề phòng AI gặp lỗi. | Sử dụng LLM (Gemini/GPT) + Google Maps API. Risk: Địa chỉ người dùng nhập không khớp với tọa độ bản đồ. |

* **Auto hay aug?** **Augmentation** — AI soạn sẵn đơn hàng (draft), người dùng kiểm tra và nhấn "Xác nhận" để đặt xe.
* **Learning signal:** Ghi nhận những lúc người dùng phải sửa lại địa chỉ hoặc loại xe mà AI đã trích xuất → Dữ liệu để tinh chỉnh Prompt (Fine-tuning/Few-shot).

---

## Chi tiết 6 mục SPEC deliverable

### 1. AI Product Canvas (Value / Trust / Feasibility + Learning Signal)
* **Value:** Giải quyết nỗi đau "phải chờ đợi" và "phải bấm quá nhiều menu". Giá trị cốt lõi là sự **tiện lợi tuyệt đối**.
* **Trust:** Xây dựng niềm tin bằng cách hiển thị rõ: "Dựa trên yêu cầu của bạn, tôi tìm thấy lộ trình [A đến B] với giá [X] VNĐ".
* **Feasibility:** Kỹ thuật trích xuất thực thể (Entity Extraction) hiện nay đã rất chín muồi trên các model LLM lớn.
* **Learning Signal:** Theo dõi "Success Booking Rate" (Tỷ lệ đặt xe thành công) so với "Chat-to-Booking Rate".

### 2. User Stories × 4 paths (Happy / Low-confidence / Failure / Correction)
* **Happy Path:** "Lấy cho mình 1 xe máy từ 191 Bà Triệu về Cầu Giấy" → AI xác định đúng vị trí và loại xe Xanh SM Bike → Báo giá 45k → User bấm "Đặt ngay".
* **Low-confidence:** "Đi đến quán Highlands Coffee gần đây" → Có quá nhiều quán Highlands → AI hỏi lại: "Bạn muốn đến quán ở phố A hay phố B?".
* **Failure:** "Cho tôi một chiếc máy bay đến Sài Gòn" → AI nhận diện yêu cầu ngoài khả năng → "Xin lỗi, Xanh SM hiện chỉ cung cấp xe điện. Bạn có muốn đặt xe ra sân bay Nội Bài không?".
* **Correction:** AI gợi ý xe 4 chỗ, khách nói "Nhà mình có 5 người" → AI lập tức đổi sang gợi ý xe Xanh SM Luxury (7 chỗ) và cập nhật giá.

### 3. Eval metrics: 3 metrics + threshold + red flag
* **Metric 1: Extraction Accuracy** (Độ chính xác trích xuất thông tin). **Threshold: ≥ 90%.**
* **Metric 2: Response Latency** (Thời gian phản hồi). **Threshold: < 2 giây.**
* **Metric 3: Booking Conversion Rate** (Tỷ lệ chuyển từ chat sang đặt xe thực tế).
* **Red flag:** Nếu tỷ lệ "Human Handoff" (phải chuyển sang người thật) vượt quá 20% tổng số cuộc hội thoại trong ngày.

### 4. Top 3 failure modes (Trigger / Hậu quả / Mitigation)
* **Mode 1: Ambiguous Location (Địa chỉ mơ hồ).** *Trigger:* Khách nói "Về nhà mình". *Hậu quả:* Không báo giá được. *Mitigation:* AI tự động check địa chỉ "Nhà riêng" đã lưu trong profile hoặc hỏi lại.
* **Mode 2: Hallucination (Ảo giác giá cước).** *Trigger:* AI tự bịa ra một mức giá không khớp hệ thống. *Hậu quả:* Mất uy tín, gây tranh cãi. *Mitigation:* AI không tự tính giá, chỉ gửi data qua API hệ thống Xanh SM để lấy giá chính xác.
* **Mode 3: OOD (Out-of-domain).** *Trigger:* Khách hỏi chuyện phiếm hoặc chính trị. *Hậu quả:* Bot trả lời linh tinh. *Mitigation:* Thiết lập System Prompt nghiêm ngặt để chỉ trả lời các vấn đề liên quan đến di chuyển.

### 5. ROI 3 kịch bản (conservative / realistic / optimistic)
* **Conservative:** Tiết kiệm 15% chi phí nhân sự tổng đài. Tỷ lệ đặt xe qua chat tăng 5%.
* **Realistic:** Tiết kiệm 40% chi phí vận hành; tự động hóa 60% các yêu cầu đặt xe phổ thông.
* **Optimistic:** Giảm 70% cuộc gọi tổng đài cho mục đích đặt xe; Chatbot trở thành kênh mang lại doanh thu lớn thứ 2 sau App chính thức.

### 6. Mini AI spec 1 trang
* **Tên:** Xanh SM Smart Assistant.
* **Công nghệ:** LLM + RAG (cho chính sách/khuyến mãi) + API Integration (cho định vị/giá cước).
* **Giao diện:** Tích hợp trực tiếp vào Zalo OA và Messenger của Xanh SM.
* **Cam kết:** Tốc độ, Chính xác, Luôn sẵn sàng 24/7.

---

## Hướng đi chính
* **Prototype:** Tạo chatbot thử nghiệm tập trung vào trích xuất 4 trường thông tin: [Origin], [Destination], [Vehicle_Type], [Pickup_Time].
* **Eval:** Kiểm thử với 100 câu lệnh thực tế từ người dùng để đo tỷ lệ hiểu đúng ý định (Intent).
* **Main failure mode:** Xử lý các địa chỉ không có trên bản đồ bằng cách cho phép người dùng "Thả ghim" trực tiếp trong khung chat.