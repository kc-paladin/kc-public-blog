# [C. Komposisi Fungsi II](https://tlx.toki.id/courses/basic/chapters/12/problems/C)

Author: Muhammad Hasan

Kita dapat definisikan fungsi $F(x, k)$ sebagai berikut:

- Apabila $k=1$ maka $F(x, k) = |Ax + B|$
- Apabila $k>1$ maka $F(x, k) = |A \times F(x, k - 1) + B|$

Sehingga kita cukup implementasi fungsi $F(x, k)$ tersebut.


Kompleksitas Waktu: $O(K)$

Kompleksitas Memori: $O(K)$ dikarenakan pemanggilan *stack* pada fungsi rekursif.

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int A, B, K, X;

int F(int k) {
  if (k == 1) {
    return abs(A * X + B);
  }
  return abs(A * F(k - 1) + B);
}

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  cin >> A >> B >> K >> X;
  cout << F(K) << '\n';

  return 0;
}
```
</details>