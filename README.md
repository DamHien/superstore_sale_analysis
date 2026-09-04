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

# phân khúc khách hàng RFM
phân loại các khách hoàng mua thường xuyên, mua gần đây, mua nhiều tiền hay là những khách hàng ít mua, mua 1 lần
    R = recency
    F = Frequency
    M = Monetary
