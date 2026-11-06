# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV:** 2A202603555
- **Họ và tên:** Nguyễn Bá Quảng
- **SEED** (in ở ô đầu notebook): 8744

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | x |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | x |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | x |

## 2. Kết quả chính

Hidden=4 | Params=1,545 | F1=0.0000 | Time=0.79s
Hidden=512 | Params=197,633 | F1=0.9463 | Time=5.92s

## 3. Dự đoán và thực tế

Dự đoán và kết quả. Em đoán MLP có thể kém Logistic Regression, nhưng F1 thực tế cao hơn (0,945 so với 0,838), chủ yếu nhờ recall tăng từ 72,1% lên 90,4%. Em đoán Logistic Regression đạt F1 khoảng 0,80, thực tế là 0,838 vì precision đạt 100%. Dự đoán thứ ba là few-shot tăng F1 1–3 điểm phần trăm, nhưng chưa đối chiếu được vì API báo lỗi 401.

## 4. Phân tích 50 case khó

Case #2 là tin báo có pizza miễn phí ở văn phòng. BoW có thể nhầm thành spam vì các từ free và now. Case #29 là tin lừa nhận thẻ quà tặng. Các từ w0n và Cl4im có thể né từ điển, khiến BoW bỏ sót.

## 5. Thử thách cá nhân

SEED 8744 cho em đề #3: thử MLP với 4 và 512 nơ-ron ở lớp ẩn. Em giữ nguyên dữ liệu và 30 epoch để so sánh ảnh hưởng của kích thước lớp ẩn. Mỗi nơ-ron ẩn nhận 2.000 đầu vào, có 1 bias và nối với đầu ra bằng 1 trọng số. Tính thêm 1 bias ở đầu ra, mạng 4 nơ-ron có 8.009 tham số, còn mạng 512 nơ-ron có 1.025.025 tham số.


## 6. Phương án cho sản phẩm thật

Em chọn BoW + MLP vì F1 đạt 0,945, p95 là 2,47 ms/tin và tốc độ theo lô là 11.353 tin/giây, so với nhu cầu trung bình khoảng 116 tin/giây. Em chấp nhận precision giảm nhẹ để bắt được nhiều spam hơn và sẽ đo lại p95 ở giờ cao điểm.

## 7. AI log và điều đã học

Trong quá trình làm bài, có nhiều đoạn code và thuật toán em chưa hiểu rõ. Em dùng AI để hỏi về chức năng của từng hàm, cách dữ liệu được xử lý qua các bước và lý do vì sao code được viết như vậy. Nhờ đó, em hiểu rõ hơn cách các phần trong bài liên kết với nhau và có thể tự giải thích lại một số đoạn code mà lúc đầu em còn thấy khó.
