# [B. A Tambah B](https://tlx.toki.id/courses/basic/chapters/03/problems/B)

Author: Muhammad Hasan

Soal ini hanya mendemonstrasikan bagaimana kita *input* dua bilangan bulat $A$ dan $B$ dan output hasil perjumlahan $A + B$.

Pada C++ Kita bisa gunakan `cin` dan `cout` untuk hal ini.

Kompleksitas Waktu: $O(1)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  int a, b;
  cin >> a >> b;
  cout << a + b << '\n';

  return 0;
}
```
</details>

## Komentar
    
- Dalam C++ terdapat metode lain dalam melakukan input/output yakni `scanf` atau `printf`, namun *author* lebih memilih menggunakan `cin` dan `cout` karena lebih *simple*.
- Karakter `\n` digunakan untuk membuat *new line*, ada cara lain pada C++, yakni dengan `endl`, namun `endl` membuat hasil eksekusi kode semakin lambat (baca blog pada materi yang berhubungan untuk detailnya)


## Materi Yang Berhubungan
    
- [C++ Input/Output](https://www.w3schools.com/cpp/cpp_user_input.asp)
- [Comparison Between endl and \n in C++](https://codeforces.com/blog/entry/43780)

## Soal Yang Berhubungan
    
- [Adding two numbers](https://www.hackerrank.com/contests/emseupm-sample-1/challenges/adding-two-numbers)
