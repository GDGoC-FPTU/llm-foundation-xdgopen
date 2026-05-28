# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Ở temperature 0.0, mô hình luôn trả về cùng một sự thật mỗi lần gọi (hành vi xác định). Từ 0.0 đến 1.0, phản hồi trở nên đa dạng hơn nhưng vẫn mạch lạc. Ở temperature 1.5, phản hồi trở nên ngẫu nhiên, rất sáng tạo nhưng đôi khi không liên quan đến chủ đề hoặc kém chất lượng hơn.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Đặt temperature 0.1-0.3. Chatbot hỗ trợ khách hàng cần nhất quán, chính xác và đáng tin cậy. Một temperature thấp đảm bảo mô hình luôn cung cấp thông tin chính xác, tránh những câu trả lời không liên quan hoặc sai lạc, điều quan trọng để duy trì niềm tin của khách hàng.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Dựa trên pricing: GPT-4o ($5.00 input, $20.00 output), GPT-4o-mini ($0.150 input, $0.600 output). Tỷ giá chi phí là 33x (5.00/0.150 = 20.00/0.600 ≈ 33x). Với 10,000 users × 3 calls × 350 tokens/day ≈ 10.5M tokens, GPT-4o chi phí khoảng $87.50/ngày, GPT-4o-mini chi phí khoảng $2.63/ngày, hay khoảng 33x đắt hơn.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> **GPT-4o xứng đáng**: Sử dụng cho các tác vụ phức tạp như phân tích tài liệu pháp lý, dịch tài liệu nhạy cảm, hoặc tạo nội dung chuyên sâu đòi hỏi độ chính xác cao. Chi phí tăng được bù đắp bằng chất lượng tốt hơn, giảm lỗi, và tiết kiệm công sửa chữa. **GPT-4o-mini tốt hơn**: Dùng cho các tác vụ đơn giản như phân loại email, trích xuất thông tin cơ bản, hay chatbot FAQs nhỏ. Ở đây mini vẫn đủ chính xác nhưng chi phí thấp gấp 33 lần, rất thích hợp cho workload lớn với yêu cầu chất lượng thường.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất trong các ứng dụng real-time tương tác như chatbot web, trợ lý AI đối thoại, hay công cụ viết lời khuyên nhanh. Người dùng thấy phản hồi từng chữ một thay vì phải chờ toàn bộ response, cải thiện đáng kể trải nghiệm. Ngược lại, non-streaming phù hợp hơn khi xử lý batch lớn (ví dụ phân loại 1 triệu email), khi latency không quan trọng, hoặc khi cần xử lý toàn bộ response trước khi tiếp tục (như parsing JSON). Non-streaming cũng đơn giản hơn từ góc độ lập trình và phù hợp cho backoffice/task không yêu cầu user feedback tức thì.


## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
