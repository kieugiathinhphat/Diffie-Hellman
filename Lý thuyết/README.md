<center> <h1>
     Diffie-Hellman
    </h1></center>
    
# Lý thuyết Nhóm
## Phép toán hai ngôi
Trong toán học, một phép toán hai ngôi là phép toán sử dụng hai biến đầu vào và cho ra một kết quả. Kết quả đó phải nằm cùng một tập hợp với hai biến đầu vào, tức là phép toán hai ngôi là trên tập $S$ là một tích Descartes $S \times S$ vào $S$: $f:S\times S\rightarrow S$
Nên theo định nghĩa đó, phép cộng và nhân là một phép toán hai ngôi trên tập $\mathbb{N, Z, Q, I, R, C}$. Nhưng phép trừ trên tập $\mathbb{N}$ sẽ không phải là phép toán hai ngôi. Tương tự vậy, phép chia trên tập $\mathbb{Z}$ không phải là phép toán hai ngôi.
## Nhóm
Với một tập $\mathbb{G}$, và một phép toán hai ngôi $\circ$ trên $\mathbb{G}$, ta gọi $(\mathbb{G}, \circ)$ là một nhóm khi $\forall a,b,c \in \mathbb{G}$ thỏa các tính chất:
- $a \circ b \in \mathbb{G}$
- $(a \circ b) \circ c = a \circ (b \circ c)$
- Tồn tại $e$ sao cho $a \circ e = e \circ a = a$
- $a^{-1} \circ a = a \circ a^{-1} = e$
> Nhóm $(\mathbb{G}, \circ)$ được gọi là nhóm Abel (nhóm giao hóa) khi phép toán hai ngôi đó có tính giao hoán, tức là $a \circ b = b \circ a$
> Cho nhóm $(\mathbb{G}, \circ)$, một tập con $\mathbb{H}$  được gọi là nhóm con khi $\mathbb{H}$ cũng là một nhóm với phép toán  $(\circ)$

## Nhóm Cyclic
Một nhóm $\mathbb{G}$ được gọi là nhóm Cyclic nếu trong $\mathbb{G}$ tồn tại phần tử $g$ sao cho $G = ⟨g⟩ = \left\{ g^{n} \hspace{2mm}|\hspace{2mm} n \in \mathbb{Z} \right\}$. Lúc này phần tử $g$ sẽ được gọi là phần tử sinh của nhóm.
## Bậc của nhóm, phần tử
Bậc của nhóm $G$ là số phần tử $G$, ký hiệu là $|G|$
Bậc của phần tử $a$ là số nguyên dương $m$ nhỏ nhất thỏa $a^m = e$
Ta sẽ có những tính chất, định lý sau:
- $\forall a \in G$, $ord(a)$ là ước của $|G|$
- Nếu $ord(a)$ = $G$, $a$ là phần tử sinh của $G$
- Nếu $H$ là một nhóm con của $G$, $|H|$ cũng là một ước của $|G|$ (định lý Lagrange)
# Diffie-Hellman
Diffie-Hellman là một giao thức trao đổi khóa, cho phép hai bên tự thiết lập một khóa bí mật chung thông qua một kênh truyền tin công khai (nơi mà kẻ tấn công có thể nghe lén được mọi thứ) mà không cần gặp mặt trực tiếp.
Cách hoạt động của giao thức này về cơ bản như sau:
Giả sử ta có hai người là Alice và Bob cần trao đổi với nhau.
Alice và Bob thỏa thuận dùng chung một nhóm $G$ cyclic, cụ thể là nhóm nhân $\mathbb{Z_p}$ họ chọn một phần tử sinh là $g$, phần tử này sẽ được công khai với tất cả mọi người
Alice sẽ chọn ngẫu nhiên một số $a$ bí mật (chỉ Alice biết) rồi gửi giá trị $g^a \pmod p$ cho Bob
Bob thì cũng chọn ngẫu nhiên một $b$ bí mật rồi gửi đi $g^b \pmod p$
Sau khi đã trao đổi xong, họ lần lượt tính toán như sau:
Alice lấy giá trị mình nhận được, là $g^b \pmod p$ đem mũ cho số bí mật của mình là $a$, thì sẽ nhận được $g^{ab} \pmod p$
Bob cũng làm tương tự, lấy $g^a \pmod p$ mũ a lên thành $g^{ba} \pmod p$
Vậy lúc này họ đã nhận được 2 giá trị bằng nhau, vì $g^{ab} \pmod p = g^{ba} \pmod p$

# Discrete Logarithm Problem
Về cơ bản, độ bảo mật của Diffie-Hellman là dựa trên bài toán DLP (logarithm rời rạc)
Sự an toàn dựa trên sự bất đối xứng về mức độ khó dễ giữa hai phép toán nghịch đảo.
Tức là theo chiều thuận vì việc tính $g^a \pmod p$ là rất dễ, kể cả khi $a$ rất lớn.
Nhưng để tìm chính xác giá trị $a$ là bao nhiêu khi biết $g^a \pmod p$ là rất khó, nếu $p$ được chọn cẩn thận thì về cơ bản là tốn hàng triệu năm để giải được bài toán này.
Nhưng ta có những cách sau để giải bài toán này khi có những lổ hỏng trong việc chọn cái số $p, g$
## Pohlig-Hellman
Thuật toán hoạt động dựa trên lổ hỏng $p - 1$ có các thừa số nguyên tố đủ nhỏ, lúc này ta sẽ có thể DLP trên các nhóm con tìm các giá trị $x_i$ rồi từ đó CRT để tìm được $x$.
Mục tiêu của chúng ta là tìm $g^x \pmod p$
Ta gọi bậc của nhóm là n, vì $p$ là số nguyên tố nên $n = p -1$
Phân tích thừa số $n$:
$$n = q_1^{e_1} q_2^{e_2} \dots q_k^{e_k}$$
Với mỗi hệ số $q_i^{e_i}$, ta sẽ tìm $x \pmod{ q_i^{e_i}}$ ta khai triển $x$ theo hệ số $q$:
$$x = a_0 + a_1.q + a_2.q^2 + ... + a_{e-1}.q^{e-1} \pmod {q^e}$$


chó duyyyyyyy

