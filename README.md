🛒 BA_project - Retail Demand Forecasting
Dự án dự báo nhu cầu bán lẻ được phát triển trong khuôn khổ cuộc thi ML Zoomcamp 2024 trên Kaggle, một phần của khóa học Machine Learning Zoomcamp do DataTalks.Club tổ chức. Mục tiêu của dự án là xây dựng mô hình dự đoán số lượng sản phẩm được bán ra dựa trên dữ liệu bán hàng từ các cửa hàng của một nhà bán lẻ.

🎯 Mục tiêu cuộc thi
Bài toán: Dự đoán nhu cầu sản phẩm trong tương lai dựa trên dữ liệu bán hàng trong 25 tháng từ 4 cửa hàng.

Tập huấn luyện: 7,640,724 samples

Tập kiểm tra: 883,680 samples

🔗 Link cuộc thi: [ML Zoomcamp 2024 - Kaggle](https://www.kaggle.com/competitions/ml-zoomcamp-2024-competition/overview)

📁 Cấu trúc dữ liệu
Tên file	Mô tả
sales.csv	Dữ liệu doanh số bán hàng tại cửa hàng (offline)
online.csv	Dữ liệu doanh số bán hàng online
markdown.csv	Danh sách các sản phẩm được giảm giá tại cửa hàng
price_history.csv	Lịch sử thay đổi giá sản phẩm
discount_history.csv	Lịch sử các chương trình giảm giá
actual_matrix.csv	Ma trận hiển thị các sản phẩm có mặt tại từng cửa hàng theo thời gian
catalog.csv	Thông tin mô tả sản phẩm
store.csv	Thông tin mô tả cửa hàng

🧠 Xử lý dữ liệu

❌ Loại bỏ một số feature để tránh data leakage
markdown: Do markdown thường được áp dụng cho sản phẩm bán chậm hoặc cần xả hàng (sau khi biết được hiệu suất bán), việc đưa vào mô hình gây rò rỉ dữ liệu (leakage).

➡️ Bị loại bỏ khỏi mô hình.
price_base, sum_total: Trực tiếp liên quan đến quantity → Loại bỏ để tránh học sai quan hệ.

✅ Fill missing value những feature tiềm năng và có tỉ lệ missing value thấp

✅ Sử dụng các feature mang tính nguyên nhân - kết quả rõ ràng
price_history: Dùng giá gần nhất trong quá khứ do không biết giá tương lai.

discount_history: Giữ lại các thông tin về ngày giảm giá, mức giá trước/sau giảm – có tác động trực tiếp đến hành vi mua hàng và xuất hiện trong cả tập test.

actual_matrix: Rất quan trọng – giúp mô hình hiểu rằng nếu sản phẩm không có mặt tại cửa hàng, thì sẽ không có doanh số → quantity = 0.

catalog: Giúp mô hình hiểu được đặc trưng sản phẩm (trọng lượng, thể tích, phân loại).

store: Chỉ giữ lại store_id, không dùng format và area vì cả 3 đều mang giá trị unique (dư thừa thông tin).

📊 Mô hình & Đánh giá
Xây dựng 3 mô hình khác nhau, huấn luyện và đánh giá trên tập validation nội bộ, sau đó so sánh kết quả với leaderboard của cuộc thi:
Kết quả cuộc thi: 
[ML Zoomcamp 2024 LeaderBoard](https://www.kaggle.com/competitions/ml-zoomcamp-2024-competition/leaderboard?)

Kết quả 3 mô hình:

![Image](https://github.com/user-attachments/assets/bab4aed4-2548-4a6f-80a7-451ae64bb962)
