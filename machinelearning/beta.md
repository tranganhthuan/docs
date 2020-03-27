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

Động từ

- Splitting (Phân nhánh): Phân chia Node thành các Child Node.

- Prunning (Tỉa cây): Bỏ bớt các node. Là quá trình ngược lại với Splitting. 

## Decision Tree - Classification:

Bước 1: Split Root node thành 2 node,  cách chia dựa vào values của cột Features: 

- Trường hợp Features là **boolean**: Chia theo True/False có 1 cách chia.

- Trường hợp Features là **category**: Chia theo Category(One/Rest) có c cách chia ứng với số categories.

- Trường hợp Features là **number**: Sắp xếp thứ tự của các giá trị. Lấy trung bình của 2 giá trị liên tiếp khác nhau. Chia tập data theo các giá trị này có n các chia ứng với số giá trị trung bình.
	
Bước 2: Tính Impurity/Information Gain ở từng cách chia - Impurity thể hiện độ vẫn đục của tập data sau khi chia (xấu), trong khi Information Gain thể hiện lượng thông tin thu được của tập data sau khi chia (tốt).

Với mỗi cách chia ta làm 2 bước như sau:

Bước 2.1. Tính Gini Index/ Entropy ở từng node child.
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

Bước 2.2: Tính Impurity/Infomation Gain của cách chia.

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

- Parent node chỉ có 1 phần tử.

- Parent node chỉ có 1 loại label.

- Parent node chỉ gồm các phần tử có features giống nhau hoàn toàn nhưng khác label.

## Decision Tree - Regression:
