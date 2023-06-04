# [C. Hadiah](https://tlx.toki.id/courses/competitive/chapters/05/problems/C)

Author: Andreas Timothy

Perhatikan sifat berikut:

$$
A^{B^C} = A^{B \times B \times ... \times B} = (((A^B)^B)...)^B
$$

dengan $B$-nya sebanyak $C$ kali. Oleh karena itu, kita dapat melakukan iterasi sebanyak $C$ untuk memangkatkan nilai $A$. Pemangkatan dilakukan dengan teknik pemangkatan cepat seperti pada problem [sebelumnya](https://tlx.toki.id/courses/competitive/chapters/05/problems/B).

Kompleksitas Waktu: $O(C \log B)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
#define ll long long

ll a, b, c, n, val;

ll p(ll a, ll b) {
  if (b == 0) return 1;
  ll res = p(a, b / 2);
  if (b % 2)
    return (((res * res) % n) * a) % n;
  else
    return (res * res) % n;
}

int main() {
  cin >> a >> b >> c >> n;
  val = a;
  while (c--) {
    val = p(val, b);
  }
  cout << val + 1 << '\n';
}
```

</details>

## Komentar

- Perhatikan bahwa nilai yang diminta adalah $(A^{B^C} \mod N) + 1$, bukan $A^{B^C} \mod (N + 1)$

## Materi Yang Berhubungan

- [Binary Exponentiation](https://cp-algorithms.com/algebra/binary-exp.html)

## Soal Yang Berhubungan

- [Pangkat Besar](https://tlx.toki.id/courses/competitive/chapters/05/problems/B)
