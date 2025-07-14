### **1. Giới thiệu (Introduction)**

"Làm sao để so sánh mức độ giống nhau giữa hai tài liệu?" "Làm sao để cắt người ra khỏi hậu cảnh mà không cần Photoshop?" "Làm sao mà Python có thể xử lý mảng dữ liệu nhanh như vậy?"

Chúng mình đã bắt đầu tuần đầu tiên của Module 2 trong AIO2025 bằng những câu hỏi rất đời thường như thế. Và đáp án cho tất cả nằm trong hai công cụ cực kỳ quốc dân: **Numpy** (thư viện tính toán số) và **Đại số tuyến tính (Linear Algebra)**.

Numpy giúp Python trở thành công cụ xử lý dữ liệu hữu hiệu nhất. Còn Đại số tuyến tính cung cấp ngôn ngữ toán học để ta có thể hiểu, chuyển đổi, so sánh hay biểu diễn thông tin trong dữ liệu.

Trong blog này, chúng mình sẽ cùng nhau lướt qua những khái niệm cốt lõi, những thao tác cơ bản, và những ứng dụng thực tế đã được đào sâu trong tuần đầu tiên. Dù bạn là người bắt đầu hay đang trên hành trình chinh phục AI, những nội dung này chắc chắn sẽ giúp ích rất nhiều!


---


### **2. Kiến thức trọng tâm (Key Concepts)**

#### **2.1. Cơ bản về Numpy (Numpy Basics)**

**Numpy** là một thư viện cực kỳ quan trọng trong Python giúp xử lý các mảng số (numerical arrays) một cách nhanh chóng và hiệu quả. Thay vì phải dùng các vòng lặp `for` chậm chạp như trong Python thuần, chúng mình có thể thao tác trên toàn bộ mảng chỉ với một dòng lệnh.

Một số thao tác cơ bản mà chúng mình đã học gồm:

- **Tạo mảng (array creation)**:
    - `np.array([1, 2, 3])`: tạo mảng từ list Python
    - `np.zeros((3, 4))`: tạo mảng toàn số 0
    - `np.ones((2, 2))`: tạo mảng toàn số 1
    - `np.random.rand(2, 3)`: tạo mảng số thực ngẫu nhiên
- **Thuộc tính của mảng (array attributes)**:
    - `.ndim`: số chiều của mảng
    - `.shape`: kích thước mỗi chiều
    - `.size`: tổng số phần tử
    - `.dtype`: kiểu dữ liệu của phần tử
- **Truy cập dữ liệu (indexing & slicing)**:
    - Lấy phần tử đơn: `a[0, 1]`
    - Cắt lát (slice): `a[:, 0]` để lấy toàn bộ cột đầu tiên
- **Thay đổi hình dạng (reshape)**:
    - `a.reshape(2, 3)` để chuyển mảng thành 2 hàng 3 cột
- **Broadcasting**:
    - Cho phép thực hiện phép toán giữa hai mảng khác kích thước, ví dụ:

```python
a = np.array([[1, 2], [3, 4]])
b = np.array([10, 20])
print(a + b)  # [[11 22], [13 24]]
```

Nhờ các thao tác trên, chúng mình có thể xử lý dữ liệu hàng nghìn dòng chỉ trong vài mili-giây. Đó chính là nền tảng cho việc huấn luyện mô hình AI, tiền xử lý dữ liệu lớn hay xây dựng các thuật toán tối ưu.

---

#### **2.2. Đại số tuyến tính (Linear Algebra)**

Đại số tuyến tính (Linear Algebra) chính là nền tảng toán học cho mọi phép tính trên vector (vectors) và ma trận (matrices) – những thành phần cốt lõi trong mô hình học máy (machine learning models).

Một số khái niệm và thao tác quan trọng mà chúng mình đã thực hành:

- **Độ dài vector (vector length / norm)**:
    - Công thức:  $\|v\| = \sqrt{v_1^2 + v_2^2 + \dots + v_n^2}$
    - Dùng để đo độ lớn của vector
- **Tích vô hướng (dot product)**:
    - Công thức: $v \cdot u = \sum v_i u_i$
    - Ứng dụng trong tính cosine similarity hoặc chiếu vector
- **Nhân vector với ma trận (matrix-vector multiplication)**:
    - Tính biến đổi tuyến tính (linear transformation) của vector
- **Nhân ma trận với ma trận (matrix-matrix multiplication)**:
    - Là phép toán quan trọng trong mạng neural, hệ phương trình, biến đổi không gian, v.v.

Ví dụ minh họa đơn giản bằng Numpy:

Giả sử chúng mình có bảng điểm của 3 sinh viên với 4 môn học:

| Sinh viên   | **Toán (2)** | **Lý (3)** | **Hóa (1)** | **Anh (2)** |
| ----------- | ------------ | ---------- | ----------- | ----------- |
| Sinh viên 1 | 7            | 8          | 6           | 9           |
| Sinh viên 2 | 5            | 9          | 7           | 8           |
| Sinh viên 3 | 8            | 7          | 8           | 6           |

Trong đó các hệ số lần lượt là: `Toán: 2`, `Lý: 3`, `Hóa: 1`, `Anh: 2`.
Ta có thể dùng phép nhân ma trận để tính tổng điểm có trọng số như sau:

```python
import numpy as np

# Bảng điểm của sinh viên
scores = np.array([
    [7, 8, 6, 9],
    [5, 9, 7, 8],
    [8, 7, 8, 6]
])

# Vector hệ số môn học
weights = np.array([2, 3, 1, 2])

# Tính tổng điểm có trọng số
weighted_totals = np.dot(scores, weights)

# Tính điểm trung bình
weighted_avg = weighted_totals / weights.sum()

print(weighted_avg)  # Kết quả: [7.7 7.1 7.3]
```

Kết quả cho thấy điểm trung bình có trọng số lần lượt của 3 sinh viên là 7.7, 7.1 và 7.3. Đây là một ví dụ đơn giản nhưng điển hình cho cách vận dụng đại số tuyến tính trong đời sống thực tế

Chúng mình còn học cách vận dụng các phép toán này để phục vụ cho các bài toán thực tế như tính độ tương đồng (cosine similarity), thay nền ảnh, và phân tích dữ liệu bảng – những phần sẽ được trình bày trong các mục tiếp theo.

---

#### **2.3. Cosine Similarity: Đo độ tương đồng giữa hai vector (vectors)**

Khi làm việc với dữ liệu văn bản, hình ảnh hoặc hệ thống gợi ý, chúng mình thường gặp bài toán: “Làm sao để biết hai đối tượng giống nhau tới mức nào?”. Câu trả lời nằm ở một công cụ toán học rất mạnh mẽ: **Cosine Similarity (độ tương đồng cosine)**.

##### **2.3.1. Ý tưởng cơ bản**

Thay vì so sánh trực tiếp các giá trị, cosine similarity dựa vào **góc giữa hai vector** để đo độ giống nhau. Hai vector càng gần nhau (góc càng nhỏ) thì cosine similarity càng gần 1.

**Công thức:**
$$
\text{cosine}(x, y) = \frac{x \cdot y}{\|x\| \cdot \|y\|}
$$

Trong đó:
- $x \cdot y$: tích vô hướng giữa hai vector
- $\|x\|, \|y\|$: độ dài của vector (vector norm)

![[Pasted image 20250714213045.png]]
##### **2.3.2. Ví dụ minh họa**

Giả sử chúng mình có hai vector đặc trưng cho hai tài liệu:
```python
import numpy as np

x = np.array([1, 2, 3, 4])
y = np.array([1, 0, 3, 0])

dot_product = np.dot(x, y)
norm_x = np.linalg.norm(x)
norm_y = np.linalg.norm(y)

cos_sim = dot_product / (norm_x * norm_y)
print(round(cos_sim, 3))  # Kết quả: 0.577
```

Kết quả cho thấy độ tương đồng giữa hai vector là **0.577**, tức là chúng có một mức độ tương đồng vừa phải.

##### **2.3.3. Ứng dụng thực tế**

- **Xử lý ngôn ngữ tự nhiên (NLP)**: so sánh văn bản, tìm kiếm văn bản gần nghĩa.
- **Recommender systems (hệ thống gợi ý)**: gợi ý sản phẩm tương tự dựa trên hành vi người dùng.
- **Phát hiện ảnh trùng lặp**: so sánh đặc trưng ảnh để phát hiện sự trùng khớp.

---

#### **2.4. Xử lý ảnh với Numpy (Image Processing with Numpy)**

Khi nhắc đến xử lý ảnh (image processing), người ta thường nghĩ đến các thư viện chuyên sâu như OpenCV hay PIL. Tuy nhiên, chỉ với **Numpy**, chúng mình đã có thể làm được nhiều điều thú vị – từ chuyển ảnh màu sang ảnh xám cho đến kỹ thuật tách nền.

##### **2.4.1. Ảnh là ma trận**

Một bức ảnh số thực chất là một **ma trận nhiều chiều (multidimensional array)**, trong đó mỗi phần tử biểu diễn một **pixel**. Với ảnh màu RGB:

- Kích thước ảnh sẽ là (Height, Width, 3)
- 3 kênh tương ứng với **Red, Green, Blue**

Vì vậy, việc xử lý ảnh bằng Numpy thực chất là **thao tác với các mảng số (numerical arrays)** – đúng sở trường của thư viện này!

![[Pasted image 20250714213208.png]]
##### **2.4.2. Chuyển ảnh màu sang ảnh xám (Grayscale conversion)**

Chúng mình đã thử 3 phương pháp phổ biến để chuyển đổi ảnh màu sang ảnh xám (grayscale image):

| **Phương pháp** | **Công thức**                         | **Đặc điểm**                             |
| --------------- | ------------------------------------- | ---------------------------------------- |
| **Lightness**   | $\frac{\max(R,G,B) + \min(R,G,B)}{2}$ | Đơn giản, chú ý độ tương phản            |
| **Average**     | $\frac{R + G + B}{3}$                 | Trung bình đều ba kênh                   |
| **Luminosity**  | $0.21R + 0.72G + 0.07B$               | Tái hiện đúng độ sáng con người cảm nhận |

Ví dụ:

```python
gray_img = (0.21 * img[:, :, 0] + 0.72 * img[:, :, 1] + 0.07 * img[:, :, 2]).astype(np.uint8)
```

Phép tính này được thực hiện cho **mọi pixel trong ảnh** chỉ bằng một dòng code – lợi thế lớn của Numpy!

| **Thành phần trong code**            | **Ý nghĩa cụ thể**                                                                              |
| ------------------------------------ | ----------------------------------------------------------------------------------------------- |
| `img[:, :, 0]`                       | Lấy toàn bộ kênh **Red** của ảnh                                                                |
| `img[:, :, 1]`                       | Lấy toàn bộ kênh **Green**                                                                      |
| `img[:, :, 2]`                       | Lấy toàn bộ kênh **Blue**                                                                       |
| `0.21 * ..., 0.72 * ..., 0.07 * ...` | Trọng số tương ứng với độ nhạy cảm của mắt người với từng màu (theo phương pháp **Luminosity**) |
| `+`                                  | Cộng các giá trị trọng số lại để tạo ảnh xám                                                    |
| `.astype(np.uint8)`                  | Ép kết quả về kiểu **unsigned int 8-bit** (giá trị pixel từ 0 đến 255 – chuẩn ảnh grayscale)    |
| `gray_img = ...`                     | Lưu ảnh xám kết quả vào biến gray_img                                                           |

##### **2.4.3. Tách nền ảnh (Background subtraction)**

Một kỹ thuật thú vị khác mà chúng mình đã thực hành là **tách đối tượng khỏi nền xanh (greenscreen)**. Cách làm gồm 4 bước:
1. **Resize ảnh**: Đảm bảo ảnh nền, ảnh đối tượng và nền mới cùng kích thước.
2. **Tính độ chênh lệch (difference)** giữa ảnh gốc và ảnh có đối tượng.
3. **Tạo binary mask**: Mặt nạ phân biệt vùng nền và vùng chứa đối tượng.
4. **Ghép nền mới**: Dùng np.where() để thay thế pixel tương ứng.

Ví dụ:

```python
output = np.where(binary_mask == 255, object_img, new_background)
```

##### **2.4.4. Ứng dụng thực tế**

- Làm nền cho video call (chạy ngay trong trình duyệt!)
- Tách người ra khỏi ảnh để đưa vào poster
- Chuyển ảnh màu sang trắng đen để nén dung lượng hoặc phục vụ nhận diện

Những thao tác tưởng chừng “cao siêu” này thực chất chỉ là những phép toán đơn giản trên ma trận. Nhờ **Numpy**, xử lý ảnh trở nên trực quan và nhanh chóng hơn bao giờ hết.

---

#### **2.5. Phân tích dữ liệu dạng bảng (Tabular Data Analysis)**

Dữ liệu trong thực tế không phải lúc nào cũng là ảnh hay âm thanh – phần lớn là các bảng dữ liệu (dạng **bảng tính – spreadsheets**, **file CSV**, **dữ liệu từ database**). Với **Numpy** và **Pandas**, chúng mình có thể dễ dàng thao tác, xử lý và phân tích những bảng dữ liệu này.

Trong tuần học, chúng mình đã làm việc với một tập dữ liệu quảng cáo (advertising dataset) gồm 4 cột: 

|**TV (ngân sách)**|**Radio**|**Newspaper**|**Sales (doanh số)**|
|---|---|---|---|

![[Pasted image 20250714213336.png]]

##### **2.5.1. Đọc dữ liệu bằng Pandas**

Pandas cho phép đọc dữ liệu rất dễ dàng:

```python
import pandas as pd
df = pd.read_csv("advertising.csv")
```

Sau đó, chuyển dữ liệu sang Numpy để thao tác số học nhanh hơn:

```python
data = df.to_numpy()
```


##### **2.5.2. Các thao tác phân tích cơ bản**

Dưới đây là một số ví dụ điển hình:

- 🔍 **Tìm giá trị lớn nhất cột Sales và vị trí tương ứng**
```python
sales = data[:, -1]
max_value = np.max(sales)
max_index = np.argmax(sales)
```

- 📊 **Tính trung bình cột TV**
```python
tv = data[:, 0]
mean_tv = np.mean(tv)
```

- 📈 **Đếm số dòng có Sales ≥ 20**
```python
count = np.sum(sales >= 20)
```

- 🧠 **Tính trung bình Radio với điều kiện Sales ≥ 15**
```python
radio = data[:, 1]
mean_radio = np.mean(radio[sales >= 15])
```

- 📦 **Tính tổng Sales với điều kiện Newspaper > trung bình**
```python
newspaper = data[:, 2]
mean_news = np.mean(newspaper)
sum_sales = np.sum(sales[newspaper > mean_news])
```

##### **2.5.3. Ứng dụng thực tế**

- **Kinh doanh**: phân tích mối liên hệ giữa chi phí quảng cáo và doanh số.
- **Tài chính**: phân tích xu hướng thu chi, dự đoán lợi nhuận.
- **Y tế**: thống kê dữ liệu bệnh án, tỉ lệ hồi phục, chi phí điều trị.
- **Khoa học dữ liệu**: xử lý tập dữ liệu trước khi huấn luyện mô hình học máy.

Với Numpy và Pandas, chúng mình có thể xử lý **hàng trăm nghìn dòng dữ liệu** một cách linh hoạt và nhanh chóng – đó là nền móng cho phân tích dữ liệu hiện đại.


---


### **3. Phân tích nâng cao (Advanced Insights)**

Sau khi đã thực hành các kỹ thuật với **Numpy** và **Đại số tuyến tính (Linear Algebra)**, chúng mình nhận ra rằng: đằng sau những dòng code tưởng chừng đơn giản là **những nguyên lý toán học và kỹ thuật tối ưu rất sâu sắc**. Dưới đây là những phân tích giúp hiểu bản chất và lý do vì sao những công cụ này lại quan trọng đến vậy trong thế giới AI và dữ liệu.

#### **3.1. Vì sao Numpy lại nhanh và mạnh?**

- **Tối ưu ở tầng thấp (low-level optimization)**: Numpy sử dụng các thư viện C/C++ dưới nền nên chạy nhanh hơn vòng lặp Python rất nhiều.
- **Broadcasting**: Cho phép viết code ngắn gọn nhưng vẫn thực hiện được những phép toán phức tạp.
- **Vector hóa (vectorization)**: Thay vì xử lý từng phần tử, Numpy xử lý cả mảng cùng lúc – tiết kiệm thời gian và tài nguyên.

➡️ Đây là lý do tại sao mọi thư viện học máy (machine learning libraries) như scikit-learn, TensorFlow, PyTorch… đều dùng Numpy bên dưới.

---
  
#### **3.2. Cosine Similarity – Vì sao lại phổ biến?**

Khi so sánh hai đối tượng (như văn bản, người dùng, ảnh…), có nhiều cách để đo mức độ “giống nhau”. Một cách quen thuộc là nhìn vào **độ chênh lệch giá trị giữa các phần tử** – nhưng phương pháp đó lại dễ bị ảnh hưởng nếu một vector lớn gấp nhiều lần vector còn lại (ví dụ một văn bản dài so với văn bản ngắn).

**Cosine similarity** thì khác: nó chỉ quan tâm đến **góc giữa hai vector**, chứ không quan tâm đến độ dài (tức là tổng độ lớn). Nhờ vậy, nó vẫn đo được mức độ tương đồng **về hướng** dù hai đối tượng có quy mô khác nhau.

Ví dụ:
- Một người nghe 50 bài nhạc indie và một người nghe 5 bài giống y hệt → Cosine similarity vẫn đánh giá cao vì “gu giống nhau”.
- Một bài viết ngắn và bài viết dài nhưng dùng từ khóa tương tự → Vẫn có độ tương đồng cao.

✅ Chính vì tính chất này, cosine similarity được ứng dụng nhiều trong:
- **Tìm kiếm văn bản** (search engines)
- **Hệ thống gợi ý** (recommender systems)
- **So khớp hành vi người dùng** (user behavior matching)

---

#### **3.3. Tách nền ảnh – nền tảng cho nhiều công nghệ lớn**

- **Segmentation (phân đoạn ảnh)** là bước quan trọng trong Computer Vision.
- Kỹ thuật background subtraction là tiền đề cho:
    - Deepfake
    - Green screen trong truyền hình
    - AR (Augmented Reality)
- Dù thuật toán đơn giản (so sánh pixel), nhưng nếu hiểu và kiểm soát tốt, nó giúp phát triển những ứng dụng rất “cool”.

---

#### **3.4. Phân tích dữ liệu: Từ bảng tính đến AI**

- Numpy giúp chuyển từ dữ liệu bảng (tabular data) sang dạng **vector và ma trận**, là định dạng đầu vào của mọi mô hình học máy.
- Biết cách **lọc, thống kê, trích xuất theo điều kiện** giúp rút ngắn 80% thời gian xử lý dữ liệu thực tế (data preprocessing).

Nói cách khác, những gì chúng mình học trong tuần này **không chỉ là cú pháp Python**, mà là **cách tư duy bằng dữ liệu** – một kỹ năng quan trọng với bất kỳ ai làm việc trong lĩnh vực công nghệ hiện đại.


---


### **4. Ứng dụng thực tiễn (Practical Applications)**

Những kiến thức nền tảng từ Numpy và đại số tuyến tính có thể được ứng dụng vào nhiều kịch bản thực tế trong AI và xử lý dữ liệu. Dưới đây là 4 ví dụ tiêu biểu mà chúng mình thấy thực sự hữu ích:

#### **4.1. Dự đoán thông tin trong hệ thống AI (AI-powered Inference)**

Một khi dữ liệu được chuyển thành vector hoặc ma trận, mô hình AI có thể thực hiện dự đoán rất nhanh. Numpy là công cụ giúp:

- Tiền xử lý dữ liệu đầu vào: chuẩn hóa, mã hóa, tạo đặc trưng
- Biến đổi dữ liệu thành dạng có thể đưa vào mô hình
- Tính toán đầu ra (output) trong quá trình inference

📌 _Ví dụ_: Trong chatbot thông minh, câu hỏi của người dùng được vector hóa và đưa vào model để dự đoán câu trả lời phù hợp.

---

#### **4.2. Phát hiện bất thường với Cosine Similarity (Anomaly Detection)**

Cosine similarity có thể dùng để so sánh một sự kiện mới với các hành vi bình thường đã ghi nhận. Nếu độ tương đồng thấp bất thường, đó có thể là dấu hiệu cảnh báo.

- So sánh logs hệ thống mới với logs bình thường
- Phát hiện người dùng bất thường trên website
- Phát hiện email lạ không giống với email từng gửi

📌 _Ví dụ_: Trong hệ thống SOC (Security Operation Center), cosine similarity giúp phát hiện hành vi truy cập khác biệt so với profile bình thường của người dùng.

---

#### **4.3. Tiền xử lý ảnh trong camera và học sâu (Image Preprocessing for Deep Learning)**

Trước khi ảnh được đưa vào mô hình học sâu, chúng cần được xử lý đúng cách:

- Resize về cùng kích thước
- Chuyển sang ảnh xám (grayscale) để giảm chiều dữ liệu
- Chuẩn hóa pixel để cải thiện hiệu quả học

Tất cả các bước trên đều có thể làm bằng Numpy nhanh chóng, không cần thêm thư viện phức tạp.

📌 _Ví dụ_: Trong hệ thống nhận diện khuôn mặt, ảnh từ camera được xử lý bằng Numpy trước khi đưa vào model học sâu để phân loại.

---

#### **4.4. Tăng tốc quy trình ETL với Numpy (Fast Computation in ETL Pipelines)**

ETL (Extract - Transform - Load) là quy trình nền tảng trong mọi hệ thống dữ liệu. Numpy giúp:

- Xử lý dữ liệu hàng triệu dòng trong vài giây
- Thực hiện tính toán hàng loạt như tổng hợp, lọc, chuyển định dạng
- Chuẩn hóa dữ liệu để đưa vào Data Warehouse hoặc mô hình AI
  
📌 _Ví dụ_: Một pipeline dữ liệu từ log server có thể dùng Numpy để tính toán lượng truy cập theo giờ, loại bỏ ngoại lệ và chuẩn hóa trước khi lưu vào hệ thống phân tích.


---


### **5. Tổng kết (Conclusion)**

Sau tuần đầu tiên của Module 2, chúng mình đã đi được một chặng đường rất nền tảng nhưng đầy thú vị. Từ những phép toán đơn giản với Numpy đến các ứng dụng thực tế như phân tích dữ liệu, xử lý ảnh, và đo độ tương đồng, chúng mình đã thật sự thấy được:

✅ **Numpy không chỉ là thư viện**, mà là công cụ giúp chúng ta **tư duy theo kiểu “dữ liệu lớn”** – nhanh, trực tiếp, tối ưu.

✅ **Đại số tuyến tính không chỉ là toán học lý thuyết**, mà là **ngôn ngữ chung** của mọi hệ thống AI hiện đại: từ vector hóa văn bản, nhân ma trận trong mạng neural, đến mô hình hóa dữ liệu người dùng.

✅ Các kỹ thuật như **cosine similarity**, **background subtraction**, hay **ETL pipeline bằng Numpy** đều không còn xa vời – chỉ cần hiểu rõ bản chất, chúng ta có thể áp dụng chúng vào công việc hằng ngày.

> 💡 Tuần học này giống như việc học cách “cầm cọ” trong hội họa. Dù còn đơn giản, nhưng nếu thành thạo, chúng mình đã có thể vẽ nên những bức tranh đầu tiên trong thế giới AI.