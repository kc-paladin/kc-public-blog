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
- C++ mempunyai dua cara input. Yang pertama adalah `scanf` dan `printf` yang berasal dari C. Lalu, ada `cin` dan `cout` yang ditambahkan oleh C++. Namun, penulis lebih menyukasi `cin` dan `cout` dikarenakan simplisitasnya.

## Materi Yang Berhubungan
- [C++ If ... Else](https://www.w3schools.com/cpp/cpp_conditions.asp)

## Soal Yang Berhubungan
- Mayoritas soal lain dari *course* yang sama di TLX mempunyai materi yang serupa