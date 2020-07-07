---
layout: default
title: Các công thức cơ bản
parent: Xác suất
nav_order: 4
---

# Các công thức cơ bản
{: .no_toc }

## Mục lục
{: .no_toc}

1. TOC
{:toc}

<hr/> 

## Xác suất có điều kiện:

**Khái niệm:**

Xác suất của biến cố $$A$$ được tính với điều kiện biến cố $$B$$ đã xảy ra gọi là xác suất của $$A$$ với điều kiện $$B$$ hoặc xác suất có điều kiện của $$A$$.

**Ký hiệu:** 

$$P(A/B)$$

**Ví dụ:**

Bệnh X có tỉ lệ mắc bệnh là 1/1000 (cứ 1000 người thì sẽ có 1 người bị chuẩn đoán là mắc bệnh). Một máy chuẩn đoán bệnh có độ chính xác là 95%, nghĩa là trong 100 người chuẩn đoán là mắc bệnh thì sẽ có 95 người thật sự mắc bệnh. 
Trong trường hợp trên 95% là xác suất bệnh nhân bị mắc bệnh X với điều kiện họ đã được máy chuẩn đoán là mắc bệnh.

## Nhân xác suất:

**Khái niệm:**

Xác suất của tích hai biến cố $$A$$ và $$B$$ bằng tích xác suất của một trong hai biến cố của một trong hai biến cố đó với xác suất có điều kiện của biến cố còn lại.

**Công thức:**

$$P(A.B) =  P(A).P(B/A) = P(B).P(A/B)$$

**Lưu ý:**

Nếu hai biến cố $$A$$ và $$B$$ độc lập thì:

$$P(A.B) = P(A).P(B)$$

**Ví dụ:**

Trong 1 bình có 5 quả cầu trắng và 3 quả cầu đen. Lấy ngẫu nhiên lần lượt 2 quả cầu. Tính xác suất để lấy được 2 quả cầu trắng. Biết rằng các quả cầu được lấy không hoàn lại.
Xác suất lấy được thứ nhất là quả cầu màu trắng: $$\frac{5}{8}$$ (5 quả cầu trắng trong số 8 quả cầu)
Xác suất lấy được thứ hai là quả cầu màu trắng: $$\frac{4}{7}$$ (1 quả cầu trắng đã bị lấy đi nên trong bình còn lại 4 quả cầu trắng trong số 7 quả cầu)
