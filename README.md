[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574893&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student ID:** 2A202600177
**Name:** Nguyễn Mạnh Dũng
**Student Email:** dungduhau@gmail.com

---

## Mô tả

Bài lab xây dựng một pipeline ETL đơn giản để xử lý dữ liệu sản phẩm:
- **Extract:** đọc dữ liệu từ `raw_data.json`
- **Validate:** loại bản ghi không hợp lệ (`price <= 0` hoặc `category` rỗng)
- **Transform:** chuẩn hóa `category` về Title Case, tính `discounted_price` giảm 10%, thêm `processed_at`
- **Load:** ghi dữ liệu đã xử lý ra `processed_data.csv`

Ngoài ra, bài lab có phần **stress test AI Agent** để so sánh chất lượng câu trả lời khi dùng dữ liệu sạch và dữ liệu bẩn.

---

## Cách chạy (How to Run)

### Prerequisites
```bash
python3 -m venv venv
source venv/bin/activate
pip install pandas pytest
```

### Chạy ETL Pipeline
```bash
python solution.py
```

### Chạy Agent Simulation (Stress Test)
```bash
python agent_simulation.py
```

---

## Cấu trúc thư mục

```
├── solution.py              # Script ETL chính
├── agent_simulation.py      # Mô phỏng truy vấn AI Agent
├── raw_data.json            # Dữ liệu nguồn ban đầu
├── processed_data.csv       # Dữ liệu sau ETL
├── garbage_data.csv         # Dữ liệu bẩn để stress test
├── experiment_report.md     # Báo cáo thí nghiệm Clean vs Garbage
├── tests/test_autograder.py # Test tự động
└── README.md                # Tài liệu bài làm
```

---

## Kết quả

### 1) Kết quả ETL
- Tổng số bản ghi đầu vào: **5**
- Bản ghi hợp lệ được giữ lại: **3**
- Bản ghi bị loại: **2**
  - `id=3`: `Price <= 0`
  - `id=4`: `Missing Category`
- File output: `processed_data.csv` gồm các cột:
  - `id`, `product`, `price`, `category`, `discounted_price`, `processed_at`

### 2) Kết quả Agent Simulation
- Với **Clean Data (`processed_data.csv`)**:
  - `Agent: Based on my data, the best choice is Laptop at $1200.`
- Với **Garbage Data (`garbage_data.csv`)**:
  - `Agent: Based on my data, the best choice is Nuclear Reactor at $999999.`

Nhận xét: dữ liệu bẩn chứa outlier, duplicate, sai kiểu dữ liệu và giá trị thiếu làm Agent trả lời sai lệch nghiêm trọng.
