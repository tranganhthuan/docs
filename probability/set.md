---
layout: default
title: Tập hợp
parent: Xác suất
nav_order: 2
---

# Tập hợp
{: .no_toc }

## Mục lục
{: .no_toc}

1. TOC
{:toc}

<hr/> 

## Các phép toán tập hợp (Set operations)

### Phép hợp (Union)
{: .no_toc }

**Khái niệm:** 

Cho $$A$$ và $$B$$ là hai biến cố bất kì, hợp của $$A$$ và $$B$$, là biến cố chứa tất cả các kết quả hoặc chỉ thuộc về $$A$$, hoặc chỉ thuộc về $$B$$, hoặc thuộc về cả $$A$$ lẫn $$B$$. Do vậy, biến cố này xảy ra khi có ít nhất $$A$$ hoặc $$B$$ xảy ra.

**Ký hiệu:**

$$A \cup B$$ hoặc $$A + B$$

**Ví dụ:**

- $$A$$ là biến cố: "Tung xúc xắc ra được mặt 1 chấm"

- $$B$$ là biến cố: "Tung xúc xắc ra được mặt 2 chấm"

- $$A \cup B$$ là biến cố: "Tung xúc xắc ra được mặt 1 chấm hoặc 2 chấm"

### Phép giao (Intersection)

**Khái niệm:** 
Cho A và B là hai biến cố bất kì, giao của A và B, là biến cố chứa tất cả các kết quả cùng thuộc về cả A lẫn B. Do vậy, biến cố này xảy ra khi cả A và B cùng xảy ra.

**Ký hiệu:** 

$$A \cap B$$ hoặc $$A.B$$

**Ví dụ:**

- $$A$$ là biến cố: "Tung xúc xắc ra được mặt chẵn chấm".
- $$B$$ là biến cố: "Tung xúc xắc ra được mặt nhỏ hơn 3 chấm".
- $$A \cap B$$ là biến cố: "Tung xúc xắc ra được mặt 2 chấm".

### Phép bù (Complement)

**Khái niệm:** 

Cho A là biến cố bất kì, bù của A là biến cố chứa tất cả biến cố trong không gian mẫu S nhưng không thuộc về A.

**Ký hiệu:**

$$\bar{A}$$ hoặc $$A^c$$

**Ví dụ:**

- $$A$$ là biến cố: "Tung xúc xắc ra được mặt 1 chấm".
- $$\bar{A}$$ là biến cố: "Tung xúc xắc ra được mặt lớn hơn 1 chấm".


### Tổng kết 
{: .no_toc }

![](/assets/images/probability/img_1.png)

<hr/> 

## Tính chất

| Giao hoán | $$A \cup B = B \cup A$$<br>$$A \cap B = B \cap A$$ |
|:-:|:-:|
| Kết hợp | $$A \cup (B \cup C) = (A \cup B) \cup C$$<br>$$A \cap (B \cap C) = (A \cap B) \cap C$$ |
| Phân phối | $$A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$$<br>$$A \cup (B \cap C) = (A \cup B) \cap (A \cup C)$$ |
| Phần bù | $$\bar{\bar{A}} = A$$<br>$$\overline{A \cup B} = \bar{A} \cap \bar{B}$$<br>$$\overline{A \cap B} = \bar{A} \cup \bar{B}$$ |
