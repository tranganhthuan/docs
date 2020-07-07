---
layout: default
title: Quan hệ giữa các biến cố
parent: Xác suất
nav_order: 2
---

# Quan hệ giữa các biến cố
{: .no_toc }

## Mục lục
{: .no_toc}

1. TOC
{:toc}

<hr/> 

## Biến cố độc lập (Independence events)
(Chút về viết)

<hr/>

## Biến cố xung khắc (Mutually exclusive chút chỉnh lại)

**Khái niệm:**

Các biến cố $$A_i (i = \overline{1,n})$$ xung khắc với nhau nếu bất kỳ 2 biến cố nào trong nhóm này không thể đồng thời xảy ra trong cùng một phép thử.

**Tính chất:**

$$A$$ và $$B$$ xung khắc <=> $$A.B$$ = rỗng

**Ví dụ:**

Trong một bình có 2 loại quả cầu: cầu trắng và cầu đỏ. Lấy ngẫu nhiên từ bình đó một quả cầu.
- Gọi $$A$$ là biến cố "Lấy được quả cầu trắng".
- Gọi $$B$$ là biến cố "Lấy được quả cầu đỏ".
$$\implies$$ $$A$$ và $$B$$ là hai biến cố xung khắc.

**Bổ sung:**

Xung khắc từng đôi thực chất là một cách nói đầy đủ khi nói về xung khắc của nhiều biến cố để nhấn mạnh sự xung khắc.

<hr/>

## Biến cố đối lập ()

**Khái niệm:**

Các biến cố $$A_i (i = \overline{1,n})$$ gọi là đối lập với nhau nếu hợp của chúng tạo nên một nhóm biến cố đầy đủ.

**Tính chất:**

$$A_i (i = \overline{1,n})$$ đối lập <=>  $$\sum_{i=1}^n A_i = \Omega$$ và $$A.\bar{A} = \text{\O}$$

**Ví dụ:**

Gọi:
- $$A$$ là biến cố "Tung xúc xắc được mặt $${1}$$"
- $$B$$ là biến cố "Tung xúc xắc được mặt là số nguyên tố - $${2,3,5}$$"
- $$C$$ là biến cố "Tung xúc xắc được mặt chẵn - $${2,4,6}$$"
$$\implies$$ $$A$$,$$B$$ và $$C$$ là các biến cố đối lập. 

