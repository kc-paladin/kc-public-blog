# [While + Pencacah](https://tlx.toki.id/courses/basic/chapters/06/problems/D)

Author: Hamiz Ghani

<!-- Masukkan penjelasan disini -->
Pada soal ini kita diminta membuat program yang membaca input secara terus menerus hingga `EOF`, kemudian kita mencetak sebuah output yang merupakan penjumlahan bilangan pada input.

Kita dapat menggunakan fungsi perulangan `while`. Selama masih ada input, tambahkan nilai variabel jumlah dengan input tersebut.
```c++
while (cin >> x) {
  sum += x;
}
```

Kompleksitas Waktu: $O(N)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
int main() {
  int x, sum = 0;
  while (cin >> x) {
    sum += x;
  }
  cout << sum;
}
```
</details>




## Komentar
    
- Program akan selalu menunggu input dan tidak akan berhenti berjalan apabila dijalankan pada interactive console



<!-- Tambahkan referensi link materi yang berhubungan apabila perlu
-->

## Materi Yang Berhubungan
    
-  [C++ While loop](https://www.w3schools.com/cpp/cpp_while_loop.asp)
-  [end-of-file (EOF)](https://en.wikipedia.org/wiki/End-of-file#:~:text=In%20computing%2C%20end%2Dof%2D,called%20a%20file%20or%20stream.)


<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal 1](link-soal)
- [Nama Soal II](link-soal)

-->