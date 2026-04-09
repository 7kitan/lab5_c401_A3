# Individual reflection — Nguyễn Duy Hưng (2A202600154)

## 1. Role
Product + AI design, phụ trách viết SPEC.

## 2. Đóng góp cụ thể
- Xây dựng AI Product Canvas (Value / Trust / Feasibility)
- Hiển thị các địa điểm trong itinerary dưới dạng marker trên bản đồ

## 3. SPEC mạnh/yếu
- Mạnh nhất: ý tưởng rõ ràng và có tính thực tế — giải quyết pain thật (không biết đi đâu khi du lịch) và gắn trực tiếp với business (tăng số chuyến đi)
- Yếu nhất: phần evaluation và ROI còn mang tính giả định, chưa có dữ liệu thực để validate các con số

## 4. Đóng góp khác
- Brainstorm cùng nhóm để refine idea (từ chatbot → AI agent)
- Góp ý chỉnh sửa user stories để rõ hơn các tình huống thực tế
- Đề xuất sử dụng MapView API để trực quan hóa itinerary, giảm cognitive load cho người dùng
- Review tổng thể SPEC để đảm bảo các phần logic nhất quán

## 5. Điều học được
Trước hackathon nghĩ AI chỉ cần trả lời đúng là đủ.
Sau khi làm SPEC mới hiểu: một AI product tốt cần kết hợp giữa reasoning (LLM) và visualization (UI).
Ví dụ: itinerary dạng text khó hình dung, nhưng khi kết hợp MapView API để hiển thị vị trí và tuyến đường thì trải nghiệm rõ ràng và dễ hiểu hơn nhiều.

## 6. Nếu làm lại
Sẽ dành nhiều thời gian hơn cho việc define rõ user persona và use case ngay từ đầu.
Ngoài ra, sẽ thiết kế phần map + UI song song với phần AI thay vì làm sau, để đảm bảo trải nghiệm end-to-end tốt hơn.

## 7. AI giúp gì / AI sai gì
- **Giúp:** dùng AI để brainstorm idea, đặc biệt là cách kết hợp AI với map để tạo trải nghiệm trực quan hơn
- **Sai/mislead:** AI thường gợi ý thêm nhiều feature hấp dẫn nhưng vượt quá scope hackathon (ví dụ: full booking system hoặc social features). 
  Bài học: cần giữ scope gọn và tập trung vào core value