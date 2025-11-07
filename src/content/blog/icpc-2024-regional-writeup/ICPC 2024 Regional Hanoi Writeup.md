---
title: ICPC 2024 Regional Hanoi Writeup
description: Lời giải các bài trong đề Regional ICPC 2024
tags:
  - competitive-programming
date: 2025-07-11
modified: 2025-11-07
author: dnx04
share: "true"
icon: fontawesome-solid:code
color: "#22c55e"
image: "[[Pasted image 20251106234320.png]]"
slug: icpc-2024-regional-writeup
---
Đây là một trong những kì thi để đời của mình và anh em trong đội, khi đã vượt mọi kì vọng và được đến quốc đảo Singapore đánh APAC Championship tại NUS. Sau khi quá lâu vẫn không thấy BTC công khai lời giải tất cả các bài ở nguồn nào, mình quyết định viết 1 cái writeup, cũng là để tưởng nhớ và kỉ niệm chiến thắng hào hùng sau bao cố gắng. 

# [A: Approaching Hurricane](https://oj.vnoi.info/problem/icpc24_regional_a)

## Đề bài

Có một hòn đảo có thể biểu diễn thành một đa giác \$n\$ đỉnh bất kì không tự cắt, với toạ độ các điểm nguyên. Có $q$ truy vấn, mỗi truy vấn gồm 6 số $x_s, y_s, r_s, x_t, y_t, r_t$ biểu diễn một cơn bão, là một hình tròn có tâm $(x_s, y_s)$ và tâm này sẽ di chuyển theo đường thẳng đến $(x_t, y_t)$ , và trong quá trình di chuyển đó, bán kính của nó sẽ thay đổi đều liên tục từ $r_s$ đến $r_t$.

Với mỗi truy vấn, tính phần diện tích của đảo bị cơn bão quét qua, với sai số tuyệt đối hoặc tương đối không quá $10^{-6}$.

Giới hạn: $n \le 3 \times 10^5, n \times q \le 10^6, |x_i|, |y_i| \le 5000, 1 \le r_s, r_t \le 100$.

## Lời giải

Một kinh nghiệm thi cử là bài hình sẽ luôn là bài làm sau cùng, hoặc bỏ luôn không nghĩ đến. Hay nói cách khác, cách tốt nhất để làm bài hình là bỏ. Không có đội nào làm được bài này trong kì thi. Tuy nhiên thì khi mình rảnh về thời gian thì có thể làm được hết. Làm xong rồi thì khẳng định được rằng bỏ là đúng, và trong ICPC chẳng có giới hạn kiến thức nên là chuẩn bị hình bao nhiêu cũng là không đủ. Hình là dạng bài khiến ta ảo tưởng nhiều nhất về những gì có thể làm được.

Một thuật toán hình quan trọng sử dụng trong bài toán này là thuật toán cắt đa giác bằng đa giác lồi của Sutherland-Hodgman. Nôm na thì đây là thuật toán cho phép tính phần giao của một đa giác bất kì không tự cắt (chính là đa giác của đề bài cho, sau đây sẽ gọi là `poly`) với một đa giác lồi nào đó (sau đây sẽ gọi là `clipper`).

[Sutherland–Hodgman algorithm](https://en.wikipedia.org/wiki/Sutherland%E2%80%93Hodgman_algorithm)

Chúng ta chia bài toán thành 2 trường hợp lớn, tuỳ vào số tiếp tuyến chung ngoài của 2 hình tròn được cho trong đề bài.

## Trường hợp 1: 0 hoặc 1 tiếp tuyến

Trường hợp này xảy ra khi và chỉ khi một hình tròn hoàn toàn nằm trong hình tròn còn lại. Khi này đáp án là diện tích phần giao của đa giác với hình tròn lớn nhất trong hai hình tròn của đề bài. Bài toán này có template hình để giải nên chỉ cần chép lại.

[kactl/content/geometry/CirclePolygonIntersection.h at main · kth-competitive-programming/kactl](https://github.com/kth-competitive-programming/kactl/blob/main/content/geometry/CirclePolygonIntersection.h)

## Trường hợp 2: 2 tiếp tuyến

Ta tách phần diện tích được bao phủ bởi cơn bão thành các hình sau:



Trong hình trên, ta đã kẻ 2 tiếp tuyến của hai đường tròn tâm A và B. Đáp án sẽ là tổng diện tích phần giao của hòn đảo với hình thang CDEF và hai hình viên phân còn lại được tạo bởi CF và cung lớn CF, DE và cung nhỏ DE.
### Bài toán 1: Tính diện tích giao của hình thang với đa giác

Với bài toán này ta có thể sử dụng thuật toán Sutherland-Hodgman, sử dụng hình thang CDEF để cắt đa giác ban đầu. Các bạn có thể hỏi ChatGPT để sinh cài đặt cho thuật toán này.
### Bài toán 2: Tính diện tích giao của hình thang với hai hình viên phân

(WIP)

# [B: Bullet Train](https://oj.vnoi.info/problem/icpc24_regional_b)

## Đề bài

Cho một đồ thị vô hướng $n$ đỉnh, khoảng cách giữa 2 đỉnh $i, j$ bất kì là $d(i, j)$. Chi phí của một đường đi nào đó (không nhất thiết là đường đi đơn) giữa 2 đầu mút $u, v$ là tổng $d$ của các cạnh liên tiếp đi qua.

Có $m$ cặp đỉnh quan trọng. Mục tiêu là dựng ra một tập các đường đi **độc lập nhau**, mỗi đường không có quá $k$ đỉnh, sao cho với mỗi cặp đỉnh quan trọng đều có ít nhất một đường trong tập đi qua nó. In cách dựng có tổng chi phí bé nhất, cùng thứ tự các đỉnh của mỗi đường đi.

Giới hạn: $k \le n \le 19, m \le 15$.

## Lời giải

Bài toán này là ghép cơ học của 3 bài toán DP bitmask, và cả 3 bài đều phải lưu truy vết. Truy vết đơn giản là xác định những thứ cần phải lưu để bạn biết là phương án tối ưu đã được dựng như thế nào khi tính DP, và code thì cũng na ná nhau.

1. Tính chi phí nhỏ nhất `TSP[S][v]` để đi qua toàn bộ các đỉnh biểu diễn bởi bitmask `S` và kết thúc tại đỉnh `v` thuộc `S`. Đây là bài toán TSP truyền thống với độ phức tạp $O(n^2 \times 2^n)$.
2. DP SOS các cặp đỉnh quan trọng. Với mỗi mask cặp `pm` thoả điều kiện không có quá $k$ đỉnh, ta cần tính **một** đường đi có chi phí ít nhất mà phủ hết được các cặp trong `pm`. Gọi giá trị này là `min_cost[pm]`. Phần này tối ưu nhất là cài được trong $O(n \times 2^n)$.
3. Sau khi tính được hết `min_cost`, ta sẽ tính được `dp_cover[pm]` là chi phí ít nhất để xây một số tuyến đường phủ qua tất cá các cặp trong `pm`. Độ phức tạp có thể là $O(m \times 2^m)$ sử dụng SOS hoặc $O(3^m)$ bằng duyệt submask cũng chấp nhận được.

Lưu ý rằng, một đường đi không nhất thiết chỉ đi qua **chính xác** các đỉnh quan trọng, mà có thể thêm các đỉnh khác làm trung chuyển để giảm tổng chi phí. Nên ở bài toán 2, với mỗi `pm`, ta có tập đỉnh bắt buộc `base` là hợp các đỉnh quan trọng `u[i], v[i]`. Sau đó, với những đỉnh phụ trợ còn lại, ta phải xét tiếp mọi tập con `extra` có thể thêm vào `base` sao cho cuối cùng `|base| + |extra| <= k`. Khi đó ta có `min_cost[pm] = min TSP[S][v]` với `S = base ∪ extra, |S| <= k` và `v` thuộc `S`. Sau đó tính `dp_cover` bằng kĩ thuật DP SOS: `dp_cover[pm] = min(dp_cover[pm \ sub] + min_cost[sub]`. Cuối cùng là truy vết từng đường đi một bằng thông tin truy vết của cả 3 bài toán ở trên.

Trong kì thi, anh Thuận team mình đã xử đẹp bài này với 1 đấm. 

# [C: Classroom Carnival Chaos](https://oj.vnoi.info/problem/icpc24_regional_c)

## Đề bài

Có $n$ lớp, mỗi lớp có $m$ học sinh phân biệt xếp thành đội hình $n \times m$. Đếm số cấu hình mà không có 2 học sinh cùng lớp đứng cùng cột. Giải $T$ test.

Giới hạn: $T \le 10^5, 1 \le n, m \le 10^7$.

## Lời giải

Nếu chỉ xét lớp, thì số cách xếp thoả mãn không có 2 lớp chung cột là $(n!)^m$. Với mỗi cách xếp trong đó, từng mỗi lớp trong $n$ lớp ta có $m!$ cách điền thứ tự học sinh nên sẽ sinh ra $(m!)^n$ cấu hình thoả mãn đề bài. Do đó đáp số của bài toán cho mỗi test là $(n!) ^ m \times (m!)^n$. 

Ta tính trước giai thừa đến giới hạn của đề và mỗi test ta có thể tính kết quả trong $O(\log n + \log m)$, nên độ phức tạp cuối cùng là $O(\max n + T (\log n + \log m))$.

# [D: Distinguished Permutation](https://oj.vnoi.info/problem/icpc24_regional_d)

## Đề bài

Một hoán vị đúng là một dãy chứa đủ $k$ số từ $1$ đến $k$ theo thứ tự bất kì. Với một hoán vị $P$ từ $1$ đến $N$, gọi $F(P)$ là số đoạn con của $P$ mà cũng là hoán vị đúng. $P$ là hoán vị đặc biệt nếu nó có $F(P)$ lớn nhất và có thể có nhiều hoán vị như vậy.

Cho $T$ test, mỗi test gồm 2 số $N, K$. Dựng hoán vị đặc biệt có $N$ phần tử và có thứ tự từ điển thứ $K$ trong tập các hoán vị đặc biệt.

Giới hạn: $T \le 10^5, 1 \le \sum N \le 10^5, 1 \le K \le 10^{18}$.

## Lời giải

Để đơn giản tính toán ta coi thứ tự từ điển được đánh số từ $0$.

Hiển nhiên ta có $\max F(P) = N$. Ta có thể dựng hoán vị thoả mãn bằng quy nạp. 

Giả sử ta đã dựng được hoán vị $P$ đặc biệt có $k$ phần tử, thì bằng việc đặt số $k + 1$ nằm đầu hoặc đuôi của $P$ thì ta sẽ có hoán vị đặc biệt $k + 1$ phần tử. Theo đó ta cũng chứng minh được số hoán vị đặc biệt có $N$ phần tử là $2^{N - 1}$, vì với việc cố định số $1$ trước, $N - 1$ phần tử còn lại có $2$ cách điền, hoặc đầu hoặc đuôi.

Khi đã dựng được $k$ phần tử, có thể thấy nếu ta đặt tiếp $k + 1$ lên đầu thì sẽ làm tăng thứ tự từ điển của hoán vị thêm $2^{k - 1}$, còn nếu đặt tiếp $k + 1$ ở đuôi thì thứ tự từ điển không tăng. Từ đó ta có phương pháp giải sử dụng hàng đợi 2 đầu (deque):

```cpp
auto get_bit = [&](ll x, int pos) { return (x >> pos) & 1; };
int pivot = min(n, 61);
for (int i = 2; i <= pivot; ++i) {
	if (get_bit(k, i - 2) == 1) p.push_front(i);
	else p.push_back(i);
}
for (int i = pivot + 1; i <= n; ++i) {
	p.push_back(i);
}
for (auto i : p) cout << i << ' ';
```

Độ phức tạp toàn bài là $O(\sum N + T \log K)$.

# [E: Easy Game](https://oj.vnoi.info/problem/icpc24_regional_e)

Đây là một bài game rất khó và không có ai giải được trọn vẹn trong kì thi. Page Code cùng RR đã đăng lời giải của bài này khá chi tiết rồi nên mình sẽ không viết lại nữa.

https://www.facebook.com/share/p/155pjgMFUTd/

# [F: FizzBuzz](https://oj.vnoi.info/problem/icpc24_regional_f)

## Đề bài

Cho $N$ và một xâu $S$ có thể nhận một trong các giá trị: $N$, `fizz`, `buzz` hoặc `fizzbuzz`. Tìm 2 số $a, b$ thoả mãn $1 \le a < b \le 10^9$ sao cho bài toán dãy FizzBuzz với đầu vào là $a, b$ có phần tử thứ $N$ là đúng giá trị của xâu $S$. Nếu không có thì in ra `-1 -1`.

## Lời giải

Giới hạn: $T \le 10^5, N \le 10^9$.

Bài rất đơn giản, thuần xét trường hợp và cũng dễ câu penalty của các đội. Sau đây mình xin trình bày cách xét trường hợp đơn giản nhất:

```cpp
if (s[0] != 'f' && s[0] != 'b') {  // s is number
	if (n == 1)
	  cout << 2 << ' ' << 3 << '\n';
	else if (n == int(1e9))
	  cout << int(1e9) - 2 << ' ' << int(1e9) - 1 << '\n';
	else if (n == int(1e9 - 1)) {
	  cout << int(1e9) - 2 << ' ' << int(1e9) << '\n';
	} else {
	  cout << n + 1 << ' ' << n + 2 << '\n';
	}
} else {
	if (s == "fizz") {
		if (n == (int)1e9) cout << 2 << ' ' << 3 << '\n';
		else cout << n << ' ' << n + 1 << '\n';
	} else if (s == "buzz") {
		if (n <= 2) cout << -1 << ' ' << -1 << '\n';
		else cout << n - 1 << ' ' << n << '\n';
	} else {
		if (n == 1) cout << -1 << ' ' << -1 << '\n';
		else cout << 1 << ' ' << n << '\n';
	}
}
```

# [G: Gid-osh](https://oj.vnoi.info/problem/icpc24_regional_g)

## Đề bài

Cho một mảng $a$ gồm $N$ số. Bỏ đi một số trong dãy sao cho $\max - \min$ của dãy là nhỏ nhất.
## Lời giải

Với $N = 2$ thì đáp án là $0$. Còn lại, sắp xếp dãy rồi in ra $\min(a_N - a_2, a_{N - 1} - a_1)$.

# [H: Hash-shashin](https://oj.vnoi.info/problem/icpc24_regional_h)

## Đề bài

A muốn gửi B một thông điệp bí mật, là một xâu nhị phân $s$ độ dài $n$ bằng cách sau:

1. A chọn trước modulo $m \ge 3$ (không nhất thiết là số nguyên tố).
2. A tính mảng hash của xâu $s$: `hash[0] = 0, hash[i] = (2 * hash[i - 1] + s[i]) % m`
3. Từ mảng `hash` ở trên, A dựng xâu `key` có các kí tự `<`, `=`, `>` với ý nghĩa: `key[i] = "<"` nếu tương ứng `hash[i - 1] < hash[i]` và tương tự. Xâu `key` này tính chỉ số từ 1.

B chỉ nhận được $n, m$, xâu `key` và không biết gì về `s`. Mục tiêu là dựng lại những kí tự chắc chắn của `s` thành xâu `ans`. Hay nói cách khác, với tập $S$ gồm tất cả $s$ thoả mãn `key`, nếu `s[i] = "0"` với mọi `i` thì  `ans[i] = "0"`, tương tự với `s[i] = "1"`. Nếu không như vậy thì `ans[i] = "?"`. Nếu xâu `ans` toàn là `"?"` thì in ra `impossible`.

Giới hạn: $T \le 10^4, n \le 2 \times 10^5, 3 \le m \le 10^9$.

## Lời giải

WIP

# [I: Inversland](https://oj.vnoi.info/problem/icpc24_regional_i)

## Đề bài

Bạn có $N$ đồng xu, đồng xu thứ $i$ có mệnh giá là $1 / p_i$. Các mẫu số ở đây đều là các số nguyên tố phân biệt: $p_1, \dots, p_n$.

Đếm số giá trị có thể giao dịch bởi các đồng xu ở trên mà người bán **bắt buộc phải trả lại tiền thừa** theo modulo $998244353$. Nếu có vô số giá trị như vậy thì in ra Infinity.

Giới hạn: $N \le 2 \times 10^5, p_i \le 998244353$.

## Lời giải

Bài toán này có thể giải bằng 2 cách, một cách sử dụng toán học thuần tuý và thường chỉ có ai học nhiều toán (IMO chẳng hạn, hoặc ChatGPT) mới biết, và một cách dùng FFT mà mình không biết nhưng bạn mình mò ra được. Mình sẽ trình bày cách toán.

Đặt $P = \prod p_i$. Ta sẽ giải bài toán ngược: tính số giá trị $\frac{x}{P}$ có thể trả bằng các mệnh giá ở trên mà không phải trả lại tiền thừa.

Điều này tương đương với tìm số lượng $x$ sao cho tồn tại tổ hợp tuyến tính $x = \sum_{i = 1}^n c_i \frac{P}{p_i}$ mà các hệ số $c_1, \dots, c_n \ge 0$. Tập các số như vậy tạo thành một [semigroup số học](https://en.wikipedia.org/wiki/Numerical_semigroup) sinh bởi các $A_i = \frac{P}{p_i}$.

Trong lý thuyết **semigroup số học**, nếu $\gcd(A_1, A_2, ..., A_n) = 1$ (đúng với mọi test vì các $p_i$ nguyên tố khác nhau), thì:

1. Tập hợp này có hữu hạn số lượng **giá trị không biểu diễn được** (gọi là **gaps**).
2. Số lượng gaps được gọi là **genus** $g$ và có công thức như sau: 
$$
g = \dfrac{F + 1}{2}, \quad F = (n - 1)P - \sum_{i=1}^n \frac{P}{p_i}
$$

$F$ ở đây còn gọi là **số Frobenius** của semigroup.

Độ phức tạp cuối cùng là $O(N \log \max p_i)$.

# [J: Jumbled Journey](https://oj.vnoi.info/problem/icpc24_regional_J)

## Đề bài

Cho một đồ thị vô hướng $n$ đỉnh $m$ cạnh, mỗi cạnh có trọng số $w_i$. Ta cần giao hàng theo lịch trình là một hoán vị $p$ từ $1$ đến $n$. Do đó có $n - 1$ chặng giao hàng, chặng thứ $i$ là một đường đi đơn từ $p_i$ đến $p_{i + 1}$.

Chi phí của một chặng là trọng số cạnh lớn nhất xuất hiện trên chặng đó, và chi phí của lịch trình là tổng chi phí của $n - 1$ chặng. Chi phí của lịch trình *càng nhỏ thì càng tối ưu.*

Tìm ra một lịch trình, sao cho *chi phí tối ưu* của lịch trình là **lớn nhất có thể.**
## Lời giải

Đây là bài mà mình đã đọc sai đề (do nhầm lẫn về minimax) trong kì thi và dẫn đến mất thời gian của cả đội, may mắn là sai lầm này đã không tước đi tấm vé dự APAC Championship của đội mình, khi mà kết quả cuối cùng, mình với đội đứng sau cùng trường kém nhau khoảng 200 penalty. 

Anh Hạnh đã chữa bài này rất cụ thể trên kênh YouTube của anh, và có lẽ điều duy nhất mình nên làm lúc này là phát biểu lại đề bài cho chuẩn.

[Lời giải: ICPC Asia Hanoi 2024 - bài J](https://www.youtube.com/watch?v=-sZk-RzIRdE&t=3466s)

## **Đề bài**

Cho một mê cung gồm $n$ hành lang vuông góc liên tiếp nhau, mỗi hành lang có độ dài $l_i$. Trước khi bắt đầu bạn có thể chọn trước độ dài tốc biến $m$ nguyên để di chuyển từ điểm bắt đầu của hành lang $1$ đến điểm kết thúc của hành lang $n$.

Ở mỗi thời điểm nguyên bạn sẽ tốc biến đúng $m$ đơn vị độ dài về phía trước trong đúng $1$ giây, nếu cú tốc biến này không chuẩn (khoảng cách từ điểm bạn tốc biến đến điểm cuối của hành lang hiện tại không đủ $m$ đơn vị) thì bạn sẽ tốc biến đến điểm cuối của hành lang và bị choáng $1$ giây, điều này áp dụng cả với hành lang cuối. Nếu không thì bạn có thể tốc biến tiếp ngay lập tức.

Tính thời gian ngắn nhất có thể để ra khỏi mê cung khi chọn $m$ tối ưu.

Giới hạn: $n \le 10^6, l_i \le 10^9$.

## **Lời giải**

Chúng ta bắt đầu với một số nhận xét như sau về đáp án tối ưu:

1. Với $m$ cho trước thì ta có công thức tổng thời gian hoàn thành: $$f(m) = \sum_{i = 1}^{n} \left \lceil \frac{l_i}{m} \right \rceil + [l_i \bmod m \ne 0] $$
2. Với mọi $m$ ta có $n \le f(m) \le 2n$. Dấu bằng thứ nhất xảy ra khi toàn bộ $l_i$ bằng nhau, còn dấu bằng thứ hai xảy ra khi ta cho $m > \max l_i$.
3. $f(m)$ tối ưu khi $m$ là một trong các $l_i$.

Nhận xét thứ 3 gợi ý rằng chúng ta cần duyệt qua tất cả các $l_i$ và tính nhanh được $f(l_i)$. Chúng ta chia mảng thành 3 phần:

1. Phần mà $l_j < l_i$, khi này với mỗi $j$ chúng ta mất $2$ giây.
2. Phần $l_j = l_i$, mỗi $j$ mất $1$ giây.
3. Phần còn lại thì với mỗi $j$ tốn $\left \lceil \frac{l_j}{l_i} \right \rceil + [l_j \bmod l_i \ne 0]$ giây.

Mấu chốt của bài toán là tính phần 3 đủ nhanh. Và thật ra, cách đủ nhanh lại rất đơn giản:

```cpp
int calc(int x,int m){
    return (((x + m - 1) / m) + (x % m != 0));
}

for (int i = 0; i < n; ++i) {
  int j = i;
  for (j = i; j < n; ++j) {
    if (a[j] > a[i]) {
      break;
    }
  }
  j--;
  int curr = 2 * n - (j - i + 1);
  for (int r = n - 1; r > j; r--) {
    curr += (calc(a[r], a[i]) - 2);
    if (curr >= ans) {
      break;
    }
  }
  ans = min(ans, curr);
  i = j;
}

cout << ans;
```

Ý tưởng của thuật toán trên là đặt cận và tham lam. Ở một thời điểm bất kì, giá trị của `ans - curr` là ngưỡng quyết định xem `l[i]` hiện tại có tối ưu hơn không. Để có thể quyết định nhanh, ta tham lam lấy các giá trị lớn trước rồi cộng phần dư vào. Ta thấy là với $l_j$ rất lớn so với $l_i$ thì `curr` sẽ tăng nhanh làm vòng lặp kết thúc sớm, còn lại thì không có quá nhiều giá trị để duyệt.

Độ phức tạp khi này là $O(nE)$ với $E$ là số bước duyệt trung bình với mỗi giá trị $i$. Trong khuôn khổ bài viết này ta thừa nhận $E = O(\log n)$, chứng minh xin dành cho độc giả như một bài tập.

Độ phức tạp cuối cùng là $O(n \log n)$.

> Trong kì thi, đội mình là một trong những đội hiếm hoi 1 đấm AC bài này, trong khi các đội mạnh khác như IBM Cloud, Azure của UET, hay đến cả gugugaga của NEU, AtCoder của HCMUS, đều phải mất nhiều sub. Đây là lợi thế cực lớn khi đội mình so penalty để kiếm suất dự APAC Championship, và đã cứu được sai lầm sảy chân ở bài J.

# [L: Locomotive Lane Logistics](https://oj.vnoi.info/problem/icpc24_regional_l)

## Đề bài

Cho một đường ray có độ dài $s$ và $q$ truy vấn. Mỗi truy vấn có 1 trong 2 dạng:

1. `+ l v`: thêm một tàu có độ dài `l` và vận tốc `v` vào lịch trình.
2. `- l v`: xoá một tàu có độ dài `l` và vận tốc `v` khỏi lịch trình.

Mỗi con tàu có phần mui và phần đuôi. Con tàu sẽ xuất phát với mui chạm vạch xuất phát và chỉ ra khỏi đường ray khi đuôi rời khỏi vạch kết thúc. Mỗi con tàu ta có thể chọn cho nó thời điểm xuất phát bất kì. 

Tính tổng thời gian ít nhất để đưa toàn bộ tàu ra khỏi đường ray mà không xảy ra tai nạn. Tai nạn xảy ra khi mui của tàu đi sau đâm vào đuôi của tàu đi trước và tàu đi trước chưa ra khỏi đường ray.

Giới hạn: $s \le 10^9, q \le 2 \times 10^5$.

## Lời giải

Qua cảm nhận, ta có thể rút ra 2 nhận xét đầu tiên về đáp án tối ưu:

1. Nếu 2 tàu có cùng vận tốc, thì chúng có thể đi nối đuôi nhau như là 1 tàu, nên ta có thể giả sử tất cả `v` đều khác nhau.
2. Thứ tự xuất phát của các con tàu sẽ phụ thuộc vào vận tốc, tàu chậm sẽ đi trước, rồi sau một khoảng thời gian tối ưu ta sẽ cho tàu nhanh hơn đuổi theo sau sao cho không xảy ra tai nạn. Dễ thấy là xếp như vậy tối ưu hơn vì ta lợi thêm về thời gian từ hiệu vận tốc của hai tàu đuổi nhau.

Từ 2 nhận xét trên, bằng việc ngồi nháp toán và chứng minh công thức ta rút ra nhận xét quan trọng nhất của bài toán:

3. Giả sử có 2 tàu `(l1, v1)` và `(l2, v2)` với `v1 < v2`. Để tối ưu nhất thì thời điểm đuôi tàu thứ nhất ra khỏi đường ray cũng chính là lúc mui của tàu thứ hai chạm vạch kết thúc. Nhận xét trên cho ta công thức tính giãn cách thời gian xuất phát tối ưu nhất của hai tàu:   
$$
\dfrac{s + l_1}{v_1} - \dfrac{s}{v_2} = \dfrac{s}{v_1} - \dfrac{s}{v_2} + \dfrac{l_1}{v_1}
$$

4. Áp dụng nhận xét trên cho $n$ tàu, thì tổng thời gian tối ưu là: 
$$
\dfrac{s}{v_1} - \dfrac{s}{v_n} + \sum_{i = 1}^{n - 1} \dfrac{l_i}{v_i} + \dfrac{s + l_n}{v_n} = \dfrac{s}{v_1} + \sum_{i = 1}^{n} \dfrac{l_i}{v_i}
$$

Do đó ta chỉ cần duy trì 2 giá trị sau qua các thao tác thêm và xoá tàu khỏi danh sách:
1. Vận tốc $v_1$ của tàu chậm nhất, có thể dùng multiset, map hoặc priority queue.
2. Tổng tỉ lệ chiều dài - vận tốc của các tàu.

Độ phức tạp cho mỗi truy vấn là $O(\log q)$.

# [M: Minotaur's Mysterious Maze](https://oj.vnoi.info/problem/icpc24_regional_m)

## Đề bài

Cho một mê cung gồm $n$ phòng giống hệt nhau, không sắp thứ tự, nối tiếp thành một vòng tròn, mỗi phòng đều có phòng liền trước và liền sau (có thể là cùng 1 phòng). Mỗi phòng có một cái đuốc ở trạng thái `0` (tắt) hoặc `1` (bật). Bạn không biết $n$ mà phải đoán nó.

Đầu tiên, và mỗi khi bạn đến một phòng nào đó, máy chấm sẽ trả về trạng thái `0` hoặc `1` của đuốc trong phòng đó và sau đó bạn có thể chọn thực hiện 1 trong 3 loại truy vấn:

1. `> v`: Đặt đuốc thành trạng thái `v` rồi đi tiếp sang phòng liền sau.
2. `< v`: Đặt đuốc thành trạng thái `v` rồi đi tiếp sang phòng liền trước.
3. `! n`: Trả lời số phòng là `n` và kết thúc. Truy vấn này không tính vào tổng số truy vấn.

Số $n$ và trạng thái ban đầu của đuốc trong phòng là cố định, và chỉ có bạn mới thay đổi được trạng thái đuốc. Mục tiêu là đoán được $n$ trong tối đa $n + 55$ truy vấn.

## Lời giải

Kì Regional này thực sự là để đời với rất nhiều sự magic, khi mà bài này teammate của mình đã code không cần test tay và AC ngay sau đó trong sự bất ngờ của tất cả mọi người.

Dễ thấy ta sẽ chỉ đi theo một chiều chứ không quay đầu, và phải tìm cách đánh dấu các phòng đã đi qua sao cho có cách để nhận diện lại nó khi ta quay trở lại. 55 truy vấn được thêm vào chính là để làm điều đó. Đơn giản thôi:

1. Sinh ngẫu nhiên một số có 55 bit. Ta sẽ chỉnh trạng thái đuốc của 55 phòng đầu tiên đi qua bằng các bit của số này. Các phòng còn lại giữ nguyên.
2. Ta lưu lại trạng thái của tất cả các phòng đã đến bằng một xâu nhị phân $n + 55$ bit. Khi ta thấy trạng thái của 55 bit đầu tiên lặp lại ở vị trí gần nhất nào đó, thì chúng ta đã xác định được $n$ với xác suất đúng $1 - 0.5^{55}$.

# Kết thúc

