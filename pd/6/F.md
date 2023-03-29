# [F. Faktor Bilangan](https://tlx.toki.id/courses/basic/chapters/06/problems/F)

Author: Muhammad Hasan

Pada soal ini kita perlu mencari faktor bilangan / pembagi dari $N$.

Untuk menyelesaikan soal ini, kita cukup melakukan `for` loop dari $1$ sampai dengan $N$. Pada `for` loop tersebut, ketika kita berada pada angka $i$ kita cukup periksa apakah $i$ habis membagi $N$ dan *output* angka $i$ tersebut. 

Dalam pemrograman kita bisa cek suatu angka habis dibagi dengan angka lain dengan *Modulo* / Sisa Bagi (yakni cek apakah `N mod i == 0`, dengan kata lain cek apakah sisa bagi $N$ sama dengan $0$ ketika dibagi $i$).

Mungkin Anda berpikir, bukankah cara ini lambat? tenang saja, karena kalau kita liat pada batasan soal, kita dapatkan nilai $N$ maksimal terbilang relatif kecil, yakni hanya $10^6$ saja (Sebagai *rule of thumb*, operasi sebanyak $2 \times 10^8$ pada program C++ memakan waktu sekitar $1$ detik lebih). Oleh karena itu, solusi `for` loop tersebut sudah cukup untuk menyelesaikan permasalahan ini.

Kompleksitas Waktu: $O(N)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  int n;
  cin >> n;
  for (int i = n; i >= 1; i--) {
    if (n % i == 0) {
      cout << i << '\n';
    }
  }

  return 0;
}
```
</details>

## Komentar
    
- Tentunya terdapat cara yang lebih efisien dalam menyelesaikan soal ini, yakni dengan for loop hanya sampai $\sqrt{N}$ saja, namun dengan cara ini kita perlu simpan hasil faktor bilangan dan melakukan pengurutan terlebih dahulu.
- Ada cara yang lebih *overkill* dalam menyelesaikan persoalan ini, apabila tertarik bisa baca artikel Integer Factorization yang ada pada materi berhubungan dibawah.

## Materi Yang Berhubungan
    
- [Modulo Operator in C++](https://www.geeksforgeeks.org/modulo-operator-in-c-cpp-with-examples/)
- [Integer Factorization](https://cp-algorithms.com/algebra/factorization.html)
- [Blog: Number of operation in 1 Second? - Codeforces](https://codeforces.com/blog/entry/80680)