---
layout: default
title: Quan hệ giữa các biến cố
parent: Xác suất
nav_order: 3
---

# Quan hệ giữa các biến cố
{: .no_toc }

## Mục lục
{: .no_toc}

1. TOC
{:toc}

<hr/> 

## Biến cố độc lập (Independence events)

### Biến cố độc lập (Independence events)
{: .no_toc }

**Khái niệm:**

Các biến cố $$A_i (i = \overline{1,n})$$ được gọi là độc lập với nhau nếu việc xảy ra hay không xảy ra của một biến cố không làm thay đổi xác suất xảy ra của các biến cố khác và ngược lại.

**Phân loại:**

Biến cố độc lập có 2 loại: 
- Độc lập từng đôi (pairwise independent) 
- Độc lập toàn phần(mutual independence/collective independence). 

**Ví dụ:**

Tung đồng xu nhiều lần:
Gọi $$A_i$$ là biến cố "Tung được mặt ngửa khi tung đồng xu lần thứ i".
$$implies$$ Các biến cố $$A_i$$ độc lập với nhau.

### Độc lập từng đôi (Pairwise independence):
{: .no_toc }

**Khái niệm:**

Các biến cố $$A_i (i = \overline{1,n})$$ được gọi là độc lập từng đôi với nhau nếu 2 biến cố bất kỳ trong n biến cố đó độc lập với nhau. 

**Công thức:**

Các biến cố $$A_i$$ độc lập từng đôi nếu chúng thỏa mãn điều kiện sau:
	$$P(A_i \cap A_j) = P(A_i)P(A_j)\quad\forall i,j =\overline{1,n}, i \ne j$$

**Ví dụ:**

Tung đồng xu đều đồng chất. Cho 3 biến cố sau:
- Biến cố $$A$$: Tung được mặt ngửa ở lần thứ nhất.
- Biến cố $$B$$: Tung được mặt ngửa ở lần thứ hai.
- Biến cố $$C$$: Mặt đồng xu giống nhau ở hai lần tung.
$$3$$ biến cố $$A,B,C$$ độc lập từng phần với nhau vì tuy $$A$$ độc lập với $$B$$, $$B$$ độc lập với $$C$$ và $$C$$ độc lập với $$A$$, nhưng $$A$$ không độc lập với $$B \cap C$$.
Cụ thể:
- Nếu $$A$$ đã xảy ra - lần thứ 1 tung được mặt ngửa, ta không biết lần thứ 2 có được mặt ngửa hay không ($$B$$) hoặc mặt đồng xu ở 2 lần tung có giống nhau hay không ($$C$$). Tương tự nếu $$B$$, $$C$$ xảy ra trước.
-  Tuy nhiên, nếu $$A$$ và $$B$$ đã xảy ra ta có thể nói được 2 mặt là giống nhau và ngược lại ($$C$$). Điều này có nghĩa hợp của $$A$$, $$B$$ đã làm thay đổi xác suất của $$C$$. Tương tự với trường hợp $$A \cap C$$ hoặc $$B \cap C$$ xảy ra.

### Độc lập toàn phần (Mutual independence/collective independence):
{: .no_toc }

**Khái niệm:**

Các biến cố $$A_i (i = \overline{1,n})$$ gọi là độc lập toàn phần với nhau nếu mỗi biến cố đó độc lập với một tổ hợp bất kỳ các biến cố còn lại.

**Công thức:**

Các biến cố $$A_i$$ độc lập từng đôi nếu chúng thỏa mãn 2 điều kiện sau:
- $$P(A_i \cap A_j) = P(A_i)P(A_j)\quad\forall i,j =\overline{1,n}, i \ne j$$
- $$P(\sum_{i=1}^n A_i) = \sum_{i=1}^nP(A_i)$$

**Ví dụ:**

Tung một con xúc xắc đều đồng chất. Các biến cố tung được mặt 1 chấm ở lần thứ $$i$$ là các biến cố độc lập toàn phần với nhau vì dù ta biết kết quả của một hay nhiều lần tung, thì xác suất của các lần tung còn lại cũng không thay đổi.

<hr/>

## Biến cố xung khắc (Mutual exclusivity)

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

## Biến cố đối lập (Partition of a set)

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

