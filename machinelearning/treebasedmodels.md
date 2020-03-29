---
layout: default
title: Tree based models
nav_order: 4
parent: Machine Learning
---
# Treebased models
{: .no_toc }

<hr/>

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

<hr/>

## Decision Tree - Khái niệm.

### Phân theo chức năng:
{: .no_toc }

- Root Node: Là node gốc, gồm toàn bộ data chưa được chia.

- Decision Node: Là node chứa câu hỏi, được chia ra từ Root Node và tiếp tục được phân chia.

- Leaf Node: Là node chứa đầu ra.

### Phân theo quan hệ:
{: .no_toc }

- Parent Node: Là node được chia thành nhiều Child Node. Có thể là Root Node, hoặc Decision Node.

- Child Node: Là node nhận data từ Parent Node và có thể tiếp tục được chia. Có thể là Decision Node, hoặc Leaf Node.

- Sibling Node: Là các node có cùng Parent Node.

### Thuộc tính:
{: .no_toc }

- Max depth: Độ cao tối đa của tree tính từ Root Node (Root Node có độ cao bằng 0).

- Max features: Số features tối đa quan tâm khi splitting.

- Min sample split: Số sample còn có thể split. Nếu ít hơn số này thì không split nữa.

- Min sample leaf: Số sample có trong Leaf Node. Nếu Decision Node phân chia Leaf Node có chứa ít sample hơn số này thì sẽ không phân chia.

### Động từ
{: .no_toc }

- Splitting (Phân nhánh): Phân chia Node thành các Child Node.

- Prunning (Tỉa cây): Bỏ bớt các node. Là quá trình ngược lại với Splitting. 

<hr/>

## Decision Tree - Classification.

### Bước 1: 
{: .no_toc }

Split Parent Node thành 2 node - ở lần đầu tiên Parent Node là Root Node,  cách chia dựa vào values của cột Features: 

- Trường hợp Features là **boolean**: Chia theo True/False có 1 cách chia.

- Trường hợp Features là **category**: Chia theo Category(One/Rest) có c cách chia ứng với số categories.

- Trường hợp Features là **number**: Sắp xếp thứ tự của các giá trị. Lấy trung bình của 2 giá trị liên tiếp khác nhau. Chia tập data theo các giá trị này có n các chia ứng với số giá trị trung bình.
	
### Bước 2: 
{: .no_toc }

Tính Impurity/Information Gain ở từng cách chia - Impurity thể hiện độ vẫn đục của tập data sau khi chia (xấu), trong khi Information Gain thể hiện lượng thông tin thu được của tập data sau khi chia (tốt).

Với mỗi cách chia ta làm 2 bước như sau:

Tính Gini Index/ Entropy ở từng node child.

- Công thức Gini Index:

	- Trường hợp Label là **true/false**: 

	$$\text{Gini} = 1 - (p^2 + q^2)$$	
		
	- Trường hợp Label là **category**: 
	
	$$\text{Gini} = 1 - \sum_{i = 1}^n p_i^2$$
		
- Công thức Entropy:

	- Trường hợp Label là **true/false**: 

	$$E(p) = - (p \log(p) + q \log(q)) $$

	- Trường hợp Label là **category**:

	$$E(p) = -\sum_{i=1}^n p_i \log(p_i)$$

- Với: 

	- Trường hợp Label là **true/false**: 
	
		$$p = p(y = true) = \frac{t}{n}$$

		- $$t$$: là số phần tử có label là true

		- $$n$$: tổng số phần tử node hiện tại
		
		$$q = p(y = false) = \frac{f}{n}$$

		- $$t$$: là số phần tử có label là false

		- $$n$$: tổng số phần tử node hiện tại
		
		$$p + q = 1$$

	- Trường hợp Label là **category**:
	
		$$p_i = p(y = k_i) = \frac{k_i}{n}$$

		- $$k_i$$: là số phần tử có label là $$k_i$$

		- $$n$$: tổng số phần tử node hiện tại

Tính Impurity/Infomation Gain của cách chia.

- Công thức tính Impurity:

$$Impurity = \sum_{i = 1}^n w_i f(n_i)$$

- Với:
	- $$w_i = \frac{n_{child}}{n_{parent}}$$: là tỉ lệ giữa số phần tử có trong node child và số phần tử có trong node parent.
	
	- $$f(n_i)$$: là Gini Index/Entropy của node children.
	
- Công thức tính Infomation Gain:

$$Gain = E(parent) - E(children)$$

- Với:

	- $$E(parent)$$: là Entropy của node parent đã được tính ở lần split trước. Entropy của Root Node bằng 1.
	
	- $$E(children)$$: là Impurity của 2 node child được tính bằng Entropy.
	
### Bước 3: 
{: .no_toc }

Chọn cách chia có Impurity nhỏ nhất hoặc Information Gain cao nhất.

### Bước 4: 
{: .no_toc }

Lặp lại bước 1,2,3 với 2 child node vừa được chia, xem mỗi child node là một parent node cho đến khi không còn chia được nửa.

Có 3 trường hợp không còn chia được nữa:

- Parent Node chỉ có 1 phần tử.

- Parent Node chỉ có 1 loại label.

- Parent Node chỉ gồm các phần tử có features giống nhau hoàn toàn nhưng khác label.

### Bước 5: 
{: .no_toc }

Sau khi đã có được Decision Tree hoàn chỉnh. Sample cần được dự đoán sẽ được hỏi qua các câu hỏi ở Decision Node cho đến khi tới Leaf Node. Label cuả Sample sẽ là Label của Leaf Node (Label của Leaf Node được xác định bằng Label có số lượng cao nhất trong Leaf Node).

<hr/>

## Decision Tree - Regression.

### Bước 1: 
{: .no_toc }

Split Parent Node thành 2 node (Giống như Decision Tree - Classification).

### Bước 2: 
{: .no_toc }

Tính Squared Error của mỗi cách chia bằng 3 bước:

- Tính giá trị trung bình của từng node:

$$mean(n) = \frac{1}{n} \sum_{i=1}^n y_i$$

- Tính Squared Error của từng node theo công thức:

$$e(n) = \sum_{i=1}^n (mean - y_i)^2$$

- Cộng Squared Error của 2 node:

$$e = e(n_1) + e(n_2)$$

### Bước 3: 
{: .no_toc }

Chọn cách chia có Squared Error thấp nhất.

### Bước 4: 
{: .no_toc }

Lặp lại bước 1,2,3 với 2 child node vừa được chia, xem mỗi child node là một parent node cho đến khi không còn chia được nửa.

### Bước 5: 
{: .no_toc }

Sau khi đã có được Decision Tree hoàn chỉnh. Sample cần được dự đoán sẽ được hỏi qua các câu hỏi ở Decision Node cho đến khi tới Leaf Node. Label của Sample sẽ là giá trị trung bình của các Label trong Leaf Node đó.

<hr/>

## Random Forest.

### Bước 1: 
{: .no_toc }

Tạo Boostrapped Sample từ Original Sample và có cùng size $$n$$.

Cách tạo Boostrapped Sample với size $$k$$:

- Chọn ngẫu nhiên 1 phần tử trong Original Sample.

- Ghi thông tin vào Boostrapped Sample.

- Bỏ lại vào Original Sample. 

- Lặp lại $$k$$ lần, ta thu được Boostrapped Sample có size $$k$$.

### Bước 2: 
{: .no_toc }

Tạo Decision Tree ứng với mỗi Boostrapped Sample. Với mỗi lần split, chỉ chọn một số Features để xem xét.

### Bước 3: 
{: .no_toc }

Lặp lại bước 1,2 cho đến khi đủ số tree mong muốn.

### Bước 4: 
{: .no_toc }

Khi đã có Random Forest, mỗi Sample đưa vào sẽ được dự đoán bởi tất cả Decision Tree - các Decision Tree sẽ vote cho các Label. Label của Sample sẽ là Label được vote nhiều nhất.  

*Bổ sung:* Độ chính xác của Random Forest có thể được tính bằng **Out of Bag Score**.

<hr/>

## Ada Boost.

### Bước 1: 
{: .no_toc }

Tạo Sample Weight ứng với mỗi Sample - Sample Weight sẽ được dùng đến ở lần chia thứ 2.

Sample Weight ban đầu bằng nhau và bằng:

$$w = \frac{1}{n}$$

Với: 
- $$w$$: là weight của mỗi phần tử.
- $$n$$ là tổng số phần tử.

### Bước 2: 
{: .no_toc }

Chọn cách chia tốt nhất (giống như Decision Tree). Tạo được một Decision Tree với cách chia này. 

Decision Tree chỉ với  một Decision Node được gọi là một **Stump** - **Weak Learner**.

### Bước 3: 
{: .no_toc }

Tính **Amount of Say** của Decision Tree này. Amount of Say càng lớn thì khi predict sample mới, vote của tree sẽ càng có giá trị.

Ta dùng Decision Tree vừa mới tạo dự đoán lại tập dữ liệu ở trên. Khi đó, Amount of Say được tính bằng công thức:

$$\text{Amount of Say} = \frac{1}{2} \log(\frac{1 - \text{Total Error}}{\text{Total Error}})$$

Với:

- $$\text{Total Error}$$: là tổng Sample Weight của các dự đoán sai

### Bước 4: 
{: .no_toc }

Cập nhật Sample Weight.

Có 2 trường hợp:

- Dữ liệu dự đoán đúng:

$$\text{New Sample Weight} = \text{Sample Weight}*e^{\text{Amount of Say}}$$

- Dữ liệu dự đoán sai:

$$\text{New Sample Weight} = \text{Sample Weight}*e^{-\text{Amount of Say}}$$

Sau đó normalize New Sample Weight - để tổng của chúng bằng 1:

$$\text{Normalized Sample Weight} = \frac{New Sample Weight}{\sum_{i=1}^n New Sample Weight}$$

### Bước 5:
{: .no_toc }

Tạo Sample mới từ Original Sample và cũng có size bằng n dựa vào Sample Weight.

Cách tạo:

- Chọn số $$t$$ ngẫu nhiên thuộc khoảng $$[0,1)$$.

- Chọn có hoàn lại phần tử thứ $$k$$ trong Original Sample thỏa:

$$\sum_{i=0}^{k-1} \text{Sample Weight} \le t < \sum_{i=0}^{k} \text{Sample Weight}$$

- Lặp lại n lần

### Bước 6:
{: .no_toc }

Lặp lại bước 1,2,3,4,5 với tập Sample mới thu được cho đến khi đủ số tree mong muốn.

### Bước 7:
{: .no_toc }

Khi đã có model hoàn chỉnh, ta có 2 trường hợp:

- Classification: Label sẽ được dự đoán bởi các Decision Tree, với vote được tính bằng tổng Amount of Say của các Decision Tree đã vote cho Label. Label nào có giá trị vote lớn nhất sẽ được chọn.
- Regression: Label sẽ được tính bằng công thức:
	
	$$h = \frac{\sum_{i=1}^{n} \text{Amount of Say}_i * h_i}{\sum_{i=1}^{n} \text{Amount of Say}_i}$$

	Với:
	
	$$h_i$$: là giá trị dự đoán của tree thứ $$i$$
	$$\text{Amount of Say}_i$$: là giá trị dự đoán của tree thứ $$i$$
	
<hr/>

## Gradient Boosting
