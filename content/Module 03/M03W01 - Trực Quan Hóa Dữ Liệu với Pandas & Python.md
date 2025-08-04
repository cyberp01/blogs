### **1. Giới thiệu**

#### **1.1. Tại sao trực quan hóa dữ liệu (data visualization) lại quan trọng?**

**Trực quan hóa dữ liệu là quá trình chuyển đổi thông tin thành ngữ cảnh trực quan**, chẳng hạn như bản đồ hoặc biểu đồ, nhằm giúp bộ não con người dễ dàng hiểu và rút ra những hiểu biết sâu sắc từ dữ liệu hơn. Nó **chuyển đổi các tập dữ liệu phức tạp thành các định dạng trực quan dễ hiểu hơn**.

Đối với bất kỳ tổ chức nào hoạt động dựa trên dữ liệu, trực quan hóa dữ liệu là một **công cụ thiết yếu**, cho phép người dùng **nắm bắt các tập dữ liệu phức tạp và truyền đạt thông tin chuyên sâu một cách hiệu quả** tới các bên liên quan.

---

#### **1.2. Mục tiêu học tập trong tuần**

Trong tuần này, chúng ta sẽ khám phá tầm quan trọng của trực quan hóa dữ liệu và cách áp dụng nó vào các tập dữ liệu thực tế. Các mục tiêu chính bao gồm:

- Hiểu các khái niệm cơ bản về trực quan hóa dữ liệu và vai trò của nó.
- Làm quen với cấu trúc dữ liệu cơ bản trong Pandas như Series và DataFrame, cùng các thao tác xử lý dữ liệu.
- Học cách tạo các loại biểu đồ phổ biến bằng các thư viện Python mạnh mẽ như Matplotlib, Seaborn và Plotly.
- Vận dụng kiến thức vào các nghiên cứu điển hình thực tế để phân tích và rút ra thông tin chi tiết.
- Nắm vững các nguyên tắc để lựa chọn biểu đồ phù hợp cho từng mục đích phân tích và đối tượng người dùng.


---


### **2. Kiến thức trọng tâm**

#### **2.1. Tổng quan về trực quan hóa dữ liệu**

Trực quan hóa dữ liệu là việc **thay đổi các tập dữ liệu phức tạp thành các định dạng trực quan dễ hiểu hơn**. Các hình thức trực quan hóa dữ liệu có thể rất đa dạng và sử dụng nhiều loại dữ liệu khác nhau. Các thư viện Python phổ biến cho trực quan hóa dữ liệu bao gồm:

- **Matplotlib**: Cung cấp khả năng tùy chỉnh rộng rãi nhưng yêu cầu nhiều mã hơn.
- **Seaborn**: Đơn giản hóa các biểu đồ thống kê với các chủ đề tích hợp.
- **Plotly**: Xuất sắc trong việc tạo ra các hình ảnh trực quan động và tương tác.

---

#### **2.2. Làm quen với Pandas Series và DataFrame**

**Pandas Series**: Là một mảng 1 chiều có thể chứa bất kỳ kiểu dữ liệu nào (số nguyên, chuỗi, số thực, đối tượng Python, v.v.).

- **Tạo và truy cập**: Có thể tạo Series và truy cập các hàng bằng cách sử dụng chỉ số vị trí (ví dụ: `data`) hoặc nhãn (ví dụ: `data.loc[2:3]`, `data['C':'P']`).
- **Thao tác hàng**: Bao gồm xóa hàng bằng cách sử dụng nhãn hoặc chỉ số vị trí (`data.drop('C')`, `data.drop(2)`), và chèn hàng (`data['K'] = 'Kotlin '`, `data[2.5] = 9`).
- **Hàm phổ biến**: Pandas Series cung cấp các hàm như `min()`, `max()`, `sum()`, `mean()`, `std()`, `var()`, `idxmax()`, `argmax()` để phân tích số liệu thống kê.
- **Thao tác chuỗi**: Các hàm như `str.count('Java')`, `str.upper()`, `replace('Java', 'C#')` cho phép xử lý dữ liệu chuỗi.
- **Nhóm giá trị**: Có thể nhóm các giá trị trong Series bằng `groupby()`.
- **Xử lý giá trị thiếu**: Sử dụng `dropna()` để loại bỏ các giá trị thiếu hoặc `fillna()` để điền các giá trị này (ví dụ: bằng giá trị trung bình). Có thể sử dụng **nội suy tuyến tính (`interpolate()`) hoặc nội suy lân cận gần nhất (`Nearest Neighbor Interpolation`)** để điền vào các giá trị bị thiếu.

**Pandas DataFrame**: Là cấu trúc dữ liệu 2 chiều với các cột có thể thuộc các kiểu khác nhau, giống như một bảng tính hoặc bảng cơ sở dữ liệu.

- **Tạo và truy cập**: Có thể truy cập các cột bằng tên (`df['Newspaper']`, `df.Newspaper`) và các hàng bằng chỉ số.
- **Sắp xếp**: Hỗ trợ sắp xếp dữ liệu.
- **Thao tác cột/hàng**: Bao gồm thêm cột, xóa hàng (`df.drop(1, axis=0)`), hoặc xóa cột (`df.drop('Radio', axis=1)`).
- **Truy cập nâng cao**: Sử dụng `loc` để lập chỉ mục bằng nhãn và `iloc` để lập chỉ mục bằng chỉ số vị trí (ví dụ: `df.loc['C', 'Radio']`, `df.iloc`).
- **Ghép nối dữ liệu**: Có thể nối các DataFrame bằng `pd.concat()`.
- **Chuyển đổi kiểu dữ liệu**: Hỗ trợ chuyển đổi các danh mục thành số.

---

#### 2.3. Vẽ biểu đồ với Pandas và thư viện Seaborn, Matplotlib

Nội dung đề cập đến các loại biểu đồ phổ biến và cách vẽ chúng bằng các thư viện khác nhau:

- **Biểu đồ đường (Line Chart)**: Dùng để quan sát sự thay đổi của một hoặc nhiều biến theo một biến khác, thường được sử dụng trong phân tích xu hướng và chuỗi thời gian. Có thể được vẽ bằng Matplotlib, Seaborn và Plotly.

![[Pasted image 20250804204147.png]]

- **Biểu đồ hộp (Box Plots)**: Mô tả phân phối dữ liệu, các giá trị ngoại lệ và giá trị trung vị. Được sử dụng để xác định sự tồn tại của các giá trị ngoại lệ trong tập dữ liệu. Có thể vẽ bằng Matplotlib và Plotly.

![[Pasted image 20250804204222.png]]

- **Biểu đồ cột (Bar Chart)**: Sử dụng các thanh để hiển thị sự thay đổi giá trị của một biến cụ thể so với biến khác. Thường dùng cho dữ liệu rời rạc hoặc phân loại, có thể là biểu đồ ngang hoặc dọc. Có thể vẽ bằng Matplotlib và Plotly.

![[Pasted image 20250804204308.png]]

- **Biểu đồ Donut (Donut Chart)**: Một loại biểu đồ bánh có lỗ ở giữa. Vẽ bằng Matplotlib.

![[Pasted image 20250804204334.png]]

- **Biểu đồ tương quan (Correlation Chart / Heatmap)**: Biểu đồ 2 chiều dùng để phân tích mối tương quan giữa các trường khác nhau trong tập dữ liệu. Các ô vuông được tô màu thể hiện mức độ tương quan. Seaborn và Matplotlib có thể tạo biểu đồ này.

![[Pasted image 20250804204444.png]]

![[Pasted image 20250804204421.png]]

- **Biểu đồ phân tán (Scatter Plot)**: Dữ liệu được phân tán giữa hai trục, dùng để nghiên cứu mối tương quan giữa hai biến. Có thể cho thấy mối tương quan dương, âm hoặc không có mối liên hệ.

![[Pasted image 20250804204512.png]]

- **Biểu đồ cặp (Pair Plot)**: Vẽ phân phối hai biến theo cặp để thể hiện mối quan hệ của mỗi biến với tất cả các biến khác trong tập dữ liệu, rất hữu ích cho việc khám phá dữ liệu. Seaborn được sử dụng cho Pairplot.

![[Pasted image 20250804204610.png]]

- **Biểu đồ bánh (Pie Chart)**: Hiển thị tỷ lệ phần trăm trung bình của từng loại tải so với tổng tải trung bình. Vẽ bằng Matplotlib.

![[Pasted image 20250804204634.png]]

- **Biểu đồ đếm (Count Plot)**: Hiển thị số lượng quan sát của một biến phân loại trong tập dữ liệu. Chỉ sử dụng với các biến phân loại. Seaborn được sử dụng cho Count Plot.

![[Pasted image 20250804204658.png]]

- **Biểu đồ tần suất (Histogram)**: Dùng để quan sát phân phối tần suất của một biến, chia biến thành các khoảng và chiều dài các thanh thể hiện tần suất. Có thể dùng cho dữ liệu rời rạc và liên tục.

![[Pasted image 20250804204735.png]]

- **Biểu đồ bong bóng (Bubble Chart)**: Tương tự như biểu đồ phân tán nhưng dùng để quan sát mối quan hệ giữa ba biến, trong đó kích thước của bong bóng tương ứng với biến thứ ba. Có thể vẽ bằng Matplotlib và Plotly.

![[Pasted image 20250804204757.png]]

- **Biểu đồ KDE (Kernel Density Estimate Plot)**: Dùng để trực quan hóa mật độ xác suất của một biến liên tục. Có thể vẽ mật độ xác suất tại các giá trị khác nhau của biến hoặc mật độ xác suất chống lại các giá trị khác của một biến khác (2D KDE Plot). Seaborn được sử dụng cho KDE Chart.

![[Pasted image 20250804204820.png]]

- **Biểu đồ DistPlot**: Kết hợp histogram và kdeplot, dùng với dữ liệu rời rạc hoặc liên tục. Seaborn được sử dụng cho DisPlot Chart.

![[Pasted image 20250804204856.png]]

- **Trực quan hóa 3D**: Sử dụng khi cần quan sát mối quan hệ giữa ba biến số. Có thể vẽ biểu đồ phân tán 3D, biểu đồ bề mặt, biểu đồ đường đồng mức.

---

#### 2.4. Phân tích dữ liệu qua các case study thực tế

Các nghiên cứu điển hình minh họa việc áp dụng trực quan hóa dữ liệu vào các vấn đề thực tế:

##### 2.4.1. Dữ liệu máy biến áp (ETTh dataset)

- **Mục tiêu phân tích**: Xác định thời điểm có nhiệt độ OT cao nhất, hiểu mối tương quan giữa các biến, phân phối dữ liệu, tỷ lệ dữ liệu lỗi và phân phối tải trung bình cho từng loại tải.
- **Các biểu đồ được sử dụng**: Biểu đồ đường, biểu đồ bánh, biểu đồ cột, biểu đồ hộp, biểu đồ Donut và biểu đồ tương quan.
- **Ví dụ phân tích**:
    - Sử dụng **Line Chart** để hiển thị nhiệt độ dầu (OT) của các mẫu đầu tiên, giúp xác định xu hướng nhiệt độ theo thời gian.
    - **Box Plots** được dùng để hiểu sự phân bố của dữ liệu và xác định các giá trị ngoại lệ.
    - **Correlation Chart (Heatmap) và Pair Plot** được dùng để phân tích mối tương quan giữa các biến.
    - **Pie Chart** để hiển thị phân phối tải trung bình cho từng loại tải (HUFL, HULL, MUFL, MULL, LUFL, LULL).

##### 2.4.2. Dữ liệu điểm học sinh (Student Performance dataset)

- **Nguồn dữ liệu**: Kaggle Dataset.
- **Các biểu đồ được sử dụng**: Biểu đồ cột và biểu đồ đếm.
- **Ví dụ phân tích**:
    - **Bar Chart** được dùng để hiển thị sự thay đổi giá trị của một biến so với biến khác, thường cho dữ liệu rời rạc hoặc phân loại.
    - **Count Plot** được dùng để hiển thị số lượng quan sát của một biến phân loại trong tập dữ liệu.

##### 2.4.3. Dữ liệu hoa Iris (Iris dataset)

- **Nguồn dữ liệu**: Kaggle Dataset.
- **Các biểu đồ được sử dụng**: Histogram, Scatter, Bubble, KDE, DisPlot và trực quan hóa 3D.
- **Ví dụ phân tích**:
    - **Histogram** để quan sát phân phối tần suất của một biến, xem cách các giá trị được phân phối và mức độ lệch của tập dữ liệu.
    - **Scatter Plot** để nghiên cứu mối tương quan giữa hai biến.
    - **Bubble Chart** để quan sát mối quan hệ giữa ba biến, với kích thước bong bóng tương ứng với biến thứ ba.
    - **KDE Plot** để trực quan hóa mật độ xác suất của một biến liên tục.
    - **DisPlot** kết hợp histogram và KDE plot.
    - **Pairplot** để hiển thị phân phối hai biến theo cặp, hữu ích cho việc khám phá dữ liệu và phân tích mối quan hệ giữa các biến.
    - **3D Visualization** khi cần quan sát mối quan hệ giữa ba biến số trở lên.

##### 2.4.4. Dữ liệu chuyến đi Uber (Uber Trips dataset)

- **Nguồn dữ liệu**: Chứa khoảng 4,5 triệu chuyến xe Uber ở New York City từ tháng 4 đến tháng 9 năm 2014 và 14,3 triệu chuyến từ tháng 1 đến tháng 6 năm 2015.
- **Thông tin chi tiết được rút ra**: Thứ Hai là ngày có lợi nhuận cao nhất, thứ Bảy có ít người dùng Uber nhất, 6 giờ tối là giờ bận rộn nhất, và hầu hết các chuyến đi Uber bắt đầu vào khoảng 5 giờ sáng gần khu vực Manhattan.
- **Phân tích cụ thể**:
    - **Phân tích số chuyến đi theo ngày**: Số chuyến đi Uber tăng vào các ngày làm việc và giảm vào cuối tuần.
    - **Phân tích số chuyến đi theo giờ**: Số chuyến đi giảm sau nửa đêm, bắt đầu tăng sau 5 giờ sáng và đạt đỉnh vào 6 giờ tối, sau đó bắt đầu giảm.
    - **Phân tích mối tương quan giữa giờ và các ngày trong tuần**: Thể hiện rõ xu hướng sử dụng Uber vào các ngày khác nhau.
    - **Phân tích mật độ chuyến đi theo khu vực (kinh độ và vĩ độ)**: Trực quan hóa mật độ chuyến đi Uber theo các khu vực của thành phố New York.


---


### 3. Phân tích nâng cao

#### 3.1. Cách chọn biểu đồ phù hợp (choose the right chart)

Việc chọn biểu đồ phù hợp là rất quan trọng vì không có loại biểu đồ nào là giải pháp "một kích thước phù hợp cho tất cả". Quy trình gồm 5 bước:

1. **Bước 1: Xác định loại dữ liệu**
    - Dữ liệu có thể được phân loại thành bốn loại: **định lượng (quantitative)** (giá trị số), **định tính (categorical)** (giá trị không phải số), **thời gian (temporal)** (dữ liệu dựa trên thời gian), hoặc **không gian (spatial)** (dữ liệu dựa trên vị trí).
2. **Bước 2: Xác định mối quan hệ giữa các biến**
    - Bạn muốn hiển thị sự **so sánh** (Comparison) giữa hai hoặc nhiều điểm dữ liệu (ví dụ: biểu đồ cột).
    - Bạn muốn hiển thị **phân phối** (Distribution) của dữ liệu (ví dụ: histogram, box plot).
    - Bạn muốn hiển thị **mối quan hệ** (Relationship) giữa hai hoặc nhiều biến (ví dụ: scatter plot, bubble chart).
3. **Bước 3: Xác định mục đích của trực quan hóa**
    - Bạn muốn truyền tải thông điệp gì qua biểu đồ?
    - Để **hiển thị xu hướng theo thời gian**, biểu đồ đường hoặc biểu đồ vùng có thể phù hợp hơn.
    - Để **so sánh các điểm dữ liệu**, biểu đồ cột có thể là lựa chọn tốt hơn.
    - Để **hiển thị phân phối**, histogram hoặc box plot có thể hữu ích hơn.
4. **Bước 4: Xác định đối tượng người xem**
    - Nếu đối tượng là **chuyên gia**, bạn có thể sử dụng các biểu đồ phức tạp hơn như heatmap.
    - Nếu đối tượng **ít quen thuộc hơn với trực quan hóa dữ liệu**, các biểu đồ đơn giản hơn như biểu đồ bánh hoặc biểu đồ cột có thể hiệu quả hơn.
5. **Bước 5: Chọn loại biểu đồ thích hợp**
    - Hãy thử nghiệm với các loại biểu đồ khác nhau để tìm ra loại phù hợp nhất với dữ liệu của bạn.

Ngoài ra, có các **mẹo lựa chọn biểu đồ** dựa trên mục đích chính của trực quan hóa:

- Hiển thị sự thay đổi theo thời gian.
- Hiển thị cấu trúc phần-tổng.
- Hiển thị cách dữ liệu được phân phối.
- So sánh các giá trị giữa các nhóm.
- Quan sát mối quan hệ giữa các biến.
- Trình bày tính năng nổi bật.

---

#### 3.2. So sánh các thư viện vẽ biểu đồ: Matplotlib, Seaborn, Plotly

- **Matplotlib**: Cung cấp khả năng **tùy chỉnh mở rộng** nhưng đòi hỏi nhiều mã hơn để tạo ra các biểu đồ phức tạp. Nó được sử dụng để vẽ nhiều loại biểu đồ như Line Chart, Box Plots, Bar Chart, Donut Chart, Correlation Chart, Pie Chart, Bubble Chart.
- **Seaborn**: **Đơn giản hóa các biểu đồ thống kê** với các chủ đề và hàm tích hợp. Nó đặc biệt hữu ích cho các biểu đồ như Line Chart, Correlation Chart (Heatmap), Pair Plot, Count Plot, KDE Chart, DisPlot, và các loại biểu đồ dựa trên phân phối.
- **Plotly**: Xuất sắc trong việc tạo ra các **hình ảnh trực quan động và tương tác**. Nó được dùng để tạo Line Chart, Box Plots, Bar Chart, Bubble Chart.

---

#### 3.3. Vai trò của biểu đồ trong phân tích tương quan, phát hiện bất thường, phân tích phân phối

- **Phân tích tương quan**:
    - **Scatter Plot**: Là một trong những biểu đồ phổ biến nhất để quan sát mối quan hệ giữa hai biến. Nếu một biến tăng/giảm cùng với biến kia, chúng có tương quan dương. Nếu một biến tăng khi biến kia giảm, chúng có tương quan âm. Nếu không có mối quan hệ rõ ràng, chúng không liên quan.
    - **Bubble Chart**: Tương tự Scatter Plot nhưng thêm một biến thứ ba được thể hiện bằng kích thước của bong bóng, giúp quan sát mối quan hệ giữa ba biến.
    - **Heatmap / Correlation Chart**: Là biểu đồ hai chiều chính để phân tích mối tương quan giữa các trường khác nhau trong một tập dữ liệu.
    - **Pair Plot**: Hiển thị phân phối hai biến theo cặp để phân tích mối quan hệ của mỗi biến với tất cả các biến khác trong tập dữ liệu.
- **Phát hiện bất thường (Outliers)**:
    - **Box Plots**: Là công cụ hiệu quả để xác định sự tồn tại của các giá trị ngoại lệ trong tập dữ liệu. Các giá trị ngoại lệ được xác định dựa trên khoảng tứ phân vị (IQR = Q3 - Q1), thường là các điểm nằm ngoài 1.5 * IQR so với Q1 hoặc Q3.
- **Phân tích phân phối**:
    - **Histogram**: Dùng để quan sát phân phối tần suất của một biến, cho thấy cách các giá trị được phân phối và mức độ lệch của tập dữ liệu.
    - **Box Plots**: Mô tả phân phối dữ liệu, cho thấy trung vị, các tứ phân vị và phạm vi của dữ liệu.
    - **KDE Plot**: Trực quan hóa mật độ xác suất của một biến liên tục, hữu ích để xem hình dạng phân phối của dữ liệu.
    - **DistPlot**: Kết hợp Histogram và KDE plot để cung cấp cái nhìn tổng quan về phân phối của một biến.


---


### 4. Ứng dụng thực tiễn

#### 4.1. Trực quan hóa dữ liệu để dự báo thời tiết (weather forecasting)

- Trong trường hợp nghiên cứu về dự báo nhiệt độ, trực quan hóa dữ liệu được sử dụng để hiểu dữ liệu chuỗi thời gian.
- Các kỹ thuật xử lý dữ liệu bị thiếu như **`fillna(mean)`** (điền giá trị trung bình) và **`interpolate()`** (nội suy) được áp dụng để chuẩn bị dữ liệu cho mô hình.
- Để giảm nhiễu (noise reduction) trong dữ liệu thời tiết, các phương pháp như **Simple Moving Average (SMA)** và **Exponential Moving Average (EMA)** được sử dụng để làm mượt dữ liệu và làm nổi bật xu hướng.

---

#### 4.2. Phát hiện gian lận trong giao dịch (fraud detection)

- Nghiên cứu điển hình về phát hiện gian lận thẻ tín dụng sử dụng trực quan hóa để phân tích các giao dịch.
- Các chỉ số đánh giá hiệu suất mô hình như **Accuracy, Precision và Recall** được tính toán và trực quan hóa để hiểu khả năng phát hiện gian lận.
- Các kỹ thuật như **Class weights** và **Focal loss** được áp dụng để cải thiện hiệu suất, đặc biệt là tăng **Recall** (khả năng phát hiện đúng giao dịch gian lận) từ 0.76 lên 0.906 và sau đó là 0.96, điều này rất quan trọng trong phát hiện gian lận.

---

#### 4.3. Tối ưu hiển thị dữ liệu cho từng đối tượng người dùng

- Việc **xác định đối tượng người xem** là một bước quan trọng trong quy trình chọn biểu đồ phù hợp.
- Nếu đối tượng là **chuyên gia**, bạn có thể sử dụng các biểu đồ phức tạp hơn như heatmap để cung cấp thông tin chi tiết và đầy đủ.
- Nếu đối tượng **ít quen thuộc hơn với trực quan hóa dữ liệu**, các biểu đồ đơn giản hơn như biểu đồ bánh hoặc biểu đồ cột sẽ hiệu quả hơn để truyền tải thông điệp một cách rõ ràng và dễ hiểu. Điều này đảm bảo rằng thông tin được tiếp cận và hiểu bởi đúng đối tượng.

---

#### 4.4. Tạo biểu đồ tương tác và nâng cao trải nghiệm người dùng

- Thư viện **Plotly** được nhấn mạnh vì khả năng **tạo ra các hình ảnh trực quan động và tương tác**.
- Các biểu đồ tương tác cho phép người dùng **tự khám phá dữ liệu, phóng to, thu nhỏ, hoặc xem thông tin chi tiết** khi di chuột, qua đó **nâng cao trải nghiệm người dùng** và giúp họ tự rút ra những hiểu biết sâu sắc hơn.


---


### 5. Tổng kết

- **Trực quan hóa dữ liệu là chìa khóa để chuyển đổi dữ liệu phức tạp thành thông tin dễ hiểu** và truyền đạt hiệu quả.
- **Quy trình 5 bước** để chọn biểu đồ phù hợp bao gồm xác định loại dữ liệu, mối quan hệ biến, mục đích, đối tượng và cuối cùng là chọn biểu đồ.
- Các thư viện Python như **Matplotlib, Seaborn và Plotly** cung cấp các khả năng đa dạng, từ tùy chỉnh chuyên sâu đến tương tác động.
- **Pandas Series và DataFrame** là nền tảng quan trọng cho việc xử lý và chuẩn bị dữ liệu trước khi trực quan hóa.
- Các nghiên cứu điển hình (ETTh, Student Performance, Iris, Uber) minh họa cách các biểu đồ và kỹ thuật trực quan hóa được áp dụng để **phân tích xu hướng, mối quan hệ, phân phối và phát hiện bất thường** trong các tập dữ liệu thực tế.
- Trực quan hóa không chỉ dùng để hiểu dữ liệu mà còn để **giải quyết các vấn đề thực tiễn** như dự báo thời tiết và phát hiện gian lận, đồng thời **tối ưu hóa trải nghiệm người dùng**.