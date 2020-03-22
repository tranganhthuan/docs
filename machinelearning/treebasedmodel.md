---
layout: default
title: Tree based model
nav_order: 3
parent: Machine Learning
---

# Treebased 
{: .no_toc }

Ở bài này ta sẽ cùng làm quen với một số model dự đoán bằng cách đặt các câu hỏi.

<hr/>

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Decision Tree - Classification
Đây là thuật toán đơn giản nhất trong các tree-based model, làm nền tảng cho các thuật toán sau này.

Một số thuật ngữ cơ bản:
![](https://miro.medium.com/max/592/0*X-UrBzBeKMnoTY6H.png)


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


>Công thức gini index: 
>
>$$1 - \sum_{i=1}^{n} p_i^2$$ 
>
>Công thức entropy:
>
>$$ - \sum_{i=1}^{n} p_i log(p_i)$$ 

Ví dụ ta tính gini index cho cột **Học bài** ở bảng trên.

Từ 2 cột **Học bài** và **Qua môn**, ta được 2 node: Đậu và Rớt như sau:
- Node Đậu bao gồm: có - 3, không - 1. Với Gini index = $$1 -(0.75^2 + 0.25^2) = 0.375$$
- Node Rớt bao gồm: có - 1, không - 1. Với Gini index = $$1 -(0.5^2 + 0.5^2) = 0.5$$

Sau đó lấy trung bình có trọng số của 2 node này $$\frac{4}{6}0.375 + \frac{2}{6}0.5 = 0.4$$

$$0.4$$ chính là Gini index của cột **Học bài**. 

Tương tự, ta được Gini index của cột **Thành tích** là

