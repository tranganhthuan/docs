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


## Decision Tree - Classification:
- Bước 1: Tính Impurity của từng Features bằng cách chia 2 node, rồi tính $$p_i$$ của cột label ứng với 2 node này.
  - Công thức Gini Index:
	
   $$\text{Gini} = 1 - \sum_{i = 1}^n p_i$$
	
  - Công thức Entropy:
	
    $$E(p_i) = -\sum_{i=1}^n p_i \log(p_i)$$
	
  - Với: 
	  - Trường hợp Label là **true/false**: 

	  - Trường hợp Label là **category**: 
	    
      $$p_i = p(y = y_i | x = x_i) = \frac{k_i}{n}$$
	
      - $$k_i$$: là số phần tử có label là $$k_i$$
      
      - $$n$$: tổng số phần tử node hiện tại
      
- Số cách chia dựa vào values của cột Features:
	- Trường hợp 1 (boolean): Chia theo True/False có 1 trường hợp.
	- Trường hợp 2 (category): Chia theo Category(One/Rest) có c trường hợp ứng với số categories.
	- Trường hợp 3 (number): Sắp xếp thứ
- Chọn câu hỏi có Entropy/ Gini Index nhỏ nhất.
