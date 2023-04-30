# [A. Break Continue Exit](https://tlx.toki.id/courses/basic/chapters/07/problems/A)

Author: Ackhava Adam Malonda

Soal ini mendemonstrasikan cara mengaplikasikan *loop* dengan *break* dan *continue*.

Dalam C++, kita dapat menggunakan *keyword* berupa `for`, `break`, dan `continue`.

Kompleksitas Waktu: $O(N)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <cstdio>

int main() {
  int N;
  scanf("%d", &N);
  for (int i = 1; i <= N; i++) {
    if (i % 10 == 0) {
      continue;
    } else if (i == 42) {
      printf("ERROR");
      break;
    }
    printf("%d", i);
    if (i < N) {
      printf("\n");
    }
  }
}
```
</details>

## Komentar
- Meskipun *loop* berjalan dari $1$ sampai $N$, sebenarnya loop pasti akan berhenti pada angka $42$ jika $N>42$. Hal ini karena penggunaan `break`.
- C++ mempunyai dua cara input. Yang pertama adalah `scanf` dan `printf` yang berasal dari C. Lalu, ada `cin` dan `cout` yang ditambahkan oleh C++. Namun, penulis lebih menyukai `cin` dan `cout` dikarenakan simplisitasnya.
- `cin` dan `cout` lebih lambat dari `printf` dan `scanf` secara *default*. Gunakan perintah berikut jika tidak mencampurkan kedua jenis operator:
  ```c++
  ios_base::sync_with_stdio(false);
  cin.tie(0);
  cout.tie(0);
  ```

## Materi Yang Berhubungan
- [C++ If Else](https://www.w3schools.com/cpp/cpp_conditions.asp)
- [Cin-Cout vs Scanf-Printf](https://www.geeksforgeeks.org/cincout-vs-scanfprintf/)
