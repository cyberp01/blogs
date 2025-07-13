### **1. Giới thiệu (Introduction)**

Phân loại (**classification**) là một trong những bài toán nền tảng và phổ biến nhất trong lĩnh vực học máy (**Machine Learning**). Dù bạn đang xây dựng một hệ thống lọc thư rác, phân loại cảm xúc trên mạng xã hội, hay dự đoán kết quả trận đấu, thì việc đưa ra quyết định dựa trên dữ liệu đầu vào luôn là một yêu cầu cốt lõi.

Trong tuần học này của chương trình AIO2025, chúng mình đã cùng nhau tiếp cận một trong những phương pháp cổ điển nhưng hiệu quả nhất cho bài toán phân loại: **mô hình Naïve Bayes** (Naïve Bayes Classifier), xuất phát từ **định lý Bayes** (Bayes' Theorem) trong xác suất thống kê (**Probability and Statistics**). Thay vì chỉ học lý thuyết một cách trừu tượng, chúng mình được dẫn dắt từng bước: từ việc hiểu **xác suất tiên nghiệm** (prior probability), **xác suất có điều kiện** (conditional probability), đến ứng dụng định lý Bayes để đưa ra dự đoán dựa trên dữ liệu thực tế.

Điều thú vị là Naïve Bayes đặt ra một giả định tưởng chừng phi thực tế: các đặc trưng đầu vào là **độc lập điều kiện**(conditionally independent) với nhau. Nhưng chính sự "ngây thơ" này lại mang đến một mô hình dễ cài đặt, cực kỳ nhanh, và đáng ngạc nhiên là hiệu quả trong rất nhiều tình huống thực tế, đặc biệt là xử lý văn bản (**text processing**) hoặc khi dữ liệu huấn luyện không nhiều.

Thông qua các bài toán như "Play Tennis" (có nên chơi tennis hay không), phân tích dữ liệu giao thông nhiều lớp, và phân loại hoa Iris theo chiều dài cánh hoa, chúng mình không chỉ nắm rõ cách mô hình hoạt động, mà còn tự tay hiện thực thuật toán bằng NumPy, từ đó hiểu sâu sắc cách một hệ thống đưa ra quyết định dựa trên dữ liệu và xác suất.

Bài viết này sẽ tóm lược lại các kiến thức trọng tâm đã học, đồng thời đi sâu vào bản chất của mô hình Naïve Bayes, phân tích những điểm mạnh - điểm yếu, và đề xuất các hướng ứng dụng thực tiễn. Hy vọng chúng mình sẽ thấy rõ hơn vì sao một mô hình đơn giản như vậy vẫn được ưa chuộng trong thế giới học máy hiện đại.


---


### **2. Kiến thức trọng tâm (Key Concepts)**

#### 2.1 Xác suất cơ bản (Basic Probability)
Trước khi xây dựng bất kỳ mô hình học máy nào sử dụng xác suất, chúng mình cần hiểu rõ những khái niệm nền tảng sau:

##### 2.1.1 Biến cố (Event)

Là một kết quả hoặc một tập hợp kết quả có thể xảy ra của một phép thử ngẫu nhiên.  
**Ví dụ:** Khi tung một đồng xu, biến cố có thể là “xu ngửa”.

##### 2.1.2 Biến cố độc lập và độc lập có điều kiện (Independence & Conditional Independence)

Hai biến cố A và B được gọi là **độc lập** nếu việc xảy ra của A không ảnh hưởng gì đến khả năng xảy ra của B, và ngược lại:
$$
P(A \cap B) = P(A) \times P(B)
$$
Chúng được gọi là **độc lập có điều kiện** theo C nếu:
$$
P(A \cap B \mid C) = P(A \mid C) \times P(B \mid C)
$$

Trong mô hình Naïve Bayes, chúng mình giả định rằng các đặc trưng đầu vào là độc lập có điều kiện theo nhãn. Đây chính là lý do mô hình này có thể đơn giản hóa việc tính toán xác suất tổng hợp.

##### 2.1.3 Xác suất (Probability)

Là giá trị đo lường khả năng xảy ra của một biến cố, nằm trong khoảng từ 0 đến 1.
- $P(A) = 1$: Biến cố A chắc chắn xảy ra.
- $P(A) = 0$: Biến cố A chắc chắn không xảy ra.

##### 2.1.4 Xác suất tiên nghiệm (Prior Probability)

Là xác suất xảy ra của một biến cố trước khi có thêm thông tin mới.  
**Ví dụ:** Trong 100 email, có 20 email là spam. Khi đó:  

$$
P(\text{Spam}) = \frac{20}{100} = 0.2
$$

##### 2.1.5 Xác suất có điều kiện (Conditional Probability)

Là xác suất của A xảy ra, khi biết rằng B đã xảy ra. Ký hiệu:  
$$
P(A \mid B) = \frac{P(A \cap B)}{P(B)}
$$
**Ví dụ:** Nếu có 10 email chứa từ “free” và 6 trong số đó là spam:  
$$
P(\text{Spam} \mid \text{Free}) = \frac{6}{10} = 0.6
$$

##### 2.1.6 Xác suất đồng thời (Joint Probability)

Là xác suất đồng thời xảy ra của hai biến cố A và B:  
$$
P(A \cap B) = P(B \mid A) \times P(A)
$$

**Ví dụ:** Xét 100 email, trong đó có 20 email là spam và trong số đó có 6 email chứa từ “free”. Khi đó:  
$$
P(\text{Spam} \cap \text{Free}) = \frac{6}{100} = 0.06
$$
Hoặc có thể tính bằng:  
$$
P(\text{Spam} \cap \text{Free}) = P(\text{Free} \mid \text{Spam}) \times P(\text{Spam}) = \frac{6}{20} \times \frac{20}{100} = 0.06
$$

##### 2.1.7 Xác suất biên (Marginal Probability)

Là xác suất xảy ra của một biến cố, bất kể các biến cố khác. Nó có thể được tính bằng cách cộng qua các trường hợp B:  
$$
P(A) = \sum_B P(A \cap B)
$$
**Ví dụ:** Tính xác suất một email chứa từ “free” bất kể có phải spam hay không:  
$$
P(\text{Free}) = P(\text{Free} \cap \text{Spam}) + P(\text{Free} \cap \text{NotSpam})
$$
Giả sử trong 100 email:
- Có 6 email vừa spam vừa chứa “free”
- Có 4 email không phải spam nhưng cũng chứa “free”  
    Khi đó:  
$$
P(\text{Free}) = \frac{6 + 4}{100} = 0.1
$$

Tóm lại, những khái niệm này chính là nền móng để hiểu định lý Bayes và mô hình Naïve Bayes. Trong thực tế, nếu nắm chắc được các công thức và hiểu rõ ý nghĩa, chúng mình sẽ dễ dàng suy luận và áp dụng vào các bài toán phân loại.

---
#### 2.2. Định lý Bayes (Bayes' Theorem)

Định lý Bayes là công cụ cơ bản để cập nhật xác suất khi có thêm thông tin mới. Công thức của nó:
$$
P(A \mid B) = \frac{P(B \mid A) \times P(A)}{P(B)}
$$
Trong bối cảnh phân loại:
- A là nhãn cần dự đoán (vd: "Email = Spam"),
- B là tập hợp các đặc trưng quan sát được (vd: chứa từ "free")

Khi áp dụng định lý Bayes, chúng mình có thể dự đoán nhãn A cho một mẫu dữ liệu dựa trên việc tính xác suất hậu nghiệm (posterior probability) - tức xác suất nhãn A xảy ra khi đã biết B:
$$
P(A \mid B) \propto P(B \mid A) \times P(A)
$$

Trong Naïve Bayes, ta giả định rằng các đặc trưng trong B là độc lập, nhờ đó có thể viết:
$$
P(x_1, x_2, \ldots, x_n \mid A) = P(x_1 \mid A) \times P(x_2 \mid A) \times \cdots \times P(x_n \mid A)
$$

Từ đó, ta tính điểm số (score) cho mỗi nhãn và chọn nhãn có xác suất hậu nghiệm cao nhất.

---
#### 2.3. Mô hình Naïve Bayes (Naïve Bayes Model)

Naïve Bayes là một mô hình phân loại xác suất dựa trực tiếp trên định lý Bayes, với một giả định quan trọng: **các đặc trưng đầu vào độc lập với nhau có điều kiện theo nhãn**. Chính giả định "naïve" này giúp mô hình trở nên đơn giản, dễ huấn luyện, và có thể áp dụng hiệu quả với dữ liệu có nhiều chiều.

Công thức xác suất hậu nghiệm khi áp dụng giả định độc lập điều kiện:
$$
P(c \mid x_1, x_2, \ldots, x_n) \propto P(c) \times P(x_1 \mid c) \times P(x_2 \mid c) \times \cdots \times P(x_n \mid c)
$$

Trong đó:
- $c$ là một lớp (class)
- $xi$ là đặc trưng thứ $i$

Naïve Bayes hoạt động theo quy trình:
1. Tính xác suất tiên nghiệm của từng lớp: $P(c)$
2. Tính xác suất có điều kiện của mỗi đặc trưng với mỗi lớp: $P(xi|c)$
3. Nhân các xác suất này để tính điểm số cho mỗi lớp
4. Chọn lớp có điểm số cao nhất làm kết quả dự đoán

---

#### 2.4. Các biến thể của Naïve Bayes (Variants of Naïve Bayes)

Tùy vào loại dữ liệu đầu vào, Naïve Bayes có thể được triển khai dưới nhiều biến thể:

##### 2.4.1. Multinomial Naïve Bayes

- Áp dụng cho dữ liệu rời rạc, đặc biệt phù hợp với mô hình hóa văn bản (bag-of-words).
- $P(xi|c)$ được ước lượng dựa trên tần suất xuất hiện từ trong từng lớp.

##### 2.4.2. Bernoulli Naïve Bayes

- Cũng dùng cho văn bản nhưng với đặc trưng dạng nhị phân (từ có xuất hiện hay không).
- Hữu ích khi dữ liệu đầu vào là vector 0-1.

##### 2.4.3. Gaussian Naïve Bayes

- Áp dụng cho dữ liệu liên tục (như chiều dài, cân nặng, nhiệt độ...).
- Giả định mỗi đặc trưng $xi$ theo phân phối chuẩn (Gaussian) với từng lớp.
- $P(xi|c)$ được tính bằng công thức phân phối chuẩn theo mean và variance của từng lớp.

---

#### 2.5. Phân phối Gaussian (Gaussian Distribution)

Trong mô hình Naïve Bayes, khi đặc trưng đầu vào là dữ liệu liên tục (ví dụ: chiều cao, nhiệt độ, cân nặng...), chúng mình không thể tính xác suất $P(xi|c)$ bằng cách đếm tần suất như với dữ liệu rời rạc. Thay vào đó, mô hình **Gaussian Naïve Bayes** giả định rằng mỗi đặc trưng theo từng lớp sẽ phân bố theo một **phân phối chuẩn (Gaussian distribution)**. Đây là lý do vì sao phân phối Gaussian trở thành một phần quan trọng trong mô hình này.

![[Pasted image 20250713224839.png]]

##### 2.5.1 Đặc điểm

- Phân phối chuẩn (còn gọi là Gaussian distribution) là một kiểu phân phối xác suất rất phổ biến trong tự nhiên và thống kê. Dữ liệu phân bố theo dạng này thường có nhiều giá trị nằm gần trung bình, và số lượng giá trị giảm dần khi càng xa trung bình.
- Đồ thị có hình chuông, đối xứng qua trục trung tâm.
- Được xác định bởi hai tham số:    
    - Trung bình (mean) — ký hiệu: μ
    - Phương sai (variance) — ký hiệu: σ²

Ví dụ: chiều cao người trưởng thành thường phân bố theo phân phối chuẩn — số người có chiều cao trung bình chiếm phần lớn, còn rất thấp hoặc rất cao thì ít hơn.

##### 2.5.2 Công thức phân phối chuẩn

$$
P(x) = \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(x - \mu)^2}{2\sigma^2}}
$$

Trong đó:
- x là giá trị đặc trưng cần tính xác suất
- μ là trung bình của dữ liệu
- σ² là phương sai (độ biến thiên) của dữ liệu quanh trung bình

##### 2.5.3 Ý nghĩa trong học máy

- Khi đặc trưng đầu vào là dữ liệu liên tục (vd: chiều cao, nhiệt độ...), ta thường giả định nó phân bố theo Gaussian.
- Với mỗi lớp, mô hình sẽ tính riêng μ và σ² cho từng đặc trưng.
- Sau đó dùng công thức trên để ước lượng $P(x|class)$.


##### 2.5.4 Lưu ý về phân phối Gaussian

- Nếu dữ liệu không tuân theo phân phối chuẩn (ví dụ: thu nhập cá nhân thường lệch phải), việc áp dụng Gaussian có thể gây sai số.
- Trong các trường hợp đó, có thể cần biến đổi dữ liệu (log, z-score) hoặc dùng mô hình khác.

---

#### 2.6. Gaussian Naïve Bayes Classifier

Sau khi hiểu về phân phối chuẩn, chúng mình có thể áp dụng nó để xây dựng mô hình phân loại Gaussian Naïve Bayes cho dữ liệu liên tục. Đây là một biến thể của Naïve Bayes sử dụng phân phối Gaussian để ước lượng xác suất có điều kiện $P(xi|class)$.

##### 2.6.1 Cách hoạt động

- Với mỗi đặc trưng liên tục, mô hình sẽ:
    - Tách dữ liệu theo từng lớp (label)
    - Tính toán trung bình (μ) và phương sai (σ²) cho từng đặc trưng trong mỗi lớp
- Với một mẫu đầu vào mới, mô hình sẽ tính:
    - Xác suất của từng đặc trưng xi theo công thức phân phối chuẩn
    - Nhân các xác suất lại với xác suất tiên nghiệm của lớp
    - Chọn lớp có xác suất hậu nghiệm cao nhất
    
**Ví dụ minh họa:** Giả sử chúng mình có dữ liệu về chiều dài cánh hoa (petal length) để phân loại hoa Iris thành 2 loại: Setosa và Versicolor.

- Tập huấn luyện cho biết:
	- Với Setosa: chiều dài có trung bình μ = 1.5, phương sai σ² = 0.1
	- Với Versicolor: chiều dài có trung bình μ = 4.5, phương sai σ² = 0.2
- Mẫu mới có chiều dài cánh hoa là 1.6. Ta tính:
	- $P(1.6 | Setosa)$ theo công thức phân phối chuẩn
	- $P(1.6 | Versicolor)$ cũng theo công thức tương tự
- Nếu $P(1.6 | Setosa)$ lớn hơn hẳn, mô hình sẽ dự đoán mẫu thuộc lớp Setosa.

##### 2.6.2 Ví dụ ứng dụng

- Phân loại hoa Iris theo chiều dài cánh hoa
- Dự đoán bệnh dựa trên các chỉ số y tế như nhịp tim, huyết áp, nhiệt độ cơ thể


---


### **3. Phân tích nâng cao (Advanced Insights)**

Ở phần này, chúng mình sẽ cùng nhau nhìn lại mô hình Naïve Bayes một cách thực tế và dễ hiểu hơn: mô hình này có gì hay, có gì dở, và tại sao nó vẫn rất hữu ích trong nhiều tình huống.

#### 3.1. Vì sao Naïve Bayes vẫn hiệu quả dù giả định đơn giản?

Naïve Bayes giả định rằng các đặc trưng (features) là **độc lập có điều kiện** — tức là mỗi đặc trưng không ảnh hưởng đến đặc trưng khác, nếu đã biết nhãn (label). Điều này nghe có vẻ phi lý, vì trong thực tế, các đặc trưng thường có liên quan. Nhưng mô hình vẫn hoạt động khá tốt vì:

- **So sánh tương đối là đủ:** Mô hình không cần tính đúng xác suất tuyệt đối, chỉ cần tính điểm số cho mỗi lớp và chọn lớp cao nhất là được.  
    _Ví dụ:_ Khi phân loại email là spam hay không, dù mô hình không ước lượng chính xác $P(Spam|Email)$, chỉ cần điểm số của $Spam > Not Spam$ là đã có thể đưa ra quyết định đúng.
- **Lỗi nhỏ không ảnh hưởng nhiều:** Dù xác suất bị ước lượng sai, nếu sai lệch tương tự giữa các lớp thì mô hình vẫn đưa ra kết quả đúng.  
    _Ví dụ:_ Nếu từ "free" và "win" cùng tăng xác suất cho cả hai lớp, nhưng tăng nhiều hơn ở lớp Spam, thì Spam vẫn được chọn.
- **Không cần thuật toán phức tạp:** Mô hình chỉ dùng các phép đếm và nhân, không cần huấn luyện bằng gradient hay thuật toán tối ưu.  
     _Ví dụ:_ Với dữ liệu 100 email, chỉ cần đếm có bao nhiêu email spam chứa từ "discount" là đủ để tính xác suất.

#### 3.2. Ưu điểm của Naïve Bayes

- **Nhanh và đơn giản:** Thời gian huấn luyện nhanh, dễ triển khai bằng vài dòng code.
- **Tốt cho dữ liệu văn bản:** Hoạt động rất tốt trong các bài toán như phân loại email, lọc bình luận độc hại, phân tích cảm xúc.  
    _Ví dụ:_ Spam filter trong Gmail từng dùng Naïve Bayes.
- **Chạy tốt với dữ liệu nhỏ:** Không cần tập huấn luyện lớn.
- **Ít bị ảnh hưởng bởi dữ liệu nhiễu nhỏ hoặc thiếu giá trị.**

#### 3.3. Hạn chế của Naïve Bayes

- **Giả định độc lập thường không đúng:** Nhiều đặc trưng liên quan chặt chẽ với nhau.  
    _Ví dụ:_ Trong bài toán dự đoán bệnh, hai đặc trưng “ho” và “sốt” thường đi kèm nhau. Naïve Bayes lại xem chúng độc lập, dẫn đến tính sai xác suất.
- **Không nắm được mối quan hệ phức tạp:** Mô hình không học được tương tác giữa các đặc trưng như mô hình phức tạp hơn (Random Forest, Neural Network...).
- **Với dữ liệu liên tục, phân phối Gaussian có thể không phù hợp:**  
    _Ví dụ:_ Dữ liệu thu nhập cá nhân có thể lệch phải (không chuẩn), mô hình sẽ ước lượng sai nếu dùng Gaussian Naïve Bayes.

Dù có những hạn chế, Naïve Bayes vẫn rất hữu ích khi chúng mình cần một mô hình đơn giản, nhanh và dễ giải thích, đặc biệt trong các hệ thống phân loại tự động như kiểm duyệt nội dung, phân loại văn bản, hoặc dự báo nhanh theo luật. trong nhiều hệ thống thực tế khi cần phân loại nhanh và dễ kiểm soát.


---


### **4. Ứng dụng thực tiễn (Practical Applications)**

Sau khi hiểu mô hình Naïve Bayes vận hành như thế nào, chúng mình hãy cùng khám phá các tình huống thực tế mà mô hình này được áp dụng rộng rãi.

#### 4.1. Ứng dụng điển hình

|Bài toán|Mô tả|Biến thể phù hợp|
|---|---|---|
|**Lọc thư rác**|Phân loại email là spam hay không|Multinomial / Bernoulli|
|**Phân tích cảm xúc**|Xác định cảm xúc tích cực/tiêu cực từ văn bản đánh giá|Multinomial|
|**Dự đoán bệnh từ chỉ số y tế**|Phân loại bệnh nhân dựa trên chỉ số sinh học|Gaussian|
|**Phân loại hoa Iris**|Xác định loài hoa từ chiều dài cánh hoa|Gaussian|
|**Nhận diện ngôn ngữ**|Dự đoán một đoạn văn bản thuộc ngôn ngữ nào|Multinomial|

---

#### **4.2. Tình huống thực tế: Phát hiện hành vi bất thường trong hệ thống IT (Anomaly Detection)**

Một ứng dụng quan trọng của Gaussian Naïve Bayes là trong lĩnh vực **an toàn thông tin**, cụ thể là bài toán **phát hiện hành vi bất thường** trong hệ thống CNTT.

 **Bài toán**  

Dự đoán xem một hành vi của người dùng (user behavior) có phải là bất thường (anomalous) hay không, dựa trên các đặc trưng định lượng như:
- Thời gian đăng nhập
- Khoảng cách giữa các lần tương tác (idle time)
- Số lượng file được truy cập
- Dung lượng dữ liệu truyền tải trong một phiên làm việc

**Cách giải quyết**

- Vì các đặc trưng trên là dữ liệu liên tục, mô hình Gaussian Naïve Bayes rất phù hợp.
- Với mỗi lớp (bình thường / bất thường), ta tính trung bình (μ) và phương sai (σ²) cho từng đặc trưng.
- Sau đó, với một hành vi mới, mô hình sẽ tính xác suất xuất hiện của hành vi đó trong mỗi lớp và chọn lớp có xác suất hậu nghiệm cao hơn.

**Ví dụ**

- Một người dùng thường đăng nhập từ 8h–17h và truy cập khoảng 20 file/ngày.
- Một phiên truy cập mới diễn ra lúc 2h sáng, truy cập hơn 200 file và upload dữ liệu lớn.
- Gaussian NB có thể đánh giá xác suất rất thấp với mẫu này trong lớp “bình thường” → đánh dấu là “bất thường”.

 **Ý nghĩa thực tiễn**

- Có thể ứng dụng để cảnh báo sớm trong hệ thống SOC (Security Operation Center)
- Giúp phát hiện tấn công nội gián, hành vi giả mạo hoặc phần mềm độc hại hoạt động lén lút trong hệ thống.


---

### **5.  Tổng kết (Conclusion)**

Qua các kiến thức đã được học ở tuần thứ 2 của module 2 trong chương trình AIO2025, chúng mình đã cùng nhau tìm hiểu cách mà mô hình Naïve Bayes hoạt động từ nền tảng lý thuyết xác suất, định lý Bayes cho đến các biến thể thực tế như Gaussian Naïve Bayes. Bằng cách giả định rằng các đặc trưng là độc lập có điều kiện, mô hình có thể đơn giản hóa việc tính toán mà vẫn mang lại hiệu quả đáng kể trong nhiều bài toán phân loại.

Không chỉ vậy, chúng mình còn được thực hành trực tiếp các bài toán như Play Tennis, Traffic Classification và đặc biệt là phát hiện hành vi bất thường trong hệ thống an toàn thông tin — một ví dụ rất gần với ứng dụng thực tế trong doanh nghiệp hiện nay.

Dù còn nhiều hạn chế, Naïve Bayes là một mô hình lý tưởng để bắt đầu học máy: dễ hiểu, dễ cài đặt, dễ giải thích và có giá trị thực tế rõ ràng. Hiểu tốt mô hình này cũng là nền tảng quan trọng để tiếp cận các thuật toán phức tạp hơn sau này.

Hy vọng sau bài viết này, bạn đã có một cái nhìn toàn diện và tự tin hơn khi áp dụng Naïve Bayes vào các bài toán của riêng mình. không chỉ giúp bạn giải quyết tốt các bài toán phân loại đơn giản mà còn là nền tảng để hiểu sâu hơn các khái niệm như xác suất, suy luận Bayes và các mô hình thống kê hiện đại hơn sau này. khi chúng mình cần một mô hình đơn giản, nhanh và dễ giải thích, đặc biệt trong các hệ thống phân loại tự động như kiểm duyệt nội dung, phân loại văn bản, hoặc dự báo nhanh theo luật. trong nhiều hệ thống thực tế khi cần phân loại nhanh và dễ kiểm soát.