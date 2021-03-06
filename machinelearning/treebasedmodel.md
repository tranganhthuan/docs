---
layout: default
title: Tree based model
nav_order: 3
parent: Machine Learning
published: false
---

# Treebased model
{: .no_toc }

Ở bài này ta sẽ cùng làm quen với một số model dự đoán bằng cách đặt các câu hỏi.

<hr/>

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Decision Tree

Decision Tree (Cây quyết định) là một hệ thống gồm các câu hỏi có dạng giống như cây nhị phân. Với root node và decision node là các câu hỏi và leaf node là quyết định được đưa ra (thuật ngữ ở hình bên dưới). 
![](https://miro.medium.com/max/592/0*X-UrBzBeKMnoTY6H.png)

Đây giống như cách mà con người đưa ra quyết định, chính vì lý do này mà người ta thường dùng Decision Tree để hiểu thêm về tập dữ liệu. Ví dụ như để đánh giá một học sinh có học lực như thế nào ta sẽ có Decision Tree sau đây:
![](/assets/images/tree_example.png)

## Decision Tree - Classification

Đây là thuật toán đơn giản nhất trong các tree-based model, làm nền tảng cho các thuật toán sau này.

Ví dụ ta có bảng về các học sinh như sau:

| Học bài | Thành tích | Qua môn |
|:-------:|:----------:|:-------:|
| Có | Kém | Không |
| Không | Tốt | Không |
| Có | Tốt | Có |
| Có | Kém | Có |
| Có | Kém | Có |
| Không | Tốt | Có |

Lần này ta sẽ dự đoán một học sinh có qua môn hay không dựa vào yếu tố học sinh có học bài trước khi thi không và thành tích có học sinh này.

Model dự đoán cho dữ liệu trên sẽ có dạng như sau:
![](/assets/images/tree.png)

Trước tiên, thuật toán sẽ tìm ra câu hỏi tốt nhất - câu hỏi sẽ chia được nhiều dữ liệu nhất. Vậy làm sao để model có thể đánh giá được câu hỏi là tốt hay không. Để làm được điều này ta tìm hiểu 2 phương pháp đánh giá là: Gini index và Entropy.


>Công thức Gini index: 
>
>$$1 - \sum_{i=1}^{n} p_i^2$$ 
>
>Công thức Entropy:
>
>$$ - \sum_{i=1}^{n} p_i log(p_i)$$ 

Ví dụ ta tính gini index cho cột **Học bài** ở bảng trên.

Từ 2 cột **Học bài** và **Qua môn**, ta được 2 node: Đậu và Rớt như sau:
- Node Đậu bao gồm: có - 3 ($$p = 3/(3+1) = 0.75$$), không - 1 ($$p = 1/(3+1) = 0.25$$). Với Gini index = $$1 -(0.75^2 + 0.25^2) = 0.375$$
- Node Rớt bao gồm: có - 1 ($$p = 1/(1+1) = 0.5$$), không - 1 ($$p = 1/(1+1) = 0.5$$). Với Gini index = $$1 -(0.5^2 + 0.5^2) = 0.5$$

>Công thức trung bình có trọng số (weighted mean):
>
> $$\sum_{i=1}^{n} w_i x_i$$
>
> Với $$w_i = n_{child}/n_{parent}$$, $n_{child}$ là số phần tử của node child sau khi chia, $n_{parent}$ là số phần tử của node parent trước khi chia

Sau đó lấy trung bình có trọng số của 2 node này $$\frac{4}{6}0.375 + \frac{2}{6}0.5 = 0.4$$

$$0.4$$ chính là Gini index của cột **Học bài**. 

Tương tự, ta được Gini index của cột **Thành tích** là: $$0.5$$

Ta chọn cột có Gini index thấp nhất để làm câu hỏi. Làm tương tự với Entropy.

> Mở rộng ra:
> - Nếu giá trị của cột trên là categorical, thì ta $$p_i$$ sẽ là xác suất của mỗi category.Tính Gini index/Entropy chia theo mỗi category rồi chọn category có kết quả thấp nhất.
> - Nếu giá trị trên là số phải sắp xếp theo thứ tự cái giá trị trong cột. Rồi tính giá trị trung bình giữa 2 phần tử kế tiếp có giá trị khác nhau. Với mỗi giá trị trung bình, ta tính Gini index hoặc Entropy. Kết quả thấp nhất sẽ là Gini index hoặc Entropy của cột.

Ví dụ:
Thành tích ở bảng trên được tính bằng số:

| Thành tích | Qua môn |
|:----------:|:-------:|
| 4 | Không |
| 7 | Không |
| 8 | Có |
| 4 | Có |
| 4 | Có |
| 7 | Có |

Sắp xếp lại dữ liệu (4,7,8) và lấy trung bình, ta được 2 giá trị: 5.5, 7.5.
- Trường hợp 5.5 ta có Gini index $$=0.5$$  
- Trường hợp 7.5 ta có Gini index $$=0.25$$
Vậy cột **Thành tích** (nếu là số) sẽ có Gini index = 0.2.

Với các tập con sau khi được chia, thuật toán sẽ tiếp tục tìm, đặt câu hỏi và chia nhỏ tập dữ liệu như trên cho đến khi tập trên cho đến khi mỗi leaf chỉ còn chứa 1 class duy nhất hoặc không thể chia được nữa (có attribute giống nhau hoàn toàn nhưng label khác nhau).

>Tổng kết lại, thuật toán Decision Tree làm các bước sau:
> - Bước 1: Tính Gini index/Entropy của từng features. Để tìm ra câu hỏi tốt nhất.
>   - Tính Gini index/Entropy của từng node leaf khi đã chia. 
>   - Trung bình có trọng số của các node leaf.
>   - Chọn câu hỏi có kết quả nhỏ nhất.
> - Bước 2: Áp dụng Bước 1 cho 2 tập con vừa mới được chia. Cho đến khi chỉ còn 1 class trong leaf hoặc không thể chia được nữa.

## Decision Tree - Regression

Nếu bây giờ mô hình của chúng ta không chỉ đưa ra những class cụ thể (hữu hạn), mà phải dự đoán các số liệu (vô hạn) thì ta phải làm sao. Điều này không khó như bạn nghĩ. Ta chỉ cần thay đổi hàm sai số từ Gini index/Entropy thành MSE (Mean squared error). Và dùng giá trị trung bình của các phần tử trong leaf làm giá trị để dự đoán.

> Công thức MSE:
> 
> $$\frac{1}{n} \sum_{i=1}^{n} (f(x_i) - y_i)^2$$

Ta cùng áp dụng vào tập dữ liệu sau đây:

| Chương | Điểm |
|:------:|:----:|
| 7 | 10 |
| 8 | 10 |
| 4 | 5 |
| 2 | 2 |
| 5 | 7 |
| 3 | 2 |

Với cột chương là số chương học sinh đã học, dựa vào số liệu này ta sẽ đoán điểm số của học sinh đó.

Vẽ sơ đồ các điểm trên:

![](/assets/images/plot 1.png)

Tiếp theo ta cũng chia node thành 2 node nhỏ hơn như Decision Tree - Classification. (Giống như trên ta sắp xếp các giá trị theo thứ tự rồi lấy giá trị trung bình của 2 dòng liên tiếp có giá trị khác nhau.)

![](/assets/images/plot 2.png)

Ở hình trên ta thấy dữ liệu được chia thành 2 node:
- Node 1: Gồm dòng thứ 4 với giá trị [2,2].
- Node 2: Gồm các dòng còn lại.

Đi tính giá trị trung bình của từng node ta được: $$mean_1 = 2$$, $$mean_2 = (10+10+5+7+2)/5 = 6.8$$. 

Áp dụng MSE vào để tính trung bình tổng khoảng cách từ mỗi điểm trong node để mean của nó.

- Node 1: $$(2 - 2)^2 = 0$$
- Node 2: $$(10 - 6.8)^2 + (10 - 6.8)^2 + (5 - 6.8)^2 + (7 - 6.8)^2 + (2 - 6.8)^2 = 46.8$$

Vậy MSE của cách chia thứ nhất là $$0+46.8 = 46.8$$.

Làm tương tự với các giá trị còn lại, MSE nhỏ nhất được lấy làm MSE của cột. 

Nếu ngoài cột **Chương** ta còn các cột khác thì ta cũng áp dụng MSE với cái category(nếu là categorical) hoặc giá trị trung bình (nếu là số) trong các cột đó.

Sau khi tính được hết tất cả MSE của các cột, ta so sánh và chọn ra MSE nhỏ nhất để đặt câu hỏi.

Tiếp tục, làm vậy với các node sau khi được chia cho đến khi leaf node chỉ còn các giá trị giống nhau hoặc không chia được nữa.

> Tổng kết lại ta thấy cách hoạt động của Decision Tree Regression giống hệt Classification, chỉ khác ở 2 điểm:
> - Thứ nhất: Hàm dùng để đánh giá câu hỏi là hàm MSE.
> - Thứ hai: Giá trị dự đoán là trung bình các giá trị trong leaf.

## Pruning Decision Tree

Trong thực tế, nếu ta để cho decision tree tự phân chia sẽ dẫn đến overfitting, để tránh việc này ta cần phải pruning decision tree (tỉa cành lá - loại bỏ các leaf node không cần thiết).

Có 2 cách đơn giản để pruning decision tree:
**Reduced error pruning:**

Ta chia dataset ra làm 2 tập - trainning set, validation set. Ta fit Decision Tree vào tập training rồi tính score trên tập valition. Nếu thấy bị overfitting, ta bỏ bớt các leaf node, từ dưới lên. Ta cứ tỉa bớt rồi thử lại cho đến khi điểm của validation không còn cải thiện được nữa.
**Cost complexity pruning:**

Ở cách làm này ta có cost function như sau:

$$L = \sum_{i=1}^n w_i l_i + \lambda*\text{num_leaf}$$

Với: 

$$w_i = n_i/N$$: là tỉ lệ giữa số lượng phần tử có trong node với tổng số phần tử

$$l_i$$: là loss của node i

$$\text{num_leaf}$$: là số lượng node leaf

Để tối ưu được hàm này, ta không thể dùng đạo hàm mà phải thử trên từng node leaf để xem model nào cho kết quả tốt nhất.

> Tổng kết lại có 2 cách đơn giản để pruning:
> - **Reduced error pruning:** đối chiếu score của model của 2 tập training set và validation set với nhau khi loại bỏ các node. 
>
> - **Cost complexity pruning:** dùng lost function $$L = \sum_{i=1}^n w_i l_i + \lambda*\text{num_leaf}$$ để đánh giá model khi loại bỏ các node.

## Random Forest

Như đã biết, decision tree gặp phải vấn đề overfiting - mặc dù fit rất tốt với dữ liệu được học nhưng khó khăn khi dự đoán dữ liệu mới. Random Forest giải quyết tốt vẫn đề này và nó vẫn giữ lại được tính dễ hiểu của Decision Tree. Như tên gọi, Random Forest là gồm nhiều model Decision Tree. Để tạo ra nhiều dữ liệu cho các model này ta dùng một kỹ thuật gọi là **Boosttrap Sampling* - lấy mẫu có hoàn lại.

> Boostrap Sampling - lấy mẫu có hoàn lại - là một kĩ thuật của Thống kê. Ta lấy một ngẫu nhiên cá thể trong tập mẫu gốc sau đó hoàn lại. Lặp lại n lần ta sẽ được một boostrapped sample có size bằng n. 

Ví dụ, ở phần trước ta có bảng sau:

**Original Dataset**

| Chương | Điểm |
|:------:|:----:|
| 7 | 10 |
| 8 | 10 |
| 4 | 5 |
| 2 | 2 |
| 5 | 7 |
| 3 | 2 |

Ta lấy dòng 2,3,5,5,6,6 ra để tạo 1 boostrapped dataset có size bằng với dataset ban đầu. Thì dataset này sẽ có dạng.

**Boostrapped Dataset**

| Chương | Điểm |
|:------:|:----:|
| 8 | 10 |
| 4 | 5 |
| 5 | 7 |
| 5 | 7 |
| 3 | 2 |
| 3 | 2 |

Với $$k$$ boostrapped dataset ta sẽ có $$t$$ Decision Tree khác nhau. Tuy nhiên, những Decision Tree này chỉ chọn random $$k$$ features có trong boostrapped dataset ở mỗi bước.

Ví dụ, ta có một boostrapped dataset như sau:

| Đau tim | Ho | Nhức đầu | Kết luận |
|:-------:|:-----:|----------|-------------|
| Không | Có | Có | Bệnh X |
| Có | Không | Có | Bình thường |
| Có | Có | Có | Bệnh X |

Thì với $$k$$ bằng 2 thì Decision Tree của data set này chỉ chọn ngẫu nhiên 2 trong 3 features trên (đau tim - ho hoặc ho - nhức đầu hoặc đau tim - nhức đầu) ở mỗi bước. $$k$$ thường được chọn bằng $$\sqrt(n)$$ với $$n$$ là tổng số features.

Mỗi kết quả dự đoán (Classification) sẽ được vote bởi các Decision Tree, kết quả cuối cùng sẽ là kết quả có nhiều lược vote nhất. Còn đối với Regression, kết quả cuối cùng sẽ bằng trung bình cộng kết quả của các Decision Tree.

Ngoài ra, ở quá trình boostrap sampling, ta thấy boostrapped dataset có độ lớn bằng original dataset nhưng có những giá trị trùng, điều này có nghĩa là có một số dữ liệu tồn tại trong original dataset nhưng không có trong boostrapped dataset. Những điểm dữ liệu này được gọi là **Out-of-Bag** datasets. Với mỗi điểm dữ liệu, ta dùng những Decision Tree không chứa nó khi training để dự đoán. Tỉ lệ dự đoán đúng với tổng số lần dự đoán cũng chính là độ chính xác (accuracy) của model. Còn độ sai lệch (1 - độ chính xác) được gọi là **Out-of-Bag Error**. 

## Ada Boost

Như ta đã thấy ở Random Forest mỗi Decision Tree đều có đóng góp bằng nhau, điều này đôi khi không hiệu quả vì các tree có độ chính xác khác nhau. Ada Boost đã cải tiến điều này bằng cách tin tưởng vào những tree có độ chính xác cao (những tree có độ chính xác cao thì kết quả sẽ được xem trọng hơn), và đối với những tree hay dự đoán sai thì Ada Boost sẽ lấy kết quả ngược lại với kết quả của những tree này. 

Đầu tiên, chúng ta cùng tìm hiểu thuật ngữ **Week Learner**. Khác với Random Forest, mỗi tree trong Ada Boost chỉ gồm có 1 node và 2 leaf,được gọi là **stump(gốc cây)**. Bởi vì mỗi stump chỉ có thể đưa ra quyết định dựa vào 1 feature nên nó được xem là **Weak Learner**.
