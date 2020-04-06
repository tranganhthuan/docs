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

## Tree - Khái niệm.

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

## Decision Tree.

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

- Xác suất $$p$$: 

	- Trường hợp Label là **true/false**: 
	
		$$p = p(y = true) = \frac{t}{n}$$
		
	Với:
		
	$$t$$: là số phần tử có label là true
		
	$$n$$: tổng số phần tử node hiện tại
		
	$$q = p(y = false) = \frac{f}{n}$$
		
	Với:

	$$t$$: là số phần tử có label là false

	$$n$$: tổng số phần tử node hiện tại
		
	Ta có:
		
	$$p + q = 1$$

	- Trường hợp Label là **category**:
	
		$$p_i = p(y = k_i) = \frac{k_i}{n}$$
		
	Với:

	$$k_i$$: là số phần tử có label là $$k_i$$

	$$n$$: tổng số phần tử node hiện tại

Tính Impurity/Infomation Gain của cách chia.

- Công thức tính Impurity:

$$Impurity = \sum_{i = 1}^n w_i f(n_i)$$

Với:

$$w_i = \frac{n_{child}}{n_{parent}}$$: là tỉ lệ giữa số phần tử có trong node child và số phần tử có trong node parent.

$$f(n_i)$$: là Gini Index/Entropy của node children.
	
- Công thức tính Infomation Gain:

$$Gain = E(parent) - E(children)$$

Với:

$$E(parent)$$: là Entropy của node parent đã được tính ở lần split trước. Entropy của Root Node bằng 1.

$$E(children)$$: là Impurity của 2 node child được tính bằng Entropy.
	
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

## Regression Tree.

### Bước 1: 
{: .no_toc }

Split Parent Node thành 2 node (Giống như Decision Tree).

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

Sau khi đã có được Regression Tree hoàn chỉnh. Sample cần được dự đoán sẽ được hỏi qua các câu hỏi ở Decision Node cho đến khi tới Leaf Node. Label của Sample sẽ là giá trị trung bình của các Label trong Leaf Node đó.

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

Tạo Tree ứng với mỗi Boostrapped Sample. Với mỗi lần split, chỉ chọn một số Features để xem xét.

### Bước 3: 
{: .no_toc }

Lặp lại bước 1,2 cho đến khi đủ số tree mong muốn.

### Bước 4: 
{: .no_toc }

Khi đã có Random Forest, mỗi Sample đưa vào sẽ được dự đoán bởi tất cả Tree. 

- Classification: Label của Sample sẽ là Label được vote nhiều nhất.  

- Regression: Label của Sample là trung bình cộng của các kết quả dự đoán.

<hr/>

## Ada Boost.

### Bước 1: 
{: .no_toc }

Tạo Sample Weight ứng với mỗi Sample - Sample Weight sẽ được dùng đến ở lần chia thứ 2.

Sample Weight ban đầu bằng nhau và bằng:

$$w = \frac{1}{n}$$

Với: 

$$w$$: là weight của mỗi phần tử.
	
$$n$$: là tổng số phần tử.

### Bước 2: 
{: .no_toc }

Chọn cách chia tốt nhất (giống như Decision Tree/Regression Tree). Tạo được một Tree với cách chia này. 

Tree chỉ với  một Decision Node được gọi là một **Stump** - **Weak Learner**.

### Bước 3: 
{: .no_toc }

Tính **Amount of Say** của Tree này. Amount of Say càng lớn thì khi predict sample mới, vote của tree sẽ càng có giá trị.

Ta dùng Tree vừa mới tạo dự đoán lại tập dữ liệu ở trên. Khi đó, Amount of Say được tính bằng công thức:

$$\text{Amount of Say} = \frac{1}{2} \log(\frac{1 - \text{Total Error}}{\text{Total Error}})$$

Với:

$$\text{Total Error}$$: là tổng Sample Weight của các dự đoán sai

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

## Gradient Boosting - Tổng quát

### Bước 1:
{: .no_toc }

Tạo ra model ban đầu với hằng số - hàm này chỉ dự đoán một giá trị duy nhất cho dù đầu vào như thế nào. Hàm số có dạng:

$$F_0(x) = \underset{\gamma}{\operatorname{argmax}}  \sum_{i = 0}^n L(y_i, \gamma)$$

Với:
	
$$\underset{\gamma}{\operatorname{argmax}}$$: là tìm giá trị $$\gamma$$ sao cho hàm đạt giá trị nhỏ nhất
	
$$\sum_{i = 0}^n L(y_i, \gamma)$$: là Cost Function
	
$$\gamma$$: là giá trị dự đoán
	
Hàm này trả về giá trị $$\gamma$$ sao cho Cost Function đạt giá trị nhỏ nhất.

### Bước 2:
{: .no_toc }
Tính $$r_{i,m}$$, với:

$$r_{i,m} = -\frac{\partial L(y_i, F(x_i))}{\partial F(x_i)}$$

Với:

$$F(x) = F_{m-1}(x)$$: là hàm dự đoán vừa được tạo.

### Bước 3:
{: .no_toc }

Tạo Tree với Label được thay bằng vector $$r$$ (tập hợp của $$r_{i,m}$$). Các Tree trong Gradient Boost được scale về cùng kích cỡ.

### Bước 4:
{: .no_toc }

Với mỗi leaf của Tree mới tạo tính $$\gamma_{j,m}$$ bằng $$\gamma$$ để hàm Cost Function của Leaf Node đạt giá trị nhỏ nhất:

$$\gamma_{j,m} = \underset{\gamma}{\operatorname{argmax}} \sum_{x_i \in \mathbb{R}_{j,m}} L(y_i,F_{m-1}(x_i) + \gamma)$$

Với:

$$j,m$$: là Leaf Node thứ $$j$$ của Tree thứ $$m$$ 

$$x_i \in \mathbb{R}_{j,m}$$: là những phần tử ở trong Leaf Node thứ $$j$$ của Tree thứ $$m$$ - những phần tử ngoài Leaf Node sẽ bị bỏ qua. 

### Bước 5:
{: .no_toc }

Update hàm F_m(x):

$$F_m(x) = F_{m-1}(x) + \nu \sum_{j = 1}^{J_m} \gamma_{j,m} I(x_i \in \mathbb{R}_{j,m})$$

Với:

$$\sum_{j = 1}^{J_m}$$: được sử dụng trong trường hợp một Sample có thể ở nhiều Leaf Node, thì ta cộng tất cả giá trị này lại

$$\gamma_{j,m} I(x_i \in \mathbb{R}_{j,m})$$: là $$\gamma$$  của Leaf Node chứa $$x_i$$

$$\nu$$: là learning rate

### Bước 6
{: .no_toc }

Lặp lại bước 2,3,4,5 với $$m$$ tăng lên 1 cho đến khi $$m$$ bằng $$M$$ - số Tree ta muốn tạo.

<hr/>

## Gradient Boosting - Regression

### Bước 1:
{: .no_toc }

Dự đoán tất cả giá trị bằng giá trị trung bình của Label, vì giá trị này giúp hàm Cost Function đạt giá trị nhỏ nhất. 

$$F_0 = mean$$

Giải thích:

- Hàm Cost Function là hàm Mean Squared Error (MSE) - nhân $$\frac{1}{2}$$ để đạo hàm triệt tiêu, có dạng:

$$Cost = \frac{1}{2} \frac{1}{n} \sum_{i = 1}^n (y_i - \gamma)^2$$

- Lấy đạo hàm theo $$\gamma$$ ta được:

$$\frac{\partial Cost}{\partial \gamma} = - \frac{1}{n} \sum_{i = 1}^n (y_i - \gamma)$$

- Cho đạo hàm bằng $$0$$:

$$\begin{align}
  - \frac{1}{n} \sum_{i = 1}^n (y_i - \gamma) &= 0 \\
      \gamma &= \frac{1}{n} \sum_{i = 1}^n y_i \\
\end{align}$$

- Ta thấy, hàm Cost Function đạt giá trị nhỏ nhất, khi $$\gamma$$ là giá trị trung bình của $$y$$ - Label.

### Bước 2:
{: .no_toc }

Tạo Residual ứng với mỗi Sample, giá trị của Residual được tính bằng:

$$r_{i,m} = y_i - F(x)$$

Với:

$$F(x)$$: là hàm mới được tạo - cụ thể ở lần đầu này là {F_0(x)}

Giải thích:
- Vì Lost Function có công thức:

$$L(y, F(x)) = \frac{1}{2} (y - F(x))^2$$

- Nên khi đạo hàm theo $$F(x)$$ ta được:

$$\frac{\partial L(y, F(x))}{\partial F(x)} = -(y - F(x))$$

- Suy ra:

$$r_{i,m} = - \frac{\partial L(y, F(x))}{\partial F(x)} = y_i - F(x)$$

### Bước 3:
{: .no_toc }

Tạo ra một Regression Tree để fit vào tập dữ liệu với Label là cột Residual.

### Bước 4:
{: .no_toc }

Giá trị dự đoán từ Leaf Node của Regression Tree mới tạo này chính là $$\gamma_{j,m}$$ - giá trị để Cost Function ở mỗi Leaf Node là nhỏ nhất.

Giải thích:

Hàm Cost Function của mỗi Leaf Node có công thức:

$$Cost = \sum_{x_i \in \mathbb{R}_{j,m}} L(y_i,F_{m-1}(x_i) + \gamma)$$

Lấy Lost Function là MSE:

$$L(y_i,F_{m-1}(x_i) + \gamma) = \frac{1}{2} (y_i - (F_{m-1}(x_i) + \gamma))^2$$

Ta được:

$$Cost = \sum_{x_i \in \mathbb{R}_{j,m}} \frac{1}{2} (y_i - (F_{m-1}(x_i) + \gamma))^2$$

Lấy đạo hàm hàm này:

$$\frac{\partial Cost}{\partial \gamma} = - \sum_{x_i \in \mathbb{R}_{j,m}} (y_i - (F_{m-1}(x_i) + \gamma))$$

Cho hàm này bằng 0 ta được:

$$\begin{align}
\sum_{x_i \in \mathbb{R}_{j,m}} (y_i - (F_{m-1}(x_i) + \gamma)) &= 0 \\
k \gamma &= \sum_{x_i \in \mathbb{R}_{j,m}} (y_i - F_{m-1}(x_i)) \\
\gamma &= \frac{\sum_{x_i \in \mathbb{R}_{j,m}} (y_i - F_{m-1}(x_i))}{k} 
\end{align}$$

Với:

$$k$$: là số phần tử trong Leaf Node

$$y_i - F_{m-1}(x_i)$$: là giá trị của cột Residual

Vậy $$\gamma$$ chính là giá trị trung bình của Leaf Node.

### Bước 5:
{: .no_toc }

Cập nhật $$F_{m-1}$$ thành $$F_{m}$$:

$$F_{m}(x) = F_{m-1}(x) + \nu \gamma$$

Với:
$$\nu$$: là learning rate

$$\gamma$$: là giá trị dự đoán của Leaf Node

$$m$$: là số lượng Tree

### Bước 6:
{: .no_toc }

Lặp lại bước 2,3,4,5 với mỗi lần lặp $$F_m$$ sẽ tăng lên tương ứng với số Regression Tree đã tạo. Đến khi đủ số Regression Tree thì ta dừng thuật toán. 
Kết quả sẽ được dự đoán bằng $$F_M(x)$$.

<hr>

## Gradient Boosting - Classification

(Coming soon - Cái ở dưới sai)

### Bước 1:
{: .no_toc }

Dự đoán tất cả giá trị bằng giá trị xác suất của True ở cột Label, vì giá trị này giúp hàm Cost Function đạt giá trị nhỏ nhất. 

$$F_0 = p$$

Giải thích:

- Hàm Cost Function là hàm  Negative Log Likelihood, có dạng:

$$Cost = -\sum_{i=1}^n (y_i \log {\gamma}_i + (1-y_i) \log (1 - \gamma))$$

- Đạo hàm hàm này ta có:

$$\begin{align}
\frac{\partial Cost}{\partial \gamma} &= -\sum_{i=1}^n \frac{y_i}{\gamma} - \frac{1-y_i}{1-\gamma} \\
\frac{\partial Cost}{\partial \gamma} &= \sum_{i=1}^n \frac{1-y_i}{1-\gamma} - \frac{y_i}{\gamma} \\
\frac{\partial Cost}{\partial \gamma} &= \sum_{i=1}^n \frac{\gamma - y}{(1 - \gamma)(\gamma)}
\end{align}$$

- Cho đạo hàm bằng $$0$$:
	- Cho tử bằng $$0$$:
	$$\begin{align}
	\sum_{i=1}^n (\gamma - y) &= 0 \\
	n\gamma - \sum_{i=1}^n y &= 0 \\ 
	\gamma &= \frac{\sum_{i=1}^n y}{n}
	\end{align}$$
	
	- Đặt điều kiện để mẫu khác $$0$$:
	$$\begin{cases}
  	\gamma &\not = 0 \\
   	\gamma &\not = 1
	\end{cases}$$
	
Nếu để ý kĩ giá trị $$\gamma$$ chính bằng xác suất của True vì tổng của $$y$$ chính là số lần xuất hiện của giá trị True.

### Bước 2:
{: .no_toc }

<hr>

> Tham khảo từ:
>
> [StatQuest: Decision Trees](https://www.youtube.com/watch?v=7VeUPuFGJHk&t=32s)
>
> [Regression Trees, Clearly Explained!!!](https://www.youtube.com/watch?v=g9c66TUylZ4&t=1116s)
>
> [Gradient Boost Part 1: Regression Main Ideas](https://www.youtube.com/watch?v=3CC4N4z3GJc&t=408s)
>
> [Gradient Boost Part 2: Regression Details](https://www.youtube.com/watch?v=2xudPOBz-vs&t=1008s)
>
> [Bài 34: Decision Trees (1): Iterative Dichotomiser 3](https://machinelearningcoban.com/2018/01/14/id3/)
