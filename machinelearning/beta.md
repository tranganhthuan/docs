---
layout: default
title: Tree based models(Beta)
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

## Decision Tree - Khái niệm:

Phân theo chức năng:

- Root Node: Là node gốc, gồm toàn bộ data chưa được chia.

- Decision Node: Là node chứa câu hỏi, được chia ra từ Root Node và tiếp tục được phân chia.

- Leaf Node: Là node chứa đầu ra.

Phân theo quan hệ:

- Parent Node: Là node được chia thành nhiều Child Node. Có thể là Root Node, hoặc Decision Node.

- Child Node: Là node nhận data từ Parent Node và có thể tiếp tục được chia. Có thể là Decision Node, hoặc Leaf Node.

- Sibling Node: Là các node có cùng Parent Node.

Thuộc tính:

- Max depth: Độ cao tối đa của tree tính từ Root Node (Root Node có độ cao bằng 0).

- Max features: Số features tối đa quan tâm khi splitting.

- Min sample split: Số sample còn có thể split. Nếu ít hơn số này thì không split nữa.

- Min sample leaf: Số sample có trong Leaf Node. Nếu Decision Node phân chia Leaf Node có chứa ít sample hơn số này thì sẽ không phân chia.

Động từ

- Splitting (Phân nhánh): Phân chia Node thành các Child Node.

- Prunning (Tỉa cây): Bỏ bớt các node. Là quá trình ngược lại với Splitting. 

## Decision Tree - Classification:

Bước 1: Split Parent Node thành 2 node - ở lần đầu tiên Parent Node là Root Node,  cách chia dựa vào values của cột Features: 

- Trường hợp Features là **boolean**: Chia theo True/False có 1 cách chia.

- Trường hợp Features là **category**: Chia theo Category(One/Rest) có c cách chia ứng với số categories.

- Trường hợp Features là **number**: Sắp xếp thứ tự của các giá trị. Lấy trung bình của 2 giá trị liên tiếp khác nhau. Chia tập data theo các giá trị này có n các chia ứng với số giá trị trung bình.
	
Bước 2: Tính Impurity/Information Gain ở từng cách chia - Impurity thể hiện độ vẫn đục của tập data sau khi chia (xấu), trong khi Information Gain thể hiện lượng thông tin thu được của tập data sau khi chia (tốt).

Với mỗi cách chia ta làm 2 bước như sau:

a. Tính Gini Index/ Entropy ở từng node child.
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

b. Tính Impurity/Infomation Gain của cách chia.

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
	
Bước 3: Chọn cách chia có Impurity nhỏ nhất hoặc Information Gain cao nhất.

Bước 4: Lặp lại bước 1,2,3 với 2 child node vừa được chia, xem mỗi child node là một parent node cho đến khi không còn chia được nửa.

Có 3 trường hợp không còn chia được nữa:

- Parent Node chỉ có 1 phần tử.

- Parent Node chỉ có 1 loại label.

- Parent Node chỉ gồm các phần tử có features giống nhau hoàn toàn nhưng khác label.

Bước 5: Sau khi đã có được Decision Tree hoàn chỉnh. Sample cần được dự đoán sẽ được hỏi qua các câu hỏi ở Decision Node cho đến khi tới Leaf Node. Label cuả Sample sẽ là Label của Leaf Node (Label của Leaf Node được xác định bằng Label có số lượng cao nhất trong Leaf Node).

## Decision Tree - Regression:

Bước 1: Split Parent Node thành 2 node (Giống như Decision Tree - Classification).

Bước 2: Tính Squared Error của mỗi cách chia bằng cách:

- Tính giá trị trung bình của từng node:

$$mean(n) = \frac{1}{n} \sum_{i=1}^n y_i$$

- Tính Squared Error của từng node theo công thức:

$$e(n) = \sum_{i=1}^n (mean - y_i)^2$$

- Cộng Squared Error của 2 node:

$$e = e(n_1) + e(n_2)$$

Bước 3: Chọn cách chia có Squared Error thấp nhất.

Bước 4: Lặp lại bước 1,2,3 với 2 child node vừa được chia, xem mỗi child node là một parent node cho đến khi không còn chia được nửa.

Bước 5: Sau khi đã có được Decision Tree hoàn chỉnh. Sample cần được dự đoán sẽ được hỏi qua các câu hỏi ở Decision Node cho đến khi tới Leaf Node. Label của Sample sẽ là giá trị trung bình của các Label trong Leaf Node đó.

## Random Forest:

Bước 1: Tạo Boostrapped Sample từ Original Sample và có cùng size $$n$$.

Cách tạo Boostrapped Sample với size $$k$$:

- Chọn ngẫu nhiên 1 phần tử trong Original Sample.

- Ghi thông tin vào Boostrapped Sample.

- Bỏ lại vào Original Sample. 

- Lặp lại $$k$$ lần, ta thu được Boostrapped Sample có size $$k$$.

Bước 2: Tạo Decision Tree ứng với mỗi Boostrapped Sample. Với mỗi lần split, chỉ chọn một số Features để xem xét.

Bước 3: Khi đã có Random Forest, mỗi Sample đưa vào sẽ được dự đoán bởi tất cả Decision Tree - các Decision Tree sẽ vote cho các Label. Label của Sample sẽ là Label được vote nhiều nhất.  

*Bổ sung:* Độ chính xác của Random Forest có thể được tính bằng **Out of Bag Score**.

## Ada Boost:

Bước 1: Tạo Sample Weight ứng với mỗi Sample.

- Sample Weight ban đầu bằng nhau, tính bằng công thức:

$$w = \frac{1}{n}$$

