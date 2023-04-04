# [A. Penjumlahan Pecahan](https://tlx.toki.id/courses/competitive/chapters/02/problems/A)

Author: Andreas Timothy

Problem ini cukup mudah diselesaikan sebagaimana kita mengerjakannya secara manual. Kita hanya perlu:

- Samakan penyebut
- Jumlahkan pembilang
- Sederhanakan

Untuk melakukan ketiga proses di atas kita hanya memerlukan $\text{FPB}$ dan $\text{KPK}$. Untuk mencari nilai $\text{FPB}$ kita bisa menggunakan fungsi `__gcd` bawaan C++ atau dengan **algoritma euclid**, sedangkan nilai $\text{KPK}$ dapat diperoleh dengan sifat berikut:

$KPK(a, b) = \frac{a \times b}{FPB(a, b)}$

Kompleksitas Waktu: $O(log(N))$

Kompleksitas Memori: $O(1)$

> Catatan: $N$ sebagai variabel-variabel yang dipakai dalam program

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

long long a, b, c, d, e, f, kpk, fpb;

int main() {
  cin >> a >> b >> c >> d;
  // Samakan penyebut, lalu kalikan dengan pembilang
  kpk = b * d / __gcd(b, d);
  a *= kpk / b;
  b = kpk;
  c *= kpk / d;
  d = kpk;

  // Jumlahkan pembilang, lalu sederhanakan
  e = a + c;
  f = kpk;
  fpb = __gcd(e, f);
  e /= fpb;
  f /= fpb;

  cout << e << ' ' << f << '\n';
}
```

</details>

## Komentar

- Gunakan tipe data `long long` untuk setiap variabel agar lebih mudah (_recommended but not required_)

## Materi Yang Berhubungan

- [C++ gcd\_\_](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/)
- [Euclidean Algorithm](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)
