### 1. Giới thiệu (Introduction)

Trong thế giới dữ liệu khổng lồ ngày nay, khả năng rút trích thông tin có giá trị và đưa ra dự đoán thông minh là chìa khóa để giải quyết vô vàn bài toán thực tế. Đây chính là lúc Machine Learning phát huy sức mạnh của mình. Tuần này, chúng ta đã tiếp cận hai "người bạn" quen thuộc: **KNN** và **K-Means**. Chúng không chỉ là những thuật toán đơn thuần mà còn là những đại diện tiêu biểu cho cách chúng ta tiếp cận dữ liệu – một cách có nhãn (supervised) hoặc không có nhãn (unsupervised).

Việc nắm vững hai thuật toán này không chỉ giúp bạn xây dựng nền tảng vững chắc về Machine Learning mà còn mở ra cánh cửa đến nhiều ứng dụng thực tế, từ việc phân loại khách hàng, chẩn đoán bệnh, cho đến xử lý ảnh và văn bản. Hãy cùng đi sâu vào tìm hiểu nhé!


---


### 2. Kiến thức trọng tâm (Key Concepts)

#### 2.1. K-Nearest Neighbors (KNN)

KNN là một trong những thuật toán học **có giám sát** (Supervised Learning) đơn giản và dễ hiểu nhất. Nó được mệnh danh là thuật toán "lười học" (Lazy Learning) hay "học dựa trên trường hợp" (Instance-based Learning). Tại sao lại gọi là "lười học"? Bởi vì trong giai đoạn huấn luyện, KNN **không thực sự xây dựng một mô hình rõ ràng** hay học bất kỳ tham số nào; nó chỉ đơn giản là **lưu trữ toàn bộ tập dữ liệu huấn luyện**. Quá trình "học" thực sự chỉ bắt đầu khi có một điểm dữ liệu mới cần được phân loại hoặc dự đoán.

KNN có thể được sử dụng cho hai loại bài toán chính:

- **Phân loại (Classification):** Xác định nhãn (loại) cho một điểm dữ liệu mới. Ví dụ, phân loại hoa Iris dựa trên các đặc trưng của nó.
- **Hồi quy (Regression):** Dự đoán một giá trị liên tục cho một điểm dữ liệu mới. Ví dụ, dự đoán giá nhà hoặc nhiệt độ ngày mai.

**Nguyên lý hoạt động của KNN (Phân loại):** Giả sử chúng ta có một điểm dữ liệu mới (điểm kiểm thử) cần phân loại. Quá trình diễn ra như sau:

- **Bước 1: Chọn số K (số láng giềng gần nhất)**. Đây là một con số quan trọng mà chúng ta sẽ nói kỹ hơn sau. Ví dụ, nếu K=3, chúng ta sẽ tìm 3 láng giềng gần nhất.

![[Pasted image 20250808205402.png]]

- **Bước 2: Tính toán độ tương đồng (hay khoảng cách)** giữa điểm dữ liệu mới và TẤT CẢ các điểm dữ liệu đã có trong tập huấn luyện. Có nhiều loại khoảng cách khác nhau để lựa chọn, phổ biến nhất là **Khoảng cách Euclidean (Euclidean Distance)**. Ngoài ra, còn có các loại khoảng cách khác như Manhattan distance, Minkowski distance, Chebyshev, Cosine, Hamming Distance, v.v..

![[Pasted image 20250808205420.png]]

![[Pasted image 20250808205458.png]]

- **Bước 3**: Sắp xếp các khoảng cách đã tính theo thứ tự tăng dần** và **chọn ra K điểm có khoảng cách nhỏ nhất** (tức là K láng giềng gần nhất).

![[Pasted image 20250808205528.png]]

- **Bước 4**: Bỏ phiếu (Voting) và dự đoán kết quả**. Trong K láng giềng gần nhất mà chúng ta vừa tìm được, chúng ta sẽ xem lớp nào xuất hiện nhiều nhất. Lớp nào "được bỏ phiếu" nhiều nhất sẽ là lớp dự đoán cho điểm dữ liệu mới đó.

![[Pasted image 20250808205544.png]]

---

#### 2.2. K-Means Clustering

K-Means là một thuật toán học **không giám sát** (Unsupervised Learning) mạnh mẽ, được sử dụng để **phân cụm (clustering) dữ liệu chưa được gán nhãn**. Mục tiêu của K-Means là nhóm các điểm dữ liệu có đặc điểm tương tự nhau vào cùng một cụm (cluster).

**Nguyên lý hoạt động của K-Means:** Quá trình phân cụm K-Means diễn ra theo các bước lặp:

1. **Khởi tạo K:** Xác định số lượng cụm (K) mà bạn muốn tạo ra.
2. **Chọn tâm cụm ban đầu:** Thuật toán chọn K điểm dữ liệu ngẫu nhiên từ tập dữ liệu làm các tâm cụm (centroids) ban đầu.
3. **Gán điểm dữ liệu vào cụm:** Với mỗi điểm dữ liệu, tính khoảng cách đến tất cả các tâm cụm và **gán điểm đó vào cụm có tâm gần nhất**.
4. **Cập nhật tâm cụm:** Sau khi tất cả các điểm đã được gán, tính toán lại vị trí mới của mỗi tâm cụm bằng cách lấy **trung bình** tất cả các điểm thuộc cụm đó.
5. **Lặp lại:** Các bước 3 và 4 được lặp lại cho đến khi các tâm cụm không thay đổi đáng kể nữa (đạt trạng thái hội tụ) hoặc đạt đến số lần lặp tối đa.

![[Pasted image 20250806220655.png]]


---


### 3. Phân tích nâng cao (Advanced Insights)

#### 3.1. KNN: Mạnh mẽ nhưng cần tinh chỉnh

**Ưu điểm của KNN:**

- **Đơn giản và dễ hiểu:** Nguyên lý hoạt động dựa trên "hàng xóm" rất trực quan.
- **Không cần huấn luyện rõ ràng:** Tiết kiệm thời gian ở giai đoạn training vì chỉ lưu trữ dữ liệu.
- **Không giả định về phân phối dữ liệu:** Nó là một thuật toán phi tham số (non-parametric), không yêu cầu dữ liệu phải tuân theo một phân phối cụ thể nào.

**Nhược điểm và cách tối ưu:**

- **Chi phí tính toán cao khi dự đoán:** Vì phải tính khoảng cách với _tất cả_ các điểm huấn luyện mỗi khi có dữ liệu mới, KNN có thể rất chậm với các tập dữ liệu lớn.
    - **Giải pháp:** Để khắc phục, có thể sử dụng các cấu trúc dữ liệu như **K-D Tree (K-Dimensional Tree)**. K-D Tree tổ chức dữ liệu theo cây phân cấp, giúp tìm kiếm K hàng xóm gần nhất nhanh hơn nhiều so với phương pháp "brute-force" (duyệt toàn bộ).
- **Nhạy cảm với nhiễu và outlier:** Một điểm dữ liệu ngoại lai có thể ảnh hưởng lớn đến việc xác định K hàng xóm gần nhất và kết quả dự đoán.
- **Thách thức chọn K:** Giá trị K ảnh hưởng trực tiếp đến hiệu suất mô hình.
    - **Chọn K tối ưu:** Chúng ta thường thử nghiệm nhiều giá trị K khác nhau và đánh giá trên tập validation (tập kiểm định) bằng các chỉ số như **Accuracy (độ chính xác), Classification Report (Precision, Recall, F1-Score)** hoặc **Error Analysis (phân tích lỗi)**. Việc lựa chọn K lẻ thường được ưu tiên trong phân loại để tránh trường hợp hòa phiếu.
- **Khoảng cách và Trọng số:**
    - Các độ đo khoảng cách khác nhau (Euclidean, Manhattan, v.v.) sẽ phù hợp với các loại dữ liệu khác nhau.
    - Có thể áp dụng các loại trọng số cho các hàng xóm: **Uniform Weights** (tất cả các hàng xóm đều có trọng số như nhau), **Distance Weights** (hàng xóm gần hơn có trọng số cao hơn), hoặc **User-Defined Weights** (trọng số tùy chỉnh). Việc gán trọng số có thể giúp giảm ảnh hưởng của các điểm nhiễu.
- **Tỷ lệ đặc trưng (Feature Scaling):** Nếu các đặc trưng có thang đo khác nhau (ví dụ: tuổi từ 0-100, thu nhập từ 0-100.000), đặc trưng có giá trị lớn hơn sẽ chi phối việc tính khoảng cách.
    - **Giải pháp:** Cần thực hiện **chuẩn hóa (Normalization)** hoặc **chuẩn hóa theo Z-score (Standardization)** để đưa các đặc trưng về cùng một thang đo trước khi áp dụng KNN.


---

#### 3.2. K-Means: Phân cụm hiệu quả nhưng cần cân nhắc

**Ưu điểm của K-Means:**

- **Đơn giản và tốc độ:** Dễ hiểu và triển khai, thường hội tụ nhanh chóng.
- **Hiệu quả với dữ liệu lớn:** Tương đối hiệu quả về mặt tính toán, đặc biệt với các bộ dữ liệu lớn khi số lượng cụm K không quá cao.

**Nhược điểm và cách tối ưu:**

- **Cần xác định K trước:** Đây là một hạn chế lớn nhất. Làm sao để biết dữ liệu của bạn nên được chia thành bao nhiêu cụm?
    - **Elbow Method (Phương pháp Khuỷu tay):** Phương pháp này dựa trên **Within-Cluster Sum of Squares (WCSS)**, hay còn gọi là Inertia. WCSS đo tổng bình phương khoảng cách từ mỗi điểm dữ liệu đến tâm cụm của nó. Chúng ta sẽ chạy K-Means với nhiều giá trị K khác nhau và vẽ biểu đồ WCSS theo K. Điểm "khuỷu tay" trên biểu đồ, nơi WCSS giảm chậm lại rõ rệt, thường được coi là giá trị K tối ưu.
    - **Silhouette Method (Phương pháp Silhouette):** Phương pháp này đo lường mức độ tách biệt của các cụm. Điểm Silhouette cho mỗi điểm dữ liệu được tính dựa trên hai yếu tố:
        - `a(i)`: Khoảng cách trung bình từ điểm `i` đến tất cả các điểm khác trong cùng cụm (đo độ gắn kết).
        - `b(i)`: Khoảng cách trung bình từ điểm `i` đến tất cả các điểm trong cụm gần nhất khác (đo độ tách biệt).
        - Điểm Silhouette `s(i)` được tính bằng công thức: `s(i) = (b(i) - a(i)) / max(a(i), b(i))`. Giá trị `s(i)` nằm trong khoảng [-1, 1], với giá trị cao hơn cho thấy cụm tốt hơn (các điểm nằm gần tâm cụm của chúng và xa các cụm khác). Chúng ta chọn K có điểm Silhouette trung bình cao nhất.
- **Nhạy cảm với khởi tạo tâm cụm ban đầu:** Vì tâm cụm được chọn ngẫu nhiên, các lần chạy khác nhau của K-Means có thể cho ra kết quả phân cụm khác nhau.
    - **Giải pháp:** Thường chạy thuật toán nhiều lần với các điểm khởi tạo ngẫu nhiên khác nhau (ví dụ: `n_init` trong thư viện scikit-learn) và chọn kết quả tốt nhất. Các kỹ thuật khởi tạo thông minh hơn như K-Means++ cũng có thể được sử dụng.
- **Chỉ hiệu quả với các cụm có hình dạng cầu:** K-Means giả định các cụm có hình dạng gần giống hình cầu và kích thước tương tự. Nó có thể gặp khó khăn với các cụm có hình dạng phức tạp hoặc mật độ khác nhau.
- **Nhạy cảm với outlier:** Các điểm ngoại lai có thể kéo tâm cụm lệch đi, làm sai lệch kết quả phân cụm.


---


### 4. Ứng dụng thực tiễn (Practical Applications)

KNN và K-Means, dù đơn giản, lại có rất nhiều ứng dụng trong thực tế:

#### 4.1. Ứng dụng của KNN

- **Phân loại sinh vật:**
    - **Phân loại hoa Iris:** Đây là ví dụ kinh điển. KNN có thể phân loại các loài hoa Iris (Setosa, Versicolor, Virginica) dựa trên chiều dài/chiều rộng cánh hoa và đài hoa, với độ chính xác cao.
- **Y học:**
    - **Chẩn đoán bệnh:** Trong phân tích y tế, KNN có thể được dùng để phân loại bệnh nhân có hoặc không có bệnh dựa trên các triệu chứng hoặc kết quả xét nghiệm. Ví dụ, với dữ liệu về bệnh tiểu đường (Diabetes Dataset), KNN có thể dự đoán mức độ nghiêm trọng của bệnh.
- **Hệ thống gợi ý (Recommender Systems):**
    - KNN có thể tìm ra những người dùng có "gu" (sở thích) tương tự (K hàng xóm gần nhất) và gợi ý các sản phẩm/nội dung mà những người đó thích.
- **Xử lý ngôn ngữ tự nhiên (NLP):**
    - **Phân loại văn bản/cảm xúc (IMDB Text Classification):** KNN có thể phân loại một đoạn văn bản (ví dụ: bình luận phim) là tích cực hay tiêu cực. Để làm được điều này, văn bản cần được chuyển đổi thành các vector số (ví dụ: sử dụng kỹ thuật **Bag of Words - BoW**). BoW đơn giản là đếm số lần xuất hiện của mỗi từ trong tài liệu, tạo thành một vector đặc trưng.

---

#### 4.2. Ứng dụng của K-Means

- **Phân khúc thị trường:**
    - **Phân nhóm khách hàng (Mall Customer Dataset):** Các công ty có thể sử dụng K-Means để phân loại khách hàng dựa trên tuổi, giới tính, thu nhập, và hành vi chi tiêu. Điều này giúp họ tạo ra các chiến dịch marketing cá nhân hóa hiệu quả hơn (ví dụ: nhóm khách hàng VIP, khách hàng thông thường, khách hàng tiềm năng).
- **Xử lý ảnh (Image Processing):**
    - **Phân đoạn ảnh (Image Segmentation):** K-Means có thể nhóm các pixel có màu sắc hoặc đặc trưng quang phổ tương tự lại với nhau, giúp tách các đối tượng trong ảnh hoặc nén ảnh. Điều này đặc biệt hữu ích trong các ứng dụng như phân tích hình ảnh y tế hoặc giám sát môi trường.
- **Phát hiện bất thường (Anomaly Detection):**
    - K-Means có thể được sử dụng để phát hiện các hành vi hoặc điểm dữ liệu bất thường. Các điểm dữ liệu nằm rất xa tâm cụm của bất kỳ cụm nào có thể được coi là outlier. Ví dụ, phát hiện các giao dịch gian lận trong ngân hàng hoặc các cuộc tấn công mạng.
- **Tiền xử lý dữ liệu (Data Preprocessing):**
    - **Giảm số chiều/Phân cụm dữ liệu để hỗ trợ thuật toán khác:** K-Means có thể giúp giảm số lượng "class" của một bài toán gốc bằng cách nhóm các điểm dữ liệu lại thành các cụm nhỏ hơn, giúp các thuật toán khác học hiệu quả hơn. Ví dụ, trong phân tích dữ liệu CO2 của các tỉnh thành, K-Means có thể phân cụm các tỉnh thành có đặc điểm phát thải tương tự trước khi áp dụng thuật toán Markov Chain để dự đoán xu hướng CO2.
    - **Lọc nhiễu và ổn định mô hình:** Trong một số mô hình phức tạp, K-Means có thể được dùng để chọn ra các đặc trưng (ví dụ: class embeddings) tốt nhất, giúp giảm nhiễu và giữ cho mô hình gọn nhẹ.
- **Tối ưu tham số/siêu tham số:**
    - Trong một số bài toán kỹ thuật, K-Means có thể hỗ trợ lựa chọn các siêu tham số tối ưu cho các vật liệu hoặc điều kiện khác nhau, ví dụ như trong dự đoán hư hại nguyên vật liệu bằng sóng cao tần.


---


### 5. Gợi mở (Further Exploration)

KNN và K-Means là điểm khởi đầu tuyệt vời. Để đào sâu hơn, bạn có thể nghiên cứu:

- **Các thuật toán phân cụm khác:** DBSCAN (Density-Based Spatial Clustering of Applications with Noise) cho các cụm có hình dạng bất kỳ, hoặc Hierarchical Clustering cho việc xây dựng cây phân cấp cụm.
- **Các thuật toán phân loại/hồi quy khác:** Support Vector Machines (SVM), Decision Trees, Random Forests, Naive Bayes.
- **Các kỹ thuật tối ưu hóa:** Tìm hiểu sâu hơn về cách K-D Tree được xây dựng và tối ưu, hoặc các phương pháp khởi tạo tâm cụm trong K-Means (K-Means++).
- **Thư viện và công cụ:** Thực hành triển khai KNN và K-Means bằng các thư viện như Scikit-learn trong Python, thử nghiệm trên các bộ dữ liệu khác nhau.
- **Kết hợp các thuật toán:** Có thể kết hợp KNN và K-Means? Ví dụ, K-Means có thể được dùng để giảm số lượng điểm dữ liệu trong tập huấn luyện cho KNN bằng cách sử dụng các tâm cụm như các đại diện.