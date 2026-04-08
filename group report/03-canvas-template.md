# AI Product Canvas — template

Điền Canvas cho product AI của nhóm. Mỗi ô có câu hỏi guide — trả lời trực tiếp, xóa phần in nghiêng khi điền.

---

## Canvas

|   | Value | Trust | Feasibility |
|---|-------|-------|-------------|
| **Câu hỏi guide** | User nào? Pain gì? AI giải quyết gì mà cách hiện tại không giải được? | Khi AI sai thì user bị ảnh hưởng thế nào? User biết AI sai bằng cách nào? User sửa bằng cách nào? | Cost bao nhiêu/request? Latency bao lâu? Risk chính là gì? |
| **Trả lời** | **User**: Người đi làm bận rộn.<br>**Pain**: Lười nhập liệu thủ công từng khoản chi.<br>**Giải pháp AI**: Tự động bóc tách, ghi chép và phân loại từ ngôn ngữ tự nhiên, giúp quản lý tài chính "nhàn hạ". | **Ảnh hưởng**: AI nội suy sai (Linear Extrapolation), đánh đồng khoản phát sinh thành định kỳ, làm dự báo tháng bị thổi phồng.<br>**Nhận biết**: Biểu đồ/dự báo cao vọt phi thực tế.<br>**Cách sửa**: Bổ sung Clarification Loop — AI chủ động đặt câu hỏi và cho nút gán nhãn [Phát sinh] / [Định kỳ] ở các khoản chi khác lạ. | **Cost**: Phí token API LLM theo mỗi request text input.<br>**Latency**: Vài trăm ms đến 2s.<br>**Risk**: Phân loại nhầm/bỏ sót khoản chi nếu list quá dài, ảo giác nội hàm chi tiêu. |

---

## Automation hay augmentation?

☐ Automation — AI làm thay, user không can thiệp
☑ Augmentation — AI gợi ý, user quyết định cuối cùng

**Justify:** Khi AI không chắc, tự ý quyết định dự báo (Automation) sẽ làm hỏng dữ liệu và gây mất niềm tin. Augmentation với "Clarification Loop" giúp xây dựng Trust; sự minh bạch và có nút thoát (Exit rating) quan trọng hơn sự thông minh tuyệt đối.

Gợi ý: nếu AI sai mà user không biết → automation nguy hiểm, cân nhắc augmentation.

---

## Learning signal

| # | Câu hỏi | Trả lời |
|---|---------|---------|
| 1 | User correction đi vào đâu? | Database cá nhân (lưu trữ trọng số tính chất Phát sinh/Định kỳ cho hạng mục cụ thể). |
| 2 | Product thu signal gì để biết tốt lên hay tệ đi? | Theo dõi tỉ lệ người dùng bấm nút đính chính [Một lần]/[Định kỳ] sau gợi ý. |
| 3 | Data thuộc loại nào? ☐ User-specific · ☐ Domain-specific · ☐ Real-time · ☐ Human-judgment · ☐ Khác: ___ | ☑ User-specific · ☐ Domain-specific · ☐ Real-time · ☑ Human-judgment · ☐ Khác: |

**Có marginal value không?** (Model đã biết cái này chưa? Ai khác cũng thu được data này không?)
Có. Dữ liệu này giúp mô hình thoát khỏi nội suy toán học máy móc (Linear Extrapolation) và học được "tâm lý, ngữ cảnh chi tiêu" của con người. Model public không có sắc thái cá nhân hóa này.

---

## Cách dùng

1. Điền Value trước — chưa rõ pain thì chưa điền Trust/Feasibility
2. Trust: trả lời 4 câu UX (đúng → sai → không chắc → user sửa)
3. Feasibility: ước lượng cost, không cần chính xác — order of magnitude đủ
4. Learning signal: nghĩ về vòng lặp dài hạn, không chỉ demo ngày mai
5. Đánh [?] cho chỗ chưa biết — Canvas là hypothesis, không phải đáp án

---

*AI Product Canvas — Ngày 5 — VinUni A20 — AI Thực Chiến · 2026*
