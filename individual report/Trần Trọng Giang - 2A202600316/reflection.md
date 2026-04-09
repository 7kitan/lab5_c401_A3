Individual reflection — Trần Trọng Giang (2A202600316)

1. Role
Phát triển Agent Tools (đặc biệt là Tool kiểm tra thời tiết), tinh chỉnh System Prompt, và chịu trách nhiệm phân tích Business/Tech (viết ROI Estimation & Mini AI Spec).

2. Đóng góp cụ thể

    Phát triển Tool: Viết và tích hợp công cụ kiểm tra thời tiết khu vực (Weather API) vào hệ thống Agent. Điều này giúp AI có khả năng nhận biết điều kiện môi trường thực tế để đưa ra quyết định thay đổi lộ trình linh hoạt (ví dụ: gạch bỏ điểm đến ngoài trời nếu trời mưa).

    Tối ưu System Prompt: Phối hợp cùng team xây dựng và cải thiện System Prompt, đảm bảo AI Agent giữ đúng vai trò "Travel Companion", giao tiếp tự nhiên và khéo léo lồng ghép dịch vụ đặt xe của Xanh SM mà không bị gượng ép.

    Viết SPEC: Chịu trách nhiệm soạn thảo phần ROI Estimation (ước tính tỷ suất hoàn vốn) và Mini AI Spec. Đóng góp này giúp làm rõ bài toán kinh doanh (tăng số lượng cuốc xe/user thông qua multi-trip) và định hình kiến trúc AI cốt lõi cho dự án.

3. SPEC mạnh/yếu

    Mạnh nhất: Phần ROI Estimation và Mini AI Spec đã gắn kết rất chặt chẽ giữa công nghệ và bài toán kinh doanh. Việc định lượng được giá trị kinh doanh giúp chứng minh tính thực tế của "Holiday Mode" thay vì chỉ là một tính năng AI "cho vui". Hơn nữa, việc tính đến biến số thời tiết trong lộ trình giúp User Stories sát với thực tế đi du lịch.

    Yếu nhất: Trong Mini AI Spec, luồng xử lý chi tiết (Error handling & Fallback) khi các External API (như Weather API) bị timeout hoặc trả về dữ liệu rỗng chưa được đặc tả đủ sâu. Nếu tích hợp thực tế, cần làm rõ hơn mức độ chủ động của AI khi thiếu hụt dữ liệu môi trường.

4. Đóng góp khác

    Phối hợp cùng Duy và Kiệt test chéo các kịch bản người dùng (User Path) để đảm bảo System Prompt hoạt động ổn định và AI gọi đúng Tool kiểm tra thời tiết khi có dấu hiệu thay đổi ngữ cảnh (Context change).

    Đóng góp ý tưởng cho phần luồng hội thoại linh hoạt, giúp xử lý các câu prompt phức tạp của người dùng.

5. Điều học được

    Về mặt kỹ thuật: Tôi nhận ra rằng việc viết mô tả (description) cho Agent Tool quan trọng không kém gì System Prompt. LLM chỉ gọi tool chính xác (như tool thời tiết) khi định nghĩa JSON Schema và mô tả input/output thực sự rõ ràng.

    Về mặt tư duy sản phẩm: Xây dựng AI không chỉ là ghép nối API. Phần viết ROI Estimation giúp tôi học được cách nhìn một hệ thống Agent dưới góc độ "nó mang lại bao nhiêu doanh thu cho doanh nghiệp" để từ đó thiết kế tính năng cho phù hợp.

6. Nếu làm lại

    Tôi sẽ đầu tư thêm thời gian để thiết kế kịch bản xử lý lỗi cho Tool thời tiết kỹ hơn. Ví dụ: Nếu API lỗi, Agent nên được prompt để chủ động hỏi user về thời tiết hiện tại thay vì bỏ qua bước này.

    Trong phần ROI Estimation, tôi sẽ đưa ra thêm 2-3 kịch bản (Pessimistic, Base, Optimistic) dựa trên tỷ lệ chuyển đổi (conversion rate) của việc book xe thành công để bản Spec thuyết phục hơn nữa.

7. AI giúp gì / AI sai gì

    Giúp: AI (Gemini) hỗ trợ cực kỳ tốt trong việc sinh ra các cấu trúc JSON Schema chuẩn xác cho Function Calling, đồng thời giúp tôi lên draft nhanh các công thức và cấu trúc tính toán cho phần ROI Estimation.

    Sai/mislead: Khi nhờ AI gợi ý cấu trúc cho Mini AI Spec, ban đầu nó đưa ra một kiến trúc rất cồng kềnh với nhiều lớp đánh giá (Evaluation layers). Nếu không tỉnh táo cắt gọt, tài liệu Spec sẽ bị lan man và không phù hợp với quy mô của một dự án Hackathon (Day 6). Đôi lúc khi test, nếu prompt không đủ "cứng", AI vẫn bị ảo giác (hallucinate) tự bịa ra thông tin thời tiết thay vì gọi Tool.
