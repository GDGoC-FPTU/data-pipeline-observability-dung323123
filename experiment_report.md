# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600177
**Name:** Nguyễn Mạnh Dũng
**Date:** 2026-04-15

---

## 1. Kết quả thí nghiệm

Chạy `agent_simulation.py` với 2 bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 9/10 | Kết quả hợp lý với tập Electronics đã được làm sạch và validate. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 1/10 | Outlier giá quá lớn làm Agent ưu tiên sai sản phẩm, kết quả không thực tế. |

---

## 2. Phân tích & nhận xét

### Tại sao Agent trả lời sai khi dùng Garbage Data?

Agent trong `agent_simulation.py` chọn sản phẩm electronics có `price` cao nhất, nên rất nhạy cảm với dữ liệu bẩn. Trong `garbage_data.csv`, bản ghi "Nuclear Reactor" có giá 999999 là outlier bất thường, vượt xa mặt bằng giá thật, nên agent bị "kéo" về lựa chọn này. Ngoài ra bộ dữ liệu rác còn có duplicate ID (`id=1` lặp lại), sai kiểu dữ liệu (`ten dollars`), và giá trị thiếu (`id` rỗng, `category` rỗng, `price=0`). Các lỗi này làm giảm độ tin cậy của nguồn tri thức, khiến quy tắc truy vấn đơn giản của agent dễ sinh ra câu trả lời sai.

---

## 3. Kết luận

**Quality Data > Quality Prompt?** (Đồng ý hay không? Giải thích ngắn gọn.)

Đồng ý. Prompt không thể "cứu" dữ liệu xấu nếu data gốc đã nhiễm nhiều outlier, null, và wrong type. Trong thí nghiệm này, cùng một câu hỏi và cùng một logic agent, clean data cho kết quả hợp lý, còn garbage data cho kết quả lệch hoàn toàn. Vì vậy, data quality là nền tảng quan trọng hơn để đảm bảo output AI ổn định và đáng tin.
