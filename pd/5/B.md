# [B. If Then](https://tlx.toki.id/courses/basic/chapters/05/problems/B)

Author: Ackhava Adam Malonda

Soal ini adalah demonstrasi cara memasukan sebuah angka, melakukan *if statement* dan mencetak angkanya jika sebuah kondisi dipenuhi. 

Dalam C++, kita menggunakan *keyword* berupa `if`, beserta fitur `cin` dan `cout`.

Kompleksitas Waktu: $O(1)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  int N;
  cin >> N;

  if (N > 0) {
    cout << N;
  }

  return 0;
}
```
</details>

## Komentar
- C++ mempunyai dua cara input. Yang pertama adalah `scanf` dan `printf` yang berasal dari C. Lalu, ada `cin` dan `cout` yang ditambahkan oleh C++. Namun, penulis lebih menyukai `cin` dan `cout` dikarenakan simplisitasnya.
    > _PENTING:_ `cin` dan `cout` lebih lambat dari `printf` dan `scanf` secara *default*. Gunakan perintah berikut jika tidak mencampurkan kedua jenis operator: `cin.tie(0);cout.tie(0);ios_base::sync_with_stdio(false);`.

## Materi Yang Berhubungan
- [C++ If ... Else](https://www.w3schools.com/cpp/cpp_conditions.asp)
- [Cin-Cout vs Scanf-Printf](https://www.geeksforgeeks.org/cincout-vs-scanfprintf/)