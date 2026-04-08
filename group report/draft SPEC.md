# Bản SPEC Tóm Tắt: Xanh SM AI Concierge Agent

Đổi mới từ một Chatbot rule based bị động sang một **AI Travel Agent** chủ động (Proactive Agent), chuyển đổi công cụ này thành một "người bạn đồng hành" thay vì chỉ là một ứng dụng đặt xe.

---

## 1. Problem Statement & Solution

**Vấn đề:**
- **Về công nghệ:** Chatbot hiện tại là **rule-based** (dựa trên menu cứng). Khách nhập câu lệnh tự nhiên (VD: "Đặt xe 5h sáng mai đi Nội Bài") sẽ không được hiểu ngay, dẫn đến luồng thao tác kéo dài và tỷ lệ rớt (drop-off rate) cao.
- **Về trải nghiệm & Kinh doanh:** Khách hàng thụ động, chỉ gọi xe khi cần. Trong khi đó, khách thiếu thông tin để tối ưu chuyến đi (thời tiết, kẹt xe, địa điểm vui chơi). Xanh SM đang bỏ lỡ cơ hội **Upsell** (bán thêm dịch vụ) và **Cross-sell** (bán chéo Xanh Tour, Xanh Luxury) ngay tại thời điểm khách hàng phát sinh nhu cầu.

**Giải pháp:** Nâng cấp lên **AI Concierge Agent** có khả năng:
1. **Chủ động (Proactive):** Gợi ý giờ đi tránh tắc đường hoặc mưa bão.
2. **Cá nhân hóa (Personalization):** Thiết kế lịch trình dựa trên sở thích người dùng.
3. **Định hướng Sale (Sales-driven):** Lồng ghép khéo léo việc sử dụng dịch vụ Xanh SM vào các hoạt động du lịch/khám phá.

---

## 2. AI Product Canvas

| Yếu tố | Nội dung |
| :--- | :--- |
| **Value (Giá trị)** | **User:** Đi đúng lúc, đến đúng chỗ, giá tốt nhất.<br>**Xanh SM:** Tăng doanh thu mỗi khách hàng (AOV) và sự trung thành bằng cách biến Xanh SM thành một "Lifestyle App" khiến khách hàng cảm thấy được chăm sóc. |
| **Trust (Niềm tin)** | Gợi ý dựa trên dữ liệu thực (Real-time weather/traffic). Tính minh bạch cao: Agent báo đường đông thay vì cố tình đặt xe để khách chờ lâu. Đồng thời kết hợp **tính minh bạch giá cước qua API** và giải pháp **"Kết nối tổng đài viên (Human Handoff)"** khi AI bối rối. |
| **Feasibility (Tính khả thi)** | Sử dụng kỹ thuật **Tool Use / Function Calling** để AI tự tra cứu API Thời tiết, Google Maps Traffic và Database địa điểm trước khi phản hồi. |

* **Mô hình tương tác:** **Augmentation** (AI gợi ý lịch trình, khách chốt) kết hợp **Agentic Action** (AI tự động thực hiện hành động đặt xe khi khách đồng ý).
* **Learning Signal:** Khách có đi theo giờ AI gợi ý không? Khách có chọn địa điểm AI đề xuất không? $\rightarrow$ Thu thập dữ liệu để học hỏi gu thẩm mỹ và thói quen sinh hoạt của khách.

---

## 3. User Stories (4 Cấp Độ)

| Path | Kịch bản ví dụ |
| :--- | :--- |
| **Happy Path**<br>*(The Concierge)* | **Khách:** "Mai mình muốn đi chơi quanh Hà Nội".<br>**AI:** "Dự báo mai nắng đẹp, bạn nên đi Xanh SM Luxury đến Phủ Thành Chương lúc 8h sáng để tránh tắc đường. Mình đặt xe luôn nhé?". |
| **Low-confidence** | **Khách:** *(Muốn đi một nơi quá xa/hẻo lánh)*<br>**AI:** "Khu vực này hiện có ít xe Xanh, bạn nên đặt trước hoặc cân nhắc đi Xanh Tour trọn gói để đảm bảo có chuyến về". |
| **Failure**<br>*(Weather Alert)* | **Khách:** *(Đặt xe đi biển khi sắp có bão)*<br>**AI:** "Mình thấy sắp có mưa lớn tại điểm đến, bạn có muốn lùi lịch sang chiều mai không? Xanh SM hỗ trợ bạn đổi lịch miễn phí". |
| **Correction** | **Khách:** "Chỗ đó ồn ào quá".<br>**AI:** *(Xin lỗi, điều chỉnh theo "vibe" và gợi ý sang các quán cafe yên tĩnh hoặc bảo tàng).* |

---

## 4. Evaluation Metrics

| Metric | Mô tả | Ngưỡng (Threshold) |
| :--- | :--- | :--- |
| **Intent & Entity Extraction Accuracy**| Độ chính xác khi AI bóc tách: Điểm đi/nơi đến, loại xe, giờ đi. | **$\ge$ 90%** |
| **Upsell Conversion Rate** | Tỷ lệ khách chọn Xanh Luxury/Xanh Tour sau khi AI gợi ý. | **$\ge$ 15%** |
| **Proactive Acceptance Rate** | Tỷ lệ khách đồng ý với giờ khởi hành và lịch trình mà AI đề xuất. | Theo dõi |

> 🚨 **Red Flags:**
> 1. Tỷ lệ **Human Handoff** (Chuyển qua tổng đài viên) > **20%** $\rightarrow$ Dấu hiệu AI đang không hiểu ngữ cảnh hoặc bóc tách sai địa chỉ liên tục.
> 2. Tỷ lệ khách nhấn nút **"Tắt gợi ý/Làm phiền"** > **10%** $\rightarrow$ Dấu hiệu AI đang quá tập trung "sale" mà thiếu sự tinh tế trong dịch vụ.

---

## 5. Top 4 Failure Modes

1. **Hallucination Giá cước & Lộ trình (Ảo giác AI):**
   * *Trigger:* AI tự bịa ra một mức giá hoặc lộ trình không có thật trên bản đồ.
   * *Hậu quả:* Gây tranh cãi, khiếu nại, mất uy tín nghiêm trọng.
   * *Mitigation:* Khóa cứng (Guardrails) – AI KHÔNG ĐƯỢC tự tính giá; mọi báo giá và xác thực lộ trình PHẢI lấy trực tiếp từ API backend của Xanh SM.
2. **Ambiguous Location (Địa chỉ mơ hồ):**
   * *Trigger:* Khách yêu cầu "đến quán cafe nào chill chill gần đây" nhưng không chốt được tọa độ chính xác.
   * *Hậu quả:* Đặt xe hoặc báo giá thất bại.
   * *Mitigation:* AI tự động hướng dẫn khách dùng tính năng "Thả ghim" bản đồ trong khung chat hoặc truy vấn từ lịch sử điểm đến.
3. **Over-pushy Sales (Quá hăng hái bán hàng):**
   * *Trigger:* AI gợi ý liên tục các dịch vụ tốn kém (Xanh Luxury/Tour) mà bỏ qua nhu cầu thực tế của khách.
   * *Hậu quả:* User cảm thấy bị làm phiền, tắt app.
   * *Mitigation:* Giới hạn số lượng gợi ý (tối đa 1-2 lần/chuyến) và ưu tiên mức độ match với Context của người dùng.
4. **Traffic/Weather Lag:**
   * *Trigger:* Dữ liệu về thời tiết/giao thông cập nhật từ API chậm so với thực tế bên ngoài.
   * *Mitigation:* Luôn đệm câu "Theo dữ liệu cập nhật cách đây 5 phút..." để quản lý tốt kỳ vọng của khách hàng.

---

## 6. ROI Estimation (3 Kịch bản)

* **Conservative (Thận trọng):** Tăng **10%** doanh thu nhờ khách đi các chuyến dài hơn (gợi ý đi chơi xa).
* **Realistic (Thực tế):** Tăng **25%** doanh thu; Xanh Tour và Xanh Luxury trở thành các dịch vụ phổ biến nhờ AI định hướng đúng tệp khách.
* **Optimistic (Lạc quan):** Xanh SM trở thành "Super App" về du lịch điện tử; giảm **50%** chi phí marketing truyền thống do AI làm tốt khâu cá nhân hóa ưu đãi.

---

## 7. Mini AI Spec (Tóm lược 1 trang)

* **Tên Agent:** Xanh SM AI Concierge
* **Core Logic:** LLM đóng vai trò "Bộ não" điều phối các Tools (*Weather, Traffic, Booking, Places*).
* **Chiến thuật Sale (Contextual Commerce):** 
  > Lồng ghép theo công thức: **Insight** (Đường đông/Mưa) $+$ **Giải pháp** (Đi giờ X) $+$ **Gợi ý kèm theo** (Đến chỗ Y bằng loại xe Z của Xanh SM).
* **Giao diện:** Trợ lý ảo có tính cách thân thiện, am hiểu văn hóa địa phương.

### 🚀 Hướng đi tiếp theo:
* **Prototype:** Thiết kế một `System Message` đóng vai trò là một hướng dẫn viên du lịch chuyên nghiệp của Xanh SM.
* **Eval:** Thử nghiệm kịch bản "Tư vấn lịch trình cuối tuần" cho một nhóm khách mẫu để đo lường độ hài lòng.
* **Focus Topic:** Tập trung giải quyết bài toán cốt lõi "Cân bằng giữa tư vấn khách quan và mục tiêu bán hàng" (Sales vs. Service) thông qua **Contextual Commerce** – chỉ bán dịch vụ khi nó thực sự có ích cho chuyến đi của khách.
