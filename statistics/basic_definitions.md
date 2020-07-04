---
layout: default
title: Khái niệm chung
parent: Thống kê
nav_order: 1
---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Các khái niệm cơ bản

### Thống kê, Thống kê mô tả và Thống kê suy luận
{: .no_toc }
- Thống kê (Statistics): Là ngành khoa học nghiên cứu về thu thập, sắp xếp và phân tích dữ liệu.
- Thống kê mô tả (Descriptive Statistics): Là loại thống kê liên quan đến việc tổ chức, tổng kết và trình bày dữ liệu một cách có ý nghĩa.
- Thống kê suy luận (Inferential Statistics): Là loại thống kê liên quan đến việc đưa ra kết luận về tổng thể dựa trên mẫu nghiên cứu.

### Tổng thể và Mẫu
{: .no_toc }
- Tổng thể (Population): Là tập hợp tất cả các phần tử của đối tượng cần nghiên cứu.
- Mẫu (Sample): Là một phần của mẫu được trích ra để nghiên cứu.

### Một số cách lấy mẫu (Sampling Methods)
{: .no_toc }
** Để sau **

## Giá trị trung tâm của dữ  (Measures of Central Tendency)

### Trung bình (Mean)
{: .no_toc }
**Định nghĩa:**

Là tổng giá trị của các phần tử chia cho tổng số phần tử.
**Cách tính:**

Tính theo công thức:

$$\text{mean} = \frac{\sum{\mathbf{X}}}{N} $$

### Trung vị (Median)
{: .no_toc }

**Định nghĩa:**

Là điểm chính giữa của dữ liệu.

**Cách tính:**liệu
Tính theo công thức:

$$\text{median} = \frac{X_{n/2} + X_{(n+2)/2}}{2}$$

**Định nghĩa:**

Là điểm xuất hiện nhiều nhất trong dữ liệu.

**Cách tính:**

Sắp xếp dữ liệu theo thứ tự. Đếm số phần tử trong từng đoạn giống nhau. Tìm ra phần tử có số đếm cao nhất.

## Phân vị:

### Tứ phân vị (Quartiles)
{: .no_toc }

**Định nghĩa:**

Tứ phân vị có 3 giá trị, đó là tứ phân vị thứ nhất, thứ nhì, và thứ ba. Ba giá trị này chia một tập hợp dữ liệu (đã sắp xếp dữ liệu theo trật từ từ bé đến lớn) thành 4 phần có số lượng quan sát đều nhau.

**Cách tính:**

Tính theo công thức:

$$Q1 = X_{(n+1)*1/4}$$
$$Q2= \frac{X_{n/2} + X_{(n+2)/2}}{2}$$
$$Q3 = X_{(n+1)*3/4}$$	

### Bách phân vị (Percentiles)
{: .no_toc }

**Định nghĩa:** 

Số phân vị thứ P là một giá trị mà tại đó nhiều nhất có P% số trường hợp quan sát trong tập dữ liệu có giá trị thấp hơn giá trị này.

**Cách tính:**

Tính theo công thức:
$$\# \text{ rank} = 100*(\frac{\#\text{ of values below x} + 0.5}{\text{Total } \# \text{ of values}})$$


## Độ phân tán của dữ liệu (Measures of Variation):

### Khoảng (Range)
{: .no_toc }

**Định nghĩa:**

Là khoảng giá trị của dữ liệu.

**Cách tính:**

Tính theo công thức:

$$\text{range} = max(X) - min(X)$$

### Khoảng tứ phân vị (Inter-quartile Range)
{: .no_toc }

**Định nghĩa:**

Là khoảng giá trị giữa tứ phân vị 1 và tứ phân vị 3.

**Cách tính:**

Tính theo công thức:

$$IQR = Q1 - Q3$$

**Áp dụng:**
- Từ Q1, Q3, IQR ta có thể tính được:

$$\text{low} = Q1 - 1.5*IQR$$

$$\text{high} = Q3 + 1.5*IQR$$

- Giá trị nằm ngoài khoảng $$[low,high]$$ được coi là điểm bất thường (outlier).

- low, Q1, Q2, Q3, high là 5 điểm thường được dùng để mô tả dữ liệu (5-number summary).

## Các đại lượng đặc trưng của tổng thể và mẫu

|  | Tổng thể | Mẫu |
|-|-|-|
| Trung bình (Mean) | $$\mu = \frac{\sum_{i=1}^N x_i}{N}$$ | $$\bar{X} = \frac{\sum_{i=1}^n x_i}{n}$$ |
| Phương sai (Variance) | $$\sigma^2 = \frac{\sum_{i=1}^N (x_i - \bar{X})^2}{N}$$ | $$s^2 = \frac{\sum_{i=1}^n (x_i - \bar{X})^2}{n-1}$$ |

**Bổ sung:**

- $$\sigma$$ được gọi là Độ lệch chuẩn (Standard Deviation).
- $$s$$ được gọi là Sai số chuẩn (Standard Error).

## Độ lệch (Skewness)

### Phân phối đối xứng (Symmetrical Distribution)
{: .no_toc }
**Định nghĩa:**

Phân phối của tập dữ liệu đối xứng khi:

$$Q2-Q1 = Q3-Q1$$

hoặc

$$mode = median = mean$$


### Độ lệch dương (Positive Skew - Right Skew)
{: .no_toc }

**Định nghĩa:**

Phân phối của tập dữ liệu lệch phải khi:

$$Q2-Q1 > Q3-Q1$$

hoặc

$$mode > median > mean$$

### Độ lệch âm (Negative Skew - Left Skew)
{: .no_toc }

**Định nghĩa:**

Phân phối của tập dữ liệu lệch trái khi:

$$Q2-Q1 < Q3-Q1$$

hoặc

$$mode < median < mean$$
