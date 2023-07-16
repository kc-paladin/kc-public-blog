# [B. Pangkat Besar](https://tlx.toki.id/courses/competitive/chapters/05/problems/B)

Author: Andreas Timothy

Perhatikan sifat berikut:

- Apabila $B$ bernilai genap, $A^B = A^{\lfloor \frac{B}{2} \rfloor} \times A^{\lfloor \frac{B}{2} \rfloor}$

- Apabila $B$ bernilai ganjil, $A^B = A^{\lfloor \frac{B}{2} \rfloor} \times A^{\lfloor \frac{B}{2} \rfloor} \times A$

Disini dapat dilihat bahwa kita cukup melakukan perpangkatan sebanyak $log B$ kali karena nilai $B$ dibagi $2$ terus-menerus. Untuk mendapatkan 6 digit terakhir kita tinggal melakukan modulo $1000000$.

Namun permasalahan selanjutnya adalah apabila nilai akhir (tanpa di modulo) melebihi $999999$ maka kita perlu menambahkan angka $0$ di depan bilangan hingga $6$ digit, tetapi jika tidak melebihi $999999$ kita tidak diminta untuk menambahkan angka $0$. Untuk mengatasi permasalahan ini kita dapat mengecek apabila sewaktu-waktu hasil pemangkatan kita melebihi $999999$, alias operasi modulonya "berfungsi".

Kompleksitas Waktu: $O(\log B)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
#define ll long long

ll a, b, res;
bool melebihi = false;
int panjang;

ll mod(ll x) {
  if (x > 999999) melebihi = true;
  return x % 1000000;
}

ll p(ll a, ll b) {
  if (b == 0) return 1;
  ll res = p(a, b / 2);
  if (b % 2)
    return mod(mod(res * res) * a);
  else
    return mod(res * res);
}

int digit(ll x) {
  if (x == 0) return 1;  // kasus khusus
  int len = 0;
  while (x > 0) {
    len++;
    x /= 10;
  }
  return len;
}

int main() {
  cin >> a >> b;
  res = p(a, b);
  if (melebihi) {
    panjang = digit(res);
    // output 0 di depan bilangan
    for (int i = 1; i <= 6 - panjang; i++) cout << 0;
  }
  cout << res << '\n';
}
```

</details>

## Komentar

- Selain metode di atas, terdapat juga satu teknik lain yang umum digunakan untuk melakukan pemangkatan bilangan besar dengan memanfaatkan basis biner. Silahkan kunjungi referensi di bawah jika ingin mempelajari lebih lanjut.

## Materi Yang Berhubungan

- [Binary Exponentiation](https://cp-algorithms.com/algebra/binary-exp.html)

## Soal Yang Berhubungan

- [Hadiah](https://tlx.toki.id/courses/competitive/chapters/05/problems/C)
