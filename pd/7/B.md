# [B. Pola II](https://tlx.toki.id/courses/basic/chapters/07/problems/B)

Author: Eileen Camelia Limneus

Setelah menganalisis contoh dalam persoalan ini, kita dapat mengetahui bahwa:

- Pada baris pertama, terdapat $4$ spasi diikuti oleh $1$ karakter `*`.
- Pada baris kedua, terdapat $3$ spasi diikuti oleh $2$ karakter `*`.
- Pada baris ketiga, terdapat $2$ spasi diikuti oleh $3$ karakter `*`.
- Pada baris keempat, terdapat $1$ spasi diikuti oleh $4$ karakter `*`.
- Pada baris kelima, tidak terdapat spasi dan terdapat $5$ atau $N$ karakter `*`.

Kita dapat menggunakan **perulangan for bersarang** untuk menyelesaikan persoalan ini. Berikut langkah - langkahnya! 👇

1. Gunakan fungsi perulangan `for` untuk menghasilkan setiap baris pada pola.
2. Di dalam perulangan `for` pertama, kita menggunakan fungsi perulangan `for` lain untuk menghasilkan pola spasi dan `*` pada setiap baris.
3. Di dalam perulangan `for` kedua, kita melakukan pengecekan kondisi $j > i$ (lihat solution code). Jika kondisi ini benar, kita menghasilkan spasi. Jika tidak, kita menghasilkan `*`.
4. Setelah selesai menghasilkan pola spasi dan bintang untuk suatu baris, kita pindah ke baris baru menggunakan newline `\n`. 

Kompleksitas Waktu: $O(N^2)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  int n;
  cin >> n;

  for (int i = 1; i <= n; i++) {
    for (int j = n; j >= 1; j--) {
      if (j > i) {
        cout << " ";
      } else {
        cout << "*";
      }
    }
    cout << "\n";
  }
}
```
</details>

## Komentar
    
- Meskipun perulangan bersarang dapat membingungkan pada awalnya, tetapi teknik ini sangat berguna untuk menyelesaikan masalah. Jadi, teman - teman boleh cek materi di bawah ya!

## Materi Yang Berhubungan
    
- [C++ for Loop (With Examples)](https://www.geeksforgeeks.org/cpp-for-loop/)
- [Nested Loops in C++ with Examples](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples-2/)
