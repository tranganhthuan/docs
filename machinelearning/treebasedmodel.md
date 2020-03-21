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
Đây là thuật toán đơn giản nhất trong các tree-based model, làm tiền đề cho các thuật toán sau này.

Ví dụ ta có bảng về các học sinh như sau:

| Học bài | Thành tích | Qua môn |
|:-------:|:----------:|:-------:|
| Có | Thấp | Không |
| Không | Cao | Không |
| Có | Cao | Có |
| Có | Không | Có |
| Có | Cao | Có |

Lần này ta sẽ dự đoán một học sinh có qua môn hay không dựa vào yếu tố học sinh có học bài trước khi thi không và thành tích có học sinh này.

Model dự đoán cho dữ liệu trên sẽ có dạng như sau:


Trước tiên, thuật toán sẽ tìm ra câu hỏi tốt nhất - câu hỏi sẽ chia được label 



