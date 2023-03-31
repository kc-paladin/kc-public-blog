# [If Then Else](https://tlx.toki.id/courses/basic/chapters/05/problems/D)

Author: Hamiz Ghani

<!-- Masukkan penjelasan disini -->
Pada soal ini kita diminta untuk membuat program yang menerima suatu bilangan bulat $N$. Apabila $N$ bilangan bulat positif, cetak `positif`. Jika $N$ bilangan bulat negatif, cetak `negatif`. Selain itu apabila $N=0$, cetak `nol`. 

Dalam C++, kita bisa menggunakan _keyword_ `if`, `else` dan `else if`.

Kompleksitas Waktu: $O(1)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
int main() {
  int n;  // deklarasi variabel input
  cin >> n;  // input
  if (n > 0) {  // jika n>0
    cout << "positif" << endl;  // cetak positif
  } else if (n < 0) {  // jika n<0
    cout << "negatif" << endl;  // cetak negatif
  } else {  // selain kasus diatas, maka n==0
    cout << "nol" << endl;  // cetak nol
  }
}
```
</details>


<!-- Tambahkan komentar apabila perlu

## Komentar
    
- Komentar I
- Komentar II

-->

<!-- Tambahkan referensi link materi yang berhubungan apabila perlu
-->
## Materi Yang Berhubungan
    
-  [how to check whether a number is postitve or negative in C++](https://prepinsta.com/cpp-program/cpp-program-to-check-whether-a-number-is-positive-or-negative/)


<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal 1](link-soal)
- [Nama Soal II](link-soal)

-->