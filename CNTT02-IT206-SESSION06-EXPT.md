# [Phân tích] So sánh Trade-off các giải pháp ra lệnh cho Ứng dụng AI trong Học tập & Nghiên cứu
## Bước 1: Đề xuất 2 prompt mẫu
### Giải pháp 1: Prompt đơn giản, ngắn gọn (Zero/Few-shot tối giản)
Đóng vai gia sư Feynman. Hãy chấm bài giải thích của học sinh về chủ đề "{chu_de}" dựa trên Rubric "{rubric_danh_gia}".
Bài làm: "{bai_lam_cua_hoc_sinh}"

Trả về: điểm từng tiêu chí, nhận xét ngắn, lỗ hổng kiến thức nếu có và 1 câu hỏi gợi mở.
### Giải pháp 2: Prompt chi tiết, nhiều ràng buộc (Guardrails + Schema rõ ràng)
Bạn là gia sư AI áp dụng phương pháp Feynman và chấm điểm chuẩn theo Rubric.

## Đầu vào:
- Chủ đề: {chu_de}
- Rubric: {rubric_danh_gia}
- Bài làm: {bai_lam_cua_hoc_sinh}

## Ràng buộc & Xử lý lỗi biên:
1. Nếu bài làm trống hoặc dưới 10 từ: KHÔNG chấm điểm, chỉ yêu cầu học sinh viết lại đầy đủ hơn.
2. Nếu bài làm lạc chủ đề hoặc chép y nguyên định nghĩa sách giáo khoa (học vẹt): trừ điểm phần Feynman và chỉ rõ cụm từ rập khuôn.
3. Không tự ý thêm tiêu chí ngoài Rubric; mọi nhận xét phải bám sát nội dung học sinh đã viết.

## Định dạng đầu ra bắt buộc:
- **Bảng Rubric:** Tiêu chí | Điểm | Lý do
- **Chẩn đoán Feynman:** Hiểu đúng | Lỗ hổng / Học vẹt
- **Bước tiếp theo:** 1 câu hỏi gợi mở giúp học sinh tự sửa.
### Bước 2: Bảng so sánh Trade-off

| Tiêu chí | Giải pháp 1 (Đơn giản) | Giải pháp 2 (Chi tiết) |
| :--- | :--- | :--- |
| **Độ dễ hiểu** | Cao — Dễ đọc, dễ sửa nhanh cho người mới. | Trung bình — Dài hơn, cần đọc kỹ luật và cấu trúc. |
| **Tốn token** | Ít — Tiết kiệm chi phí và phản hồi nhanh. | Nhiều hơn — Tốn token cho hướng dẫn và kiểm soát ngoại lệ. |
| **Chặn lỗi biên** | Trung bình — Dễ bị lọt bài trống, lạc đề hoặc chấm thiếu ổn định. | Cực tốt — Xử lý rõ bài ngắn/trống, lạc đề và lỗi học vẹt. |
| **Độ đồng nhất đầu ra** | Thấp – Trung bình — Dễ thay đổi cách trình bày giữa các lần chạy. | Cao — Cấu trúc bảng và mục phân tích ổn định hơn. |
### Bước 3: Lựa chọn và chạy thử
Phương án tối ưu: Giải pháp 2 (Chi tiết)
Lý do chọn: Trong bài toán chấm bài tự động và gia sư Feynman, tính nhất quán và khả năng chặn lỗi biên (bài trống, bài viết 2–3 chữ, lạc chủ đề) quan trọng hơn việc tiết kiệm thêm vài chục token. Giải pháp 2 giảm thiểu tình trạng AI chấm bừa khi thiếu dữ liệu.