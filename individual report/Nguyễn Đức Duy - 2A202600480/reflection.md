# Individual reflection — Nguyễn Đức Duy (2A202600480)

## 1. Role
Lên plan kiến trúc backend, viết tool và cùng xây system prompt

## 2. Đóng góp cụ thể
- Lên plan và thiết kế kiến trúc backend cho AI Agent "Xanh SM Holiday Mode", xác định luồng giao tiếp giữa LLM và các external APIs.
- Viết và test các tools (Function Calling) hỗ trợ Agent: mô phỏng lấy dữ liệu địa điểm (search_nearby_attractions).
- Cùng nhóm xây dựng và tinh chỉnh system prompt để AI làm tốt vai trò "Travel Companion" (chủ động đề xuất lịch trình và lồng ghép dịch vụ đặt xe Xanh SM một cách tự nhiên).
- Phụ trách phân tích và viết phần "Top 4 Failure Modes" (Các rủi ro sinh ra từ AI và phương án giảm thiểu) trong bản SPEC.

## 3. SPEC mạnh/yếu
- **Mạnh nhất:** Tính khả thi và tính thực tế cao nhờ concept "Mobility-first" (tích hợp đặt xe Xanh SM trực tiếp vào itinerary), giải quyết bài toán tăng doanh thu đa cuốc (multi-trip) rất rõ ràng. Các User Stories định nghĩa đầy đủ các happy path tới edge case.
- **Yếu nhất:** Phần định nghĩa luồng tích hợp Tools (Core logic) trong SPEC còn hơi chung chung. Để kịch bản "Context change" (VD: đổi lịch trình vì mưa) trơn tru, cần định nghĩa rõ ràng lúc nào AI được phép tự động gọi Weather API thay vì đợi người dùng cung cấp.

## 4. Đóng góp khác
- Mock up các dữ liệu JSON mẫu để test các cases (VD: dữ liệu POI của Đà Nẵng, mock data thời tiết) phục vụ việc chạy thử Agent local.
- Hỗ trợ các bạn trong nhóm test thử nghiệm các kịch bản Edge case (người dùng nói chung chung, thời tiết cực đoan) để kiểm chứng hệ thống có gọi đúng các tool fallback hay không.

## 5. Điều học được
Trước hackathon, tôi nghĩ AI tốt phụ thuộc chủ yếu vào prompt. Nhưng sau khi thiết kế kiến trúc và viết tool, tôi nhận ra với hệ thống Agentic, yếu tố quyết định là chất lượng của Tool Description (để AI hiểu khi nào nên gọi hàm). Xây dựng Agent thực chất là kỹ thuật điều phối logic phần mềm với sự rẽ nhánh vô định của LLM.

## 6. Nếu làm lại
Sẽ làm rõ hơn kiến trúc fallback của backend khi LLM gọi tool thất bại hoặc API timeout sớm hơn. Trong thời gian hạn hẹp, nhóm đã tập trung nhiều vào các luồng gọi tool thành công (happy path), nhưng khi demo nếu gặp lỗi mạng, cơ chế tự động chuyển sang chế độ manual cho người dùng chưa thực sự được code hoàn thiện.

## 7. AI giúp gì / AI sai gì
- **Giúp:** AI giúp code nhanh một form tổng thể, tối ưu rất tốt thời gian viết JSON Schema cho các definition của Function Calling và tạo nhanh các mã giả (mock data / boilerplate code) cho API trả về cấu trúc chính xác.
- **Sai/mislead:** Khi nhờ AI gợi ý kiến trúc backend ban đầu cho ứng dụng, AI đã đề xuất một hệ thống phức tạp. Nếu nhóm không kiểm tra lại thì đã bị "over-engineeering". Nhóm đã quay về thiết kế kiến trúc đủ gọn nhẹ và phù hợp với một dự án hackathon trong ngày. Trải nghiệm này cho thấy cần phải có mindset "giữ đúng scope" rất chặt khi tham khảo architecture từ LLM.