
### **1. Giới thiệu**

Trong hành trình học về Trí tuệ nhân tạo (AI – _Artificial Intelligence_), chắc hẳn ai trong chúng mình cũng từng nghe tới những khái niệm như “mean”, “variance”, hay “correlation”. Nhưng nếu chỉ học thuật ngữ mà không hiểu sâu bản chất và cách ứng dụng của chúng, thì những khái niệm ấy sẽ chỉ dừng lại ở mức… mơ hồ.

Tuần này, chúng mình đã được tiếp cận với một phần cực kỳ quan trọng của AI: **thống kê cơ bản** (_basic statistics_) và **cách nó được ứng dụng trực tiếp vào xử lý dữ liệu, đặc biệt là xử lý ảnh**. Đây là một nền tảng giúp chúng ta hiểu được cách dữ liệu vận hành, cách các mô hình học được thông tin, và làm sao để đưa ra những dự đoán chính xác hơn.

Từ những khái niệm cơ bản như **mean** (_giá trị trung bình_), **median** (_trung vị_), hay **variance** (_phương sai_), cho đến những kỹ thuật cao hơn như **PDF** (_hàm mật độ xác suất_), **histogram equalization** (_cân bằng biểu đồ tần suất_), và **correlation coefficient** (_hệ số tương quan_) – tất cả đều là những viên gạch đầu tiên xây nên tư duy phân tích dữ liệu trong AI.

Không chỉ dừng lại ở lý thuyết, buổi học còn dẫn chúng mình qua những ví dụ cực kỳ thực tế: từ việc làm mờ và khử nhiễu ảnh, tăng cường độ tương phản ảnh trắng đen, đến việc dùng hệ số tương quan để phát hiện vật thể trong ảnh.

Nhìn lại, chúng mình nhận ra: **thống kê không chỉ là những công thức khô khan**, mà chính là **ngôn ngữ mô tả thế giới bằng dữ liệu**, và là nền tảng cho mọi mô hình học máy.

Hãy cùng nhau đi tiếp qua từng phần của blog để khám phá kỹ hơn những kiến thức hấp dẫn này nhé!


---


### **2. Kiến thức trọng tâm**

#### **2.1. Thống kê mô tả cơ bản (Basic Descriptive Statistics)**

Khi chúng mình bắt đầu làm việc với dữ liệu, việc đầu tiên cần làm là **tóm tắt dữ liệu một cách gọn gàng và có ý nghĩa**. Đó chính là lúc các chỉ số thống kê mô tả như **mean** (_trung bình_), **median** (_trung vị_), **variance** (_phương sai_) và **standard deviation** (_độ lệch chuẩn_) phát huy sức mạnh.

##### 2.1.1 **Mean – Giá trị trung bình**

Mean là một chỉ số quen thuộc, được tính bằng tổng các giá trị chia cho số lượng phần tử. Trong thống kê, mean giúp chúng ta biết trung tâm của tập dữ liệu nằm ở đâu.

Ví dụ, dãy số $X = {2, 4, 5, 8, 1, 4}$ có mean là:
$$
\mu = \frac{2 + 4 + 5 + 8 + 1 + 4}{6} = 4
$$

Điều thú vị là mean không chỉ dùng để “tính điểm trung bình”. Trong AI, chúng mình còn dùng mean để **làm mờ ảnh** bằng cách lấy trung bình của các điểm ảnh lân cận, hoặc làm **convolution kernel** khi xử lý ảnh.

##### 2.1.2 **Expected Value – Giá trị kỳ vọng**

Khác với mean là giá trị sau khi có dữ liệu thực tế, **expected value** là giá trị **chúng ta kỳ vọng nhận được** trước khi quan sát.

Ví dụ: Trong một trò chơi, nếu mỗi lượt bạn có xác suất thắng $1 là 0.7 và thua $1 là 0.3, thì giá trị kỳ vọng là:
$$
E(X) = 0.7 \times 1 + 0.3 \times (-1) = 0.4
$$
=> Trung bình mỗi lượt chơi, bạn sẽ **kiếm được $0.4**, nếu chơi nhiều lần. Đây chính là sức mạnh của giá trị kỳ vọng trong việc **dự đoán kết quả trước khi thu thập dữ liệu**.

##### 2.1.3 **Median – Trung vị**

Median là giá trị ở giữa của tập dữ liệu sau khi đã được sắp xếp. Khi dữ liệu bị lệch hoặc có giá trị ngoại lai (outlier), **median thường đại diện tốt hơn mean**.

Ví dụ: Với dãy số $X = {1, 2, 4, 5, 8}$, median là số ở vị trí thứ 3 (sau khi sắp xếp): **4**

Nếu số lượng phần tử là chẵn, median được tính bằng trung bình hai số ở giữa.

Ứng dụng của median đặc biệt mạnh mẽ trong **khử nhiễu ảnh (image denoising)**, vì median ít bị ảnh hưởng bởi các điểm ảnh “nhiễu” bất thường.

##### 2.1.4 **Variance – Phương sai và Standard Deviation – Độ lệch chuẩn**
  
Trong khi mean cho biết dữ liệu tập trung ở đâu, **variance và standard deviation lại cho biết dữ liệu phân tán thế nào** quanh mean.
- **Variance** là trung bình của bình phương khoảng cách từ từng điểm tới mean.
- **Standard deviation (σ)** là căn bậc hai của variance, giúp chúng mình dễ hiểu hơn vì đơn vị giống dữ liệu ban đầu.

Ví dụ: Với $X = {5, 3, 6, 7, 4}$
Mean = $5$
Variance = $2$
Standard deviation = $√2 ≈ 1.41$

Trong xử lý ảnh, chúng mình có thể **tính độ lệch chuẩn cục bộ** để phát hiện **vùng có texture – chi tiết cao**, rất hữu ích trong bài toán phân đoạn ảnh hoặc trích xuất đặc trưng.

---
  
#### **2.2. Phân phối xác suất (Probability Distribution)**

Khi chúng mình đã nắm được các chỉ số cơ bản như trung bình và phương sai, bước tiếp theo là tìm hiểu xem **dữ liệu có xu hướng xuất hiện như thế nào** – đó chính là lúc chúng ta học đến các khái niệm về **phân phối xác suất**.

Trong tuần học này, chúng mình được giới thiệu ba công cụ cốt lõi: PMF, PDF và CDF

##### 2.2.1 **PMF – Hàm khối xác suất (Probability Mass Function)**

PMF dùng cho các biến rời rạc (_discrete variables_), như kết quả gieo xúc xắc hoặc số học sinh thích học toán.

PMF cho biết xác suất mà một giá trị cụ thể sẽ xảy ra. Ví dụ:

- Với một xúc xắc cân đối:
    $P(X = 1) = P(X = 2) = … = P(X = 6) = \frac{1}{6}$

PMF giúp trả lời các câu hỏi như: “Xác suất học sinh được điểm 10 là bao nhiêu?” hoặc “Có bao nhiêu người chọn A trong khảo sát?”

##### 2.2.2 **PDF – Hàm mật độ xác suất (Probability Density Function)**  

PDF được dùng với biến liên tục (_continuous variables_), như chiều cao, cân nặng, điểm thi.

PDF không cho ta xác suất tại một điểm cụ thể (vì xác suất tại một điểm = 0), mà cho biết **mật độ xác suất** tại một vùng. Để tính xác suất thật sự, chúng ta cần tính diện tích dưới đường cong PDF trong một khoảng.

Ví dụ điển hình là **phân phối chuẩn (normal distribution)** – hình chuông mà chúng mình hay thấy trong đồ thị điểm thi. Một nguyên tắc nổi tiếng gọi là **quy tắc 68-95-99.7**:
- 68% dữ liệu nằm trong 1 độ lệch chuẩn từ mean
- 95% trong 2 độ lệch chuẩn
- 99.7% trong 3 độ lệch chuẩn

![[Pasted image 20250722112249.png]]

##### 2.2.3 **CDF – Hàm phân phối tích lũy (Cumulative Distribution Function)**

CDF cho biết **xác suất mà biến ngẫu nhiên X nhỏ hơn hoặc bằng một giá trị x cụ thể**.

Ví dụ:
- Với xúc xắc:
    $P(X \leq 3) = P(1) + P(2) + P(3) = \frac{3}{6} = 0.5$

Trong xử lý ảnh, chúng mình dùng CDF để xây dựng **histogram cumulative** – bước quan trọng trong kỹ thuật tăng độ tương phản bằng **Histogram Equalization**.

Nắm được PMF, PDF, và CDF là nền tảng để hiểu xác suất, mô hình hóa dữ liệu, và tính toán phân phối đầu ra trong các mô hình AI – từ phân loại đến sinh dữ liệu (generative models).

---

#### **2.3. Histogram và Histogram Equalization**

Sau khi hiểu về các khái niệm xác suất, nhóm mình được làm quen với một công cụ cực kỳ trực quan giúp mô tả cách phân bố dữ liệu – đó là **Histogram (biểu đồ tần suất)**.

##### 2.3.1 **Histogram – Biểu đồ tần suất**

Histogram là một cách biểu diễn số lượng (hoặc tần suất) các giá trị rơi vào từng khoảng (bin). Trong xử lý ảnh, histogram thường dùng để thể hiện **phân bố độ sáng (intensity)** của các pixel trong ảnh grayscale (_ảnh mức xám_).

Ví dụ:
- Nếu một ảnh có nhiều vùng tối, histogram sẽ tập trung nhiều ở phía bên trái.
- Nếu ảnh sáng đều, histogram sẽ trải đều từ trái sang phải.

Histogram rất hữu ích khi chúng mình muốn biết ảnh đang tối quá, sáng quá, hay bị mất chi tiết ở vùng nào.

Có 3 loại histogram được nhắc đến:
- **Frequency Histogram** (_biểu đồ tần suất_): đếm số pixel ở mỗi mức sáng.
- **Density Histogram** (_biểu đồ mật độ_): chuẩn hóa tần suất bằng tổng số pixel.
- **Cumulative Histogram** (_biểu đồ tích lũy_): cộng dồn tần suất từ mức sáng thấp đến cao.

![[Pasted image 20250722112506.png]]

##### 2.3.2 **Histogram Equalization – Cân bằng biểu đồ tần suất**

Đây là một kỹ thuật mạnh mẽ dùng để **tăng độ tương phản của ảnh**, đặc biệt là các ảnh bị tối hoặc có ánh sáng không đều.

Ý tưởng chính:
- Nếu histogram của ảnh chỉ tập trung ở một vùng (ví dụ: chỉ toàn vùng xám tối), thì ảnh sẽ trông “nhạt nhòa”.
- Histogram Equalization sẽ **kéo giãn** phân bố này sao cho đều hơn, tức là gần với **uniform distribution** (phân phối đồng đều).

Cách thực hiện:
1. Tính histogram và CDF của ảnh gốc.
2. Ánh xạ giá trị pixel cũ sang giá trị mới dựa trên CDF.
3. Kết quả là ảnh có độ tương phản cao hơn, dễ nhìn hơn.

![[Pasted image 20250722112650.png]]

Chúng mình còn được thực hành từng bước bằng tay: từ tính PMF, CDF, rồi cập nhật lại từng giá trị pixel theo công thức ánh xạ. Điều đó giúp hiểu sâu bản chất của thuật toán chứ không chỉ dùng thư viện `cv2.equalizeHist()`.

##### 2.3.3 **Ứng dụng**

- Cải thiện ảnh chụp trong điều kiện ánh sáng yếu.
- Tiền xử lý ảnh đầu vào cho các thuật toán AI, giúp nhận diện tốt hơn.
- Tăng độ phân biệt của chi tiết trong ảnh y tế, vệ tinh hoặc camera an ninh.

---
  
#### **2.4. Covariance (Hiệp phương sai) và Correlation (Tương quan)**

Khi làm việc với hai biến số, điều quan trọng là phải biết: **chúng có đang thay đổi cùng chiều không? Có mối quan hệ gì với nhau không?** Đó chính là lúc **covariance (hiệp phương sai)** và **correlation coefficient (hệ số tương quan)** phát huy tác dụng.

##### 2.4.1 **Covariance – Hiệp phương sai**

Covariance cho biết **hai biến số có xu hướng biến động cùng chiều hay ngược chiều với nhau**.
- Nếu covariance > 0 → hai biến thường **tăng/giảm cùng nhau** (xu hướng thuận).
- Nếu covariance < 0 → hai biến thường **tăng/giảm ngược nhau** (xu hướng nghịch).
- Nếu covariance ≈ 0 → gần như **không có xu hướng rõ ràng**.

Ví dụ cực kỳ trực quan mà thầy đưa ra là số lượng **táo xanh và táo đỏ** ở các siêu thị. Khi một nơi có nhiều táo xanh thì cũng thường có nhiều táo đỏ → covariance dương.

Tuy nhiên, covariance **khó diễn giải** vì nó phụ thuộc vào đơn vị đo của dữ liệu (scale-sensitive). Ví dụ: nếu ta đổi đơn vị từ kg sang g, giá trị covariance sẽ thay đổi lớn dù bản chất mối quan hệ không đổi.

##### 2.4.2 **Correlation Coefficient – Hệ số tương quan**

Để khắc phục nhược điểm đó, chúng mình dùng **hệ số tương quan (correlation coefficient)** – thường ký hiệu là **r** hoặc **ρ (rho)**.

Công thức:
$$
\rho_{X,Y} = \frac{Cov(X, Y)}{\sigma_X \cdot \sigma_Y}
$$

Trong đó:
- Cov(X, Y) là hiệp phương sai giữa X và Y
- σ là độ lệch chuẩn

Ưu điểm của hệ số tương quan:
- Luôn nằm trong khoảng **$[-1, 1]$**
- **Không phụ thuộc vào đơn vị đo**
- Giúp dễ dàng so sánh mức độ tương quan giữa nhiều cặp biến

Ý nghĩa:
- **r = 1**: tương quan thuận hoàn hảo (perfect positive correlation)
- **r = -1**: tương quan nghịch hoàn hảo (perfect negative correlation)
- **r = 0**: không có tương quan tuyến tính

![[Pasted image 20250720211751.png]]

Chúng mình còn học được rằng: **correlation không đồng nghĩa với causation (quan hệ nhân quả)**. Hai biến có thể liên quan mà không phải do cái này gây ra cái kia – ví dụ: số kem bán ra và số người đi bơi tăng cùng mùa hè, nhưng một cái không gây ra cái kia.

##### 2.4.3 **Ứng dụng**

- Trong **AI xử lý ảnh**, hệ số tương quan được dùng để **tìm mẫu giống nhau (template matching)**.
- Trong phân tích dữ liệu: kiểm tra mối quan hệ giữa các đặc trưng (feature) để chọn lựa biến quan trọng.
- Trong tài chính: đánh giá mối quan hệ giữa cổ phiếu, tài sản.


---


### **3. Phân tích nâng cao (Advanced Insights)**

Sau khi nắm được các khái niệm thống kê cơ bản, tuần này chúng mình còn được đào sâu vào **những khác biệt tinh tế nhưng quan trọng** giữa các chỉ số, cũng như các **nguyên lý toán học phía sau** giúp hiểu rõ hơn cách hoạt động của thống kê trong AI.

#### **3.1 Mean vs. Expected Value – Khác nhau giữa Trung bình và Giá trị kỳ vọng**

Thoạt nhìn, **mean** và **expected value** đều là “trung bình”, nhưng điểm khác biệt nằm ở **bối cảnh sử dụng**:

- **Mean (trung bình)** được tính **sau khi đã có dữ liệu**, thường dùng để mô tả dữ liệu thực tế đã thu thập được.
- **Expected value (giá trị kỳ vọng)** là giá trị trung bình **kỳ vọng sẽ xảy ra** dựa trên xác suất, trước khi thu thập dữ liệu.

Ví dụ:
- Mean: Trung bình điểm kiểm tra của lớp sau khi chấm xong.
- Expected value: Kỳ vọng mỗi lượt chơi một game sẽ thắng bao nhiêu tiền, dựa trên xác suất.

Trong các mô hình AI như reinforcement learning, expected value được dùng để tính **giá trị kỳ vọng của hành động (expected reward)** – yếu tố cốt lõi để ra quyết định tối ưu.

---

#### **3.2 Vì sao khi tính phương sai mẫu lại chia cho (n - 1)? – Hiểu về Bậc Tự Do (Degrees of Freedom)**
  

Một câu hỏi “kinh điển” trong thống kê: **Tại sao tính phương sai mẫu lại chia cho (n - 1), chứ không phải n?**

Câu trả lời nằm ở khái niệm **“bậc tự do” (degrees of freedom)**. Khi tính **mean mẫu**, ta đã “mất” đi một bậc tự do vì tổng các giá trị bị ràng buộc (đã dùng để tính mean). Do đó, chỉ còn **n - 1 giá trị là độc lập** để ước lượng phương sai.

Điều này giúp:
- Tránh **đánh giá thấp** độ phân tán của dữ liệu mẫu so với tổng thể.
- Tạo ra **ước lượng không chệch (unbiased estimator)** cho phương sai tổng thể.

Hiểu đúng về degrees of freedom rất quan trọng khi thiết kế mô hình thống kê, từ hồi quy tuyến tính đến PCA.

---

#### **3.3 Covariance khó hiểu, Correlation dễ diễn giải hơn**

Chúng mình nhận thấy một sự thật: **Covariance tuy là nền tảng**, nhưng lại **khó diễn giải vì phụ thuộc vào scale (đơn vị đo)**.

Ví dụ: Cùng một mối quan hệ giữa số giờ học và điểm thi, nếu đổi từ giờ sang phút thì covariance sẽ thay đổi đáng kể.

Trong khi đó:
- **Correlation coefficient** luôn nằm trong $[-1, 1]$, giúp **dễ đọc, dễ so sánh**.
- Không bị ảnh hưởng bởi phép biến đổi tuyến tính như nhân/chia hoặc cộng/trừ.


Điều thú vị là correlation coefficient còn được dùng trong các kỹ thuật cao hơn như:
- **Template Matching** trong xử lý ảnh
- **Principal Component Analysis (PCA)** trong giảm chiều dữ liệu
- **Phân tích tài chính** và các mạng học sâu (_deep learning_)


---


### **4. Ứng dụng thực tiễn (Practical Applications)**

Một trong những điểm đặc biệt của tuần học này là: **chúng mình không chỉ học lý thuyết**, mà còn được **trải nghiệm trực tiếp cách thống kê được “gài cắm” trong các bài toán AI thực tế**. Dưới đây là những ứng dụng nổi bật mà chúng mình thấy thực sự thú vị

#### **4.1. Làm mờ ảnh bằng Mean Filter**

Trong xử lý ảnh (_image processing_), làm mờ ảnh giúp loại bỏ chi tiết nhỏ hoặc nhiễu bằng cách làm trung bình giá trị của các điểm ảnh lân cận. Đây chính là **ứng dụng trực tiếp của mean (trung bình)**.

Cách làm:
- Dùng một ma trận nhỏ gọi là **kernel** (ví dụ 3×3 hoặc 5×5)
- Lướt kernel qua từng vị trí trong ảnh, tính trung bình → giá trị mới

![[1_Ra4DG6PT0hxnvH2aW2OUKw.gif]]

Dùng thư viện:

```python
cv2.filter2D(input_image, -1, kernel)
```

Ứng dụng:
- Làm mượt ảnh trước khi phát hiện cạnh
- Làm đẹp hình ảnh chân dung trong camera

---

#### **4.2. Khử nhiễu ảnh bằng Median Filter**

Khi ảnh bị nhiễu kiểu “muối tiêu” – xuất hiện các chấm trắng đen rải rác – dùng **median (trung vị)** để thay thế pixel bằng giá trị trung vị của lân cận sẽ hiệu quả hơn là dùng mean.

![[Pasted image 20250716210615.png]]

Ưu điểm:
- Không bị ảnh hưởng bởi outlier (giá trị quá cao hoặc quá thấp)
- Giữ được viền và chi tiết tốt hơn

Đây là một ví dụ điển hình cho việc lựa chọn đúng công cụ thống kê phù hợp với loại dữ liệu.

---

#### **4.3. Tăng cường độ tương phản ảnh bằng Histogram Equalization**

Khi ảnh bị thiếu sáng hoặc vùng tối quá nhiều, ta có thể dùng kỹ thuật **Histogram Equalization** để “trải đều” độ sáng, giúp ảnh nhìn rõ và chi tiết hơn.

![[Pasted image 20250716223905.png]]

Về bản chất:
- Tính **PDF**, **CDF** của histogram ảnh
- Ánh xạ lại từng pixel theo CDF
- Kết quả: histogram phân bố đều hơn

Ứng dụng:
- Ảnh chụp trong điều kiện thiếu sáng
- Ảnh X-quang, ảnh y tế
- Tiền xử lý ảnh đầu vào cho AI

---

#### **4.4. Phát hiện vật thể bằng Template Matching và Correlation**

Chúng mình cũng được học cách dùng **hệ số tương quan (correlation coefficient)** để **so sánh mức độ giống nhau giữa ảnh gốc và một mẫu nhỏ (template)**.

![[Pasted image 20250720212836.png]]

Ứng dụng:
- Xác định vị trí một biểu tượng trong ảnh lớn
- Phát hiện logo, dấu hiệu trong camera
- Áp dụng trong robot thị giác (computer vision)

Dùng OpenCV:

```python
cv2.matchTemplate(image, template, cv2.TM_CCOEFF_NORMED)
```

 Hệ số ρ càng gần 1 → ảnh mẫu càng giống khu vực ảnh lớn → xác định vị trí vật thể.

---

#### **4.5. Phân tích mối quan hệ dữ liệu bằng Correlation**

Ngoài xử lý ảnh, hệ số tương quan còn được dùng rộng rãi trong phân tích dữ liệu:

- Xác định các đặc trưng có liên quan trong học máy
- Giảm chiều dữ liệu (PCA – Principal Component Analysis)
- Dự đoán xu hướng trong tài chính (cổ phiếu A có tương quan với B không?)

Tóm lại, những kiến thức thống kê mà chúng mình học được trong tuần này **không hề khô khan** mà thực sự là **xương sống cho rất nhiều ứng dụng trong AI, khoa học dữ liệu và xử lý ảnh**.

  
---


### **5. Tổng kết**

Tuần này, nhóm chúng mình đã có một chuyến hành trình rất đáng nhớ vào thế giới của **thống kê cơ bản** – nơi mà các khái niệm tưởng như “khó nhằn” như mean, variance hay correlation lại trở nên **rất gần gũi và dễ hình dung** thông qua các ứng dụng thực tế trong AI.

Chúng mình không chỉ dừng lại ở việc học công thức, mà còn hiểu sâu:
- **Mean** không chỉ là “trung bình”, mà còn giúp làm mờ ảnh.
- **Median** không chỉ để tính giữa dãy số, mà còn chống nhiễu cực hiệu quả.
- **Variance** cho thấy độ “rối” của dữ liệu – từ phân tích ảnh đến đo độ chênh lệch.
- **PMF, PDF, CDF** giúp chúng mình mô hình hóa xác suất – nền tảng cho mọi mô hình học máy.
- **Histogram Equalization** là một minh chứng tuyệt vời cho việc “điều chỉnh dữ liệu” để AI xử lý tốt hơn.
- Và đặc biệt, **Correlation Coefficient** không chỉ là một con số, mà là chìa khóa để so sánh, phát hiện và thấu hiểu mối quan hệ giữa các biến.

🎯 Từ những viên gạch thống kê cơ bản, chúng mình thấy rõ rằng: **AI không thể xây dựng hiệu quả nếu thiếu nền tảng toán học vững chắc.** Và thống kê chính là “ngôn ngữ gốc” để AI hiểu thế giới.

Hy vọng blog tuần này không chỉ giúp các bạn nắm được kiến thức, mà còn khơi gợi cảm hứng để tiếp tục khám phá sâu hơn vào thế giới dữ liệu và trí tuệ nhân tạo.