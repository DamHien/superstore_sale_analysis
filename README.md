# supersotre_sale_analysis
Data analysis of US Superstore sales — customer behavior, regional performance &amp; profitability insights

## Giới thiệu dự án
dự án phân tích dữ liệu bán hàng của Superstore (Mỹ), tập trung trả lời các câu hỏi kinh doanh:
- Vùng/bang nào đóng góp doanh thu cao nhất, vùng nào đang lỗ dù bán được nhiều?
- Khách hàng nào là VIP, khách nào có nguy cơ rời bỏ, và họ tập trung ở đây?
- Nguyên nhân nào khiến một số khu vực có lợi nhuận âm?

**Nguồn dữ liệu:** [Superstore Dataset Final](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final) trên Kaggle — 9,994 dòng giao dịch, 793 khách hàng, giai đoạn 2014–2017, chỉ phạm vi Mỹ

**Công cụ sử dụng:** Python (pandas), Jupyter Notebook

## Stage 1: Data clearning & Preparation
- Load dữ liệu gốc, kiểm tra và xác nhận không có giá trị thiếu (null) hay dòng trùng lặp
- Parse đúng định dạng ngày tháng cho `Order Date` và `Ship Date`
- Tạo các cột tính toán mới:
  + `Shipping Days`: số ngày từ lúc đặt hàng đến khi giao (trung bình ~4 ngày)
  + `Profit Margin`: biên lợi nhuận trên mỗi dòng đơn hàng (trung bình 12%, nhưng có dòng lỗ tới -275% do discount sâu)
  + `Order Year`, `Order Month`: phục vụ phân tích xu hướng theo thời gian
- Join dữ liệu với bảng tọa độ ZIP code Mỹ (nguồn: SimpleMaps) qua `Postal Code`, chuẩn bị cho các bước phân tích/trực quan hóa địa lý ở giai đoạn sau
**Output:** `superstore_cleaned2.csv` — dữ liệu sạch, đã bổ sung các cột tính toán và tọa độ địa lý.


## Stage 2: Customer & regional Analysis
### Doanh thu & lợi nhuân theo bang
- Tổng hợp doanh thu, lợi nhuân, số đơn hàng (đếm theo 'Order ID' duy nhất) và biên lợi nhuận trung bình theo từng bang
- Phát hiện: một số bang có doanh thu cao nhưng **tổng lợi nhuận âm** — nguyên nhân ban đầu nghi ngờ liên quan đến mức giảm giá (discount) sâu trên một số dòng sản phẩm

### Average Order Value (AOV)
- Tính AOV theo Region và theo Segment khách hàng (Consumer/Corporate/Home Office)
- AOV = Tổng doanh thu ÷ Số đơn hàng duy nhất (không tính theo số dòng sản phẩm, tránh sai lệch do 1 đơn có nhiều sản phẩm)

### Phân khúc khách hàng bằng RFM
- Áp dụng mô hình RFM (Recency – Frequency – Monetary) cho 793 khách hàng
- Phân khúc thành 4 nhóm: **VIP**, **Loyal**, **Regular**, **At Risk / Churned**
- Ghép phân khúc với dữ liệu bang để xác định phân bố khách hàng VIP và khách có nguy cơ rời bỏ theo khu vực địa lý
**Output:** `customer_rfm_segments.csv` — bảng phân khúc khách hàng kèm chỉ số RFM và bang cư trú.


# phân khúc khách hàng RFM
phân loại các khách hoàng mua thường xuyên, mua gần đây, mua nhiều tiền hay là những khách hàng ít mua, mua 1 lần:
- R = recency
- F = Frequency
- M = Monetary
