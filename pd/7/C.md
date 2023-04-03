# [C. Pola III](https://tlx.toki.id/courses/basic/chapters/07/problems/C)

Author: Muhammad Kamal Shafi

<!-- Masukkan penjelasan disini -->
Pada soal ini Anda diminta untuk membuat pola dari masukkan sebuah bilangan bulat $N$ sesuai dengan contoh masukkan dan keluaran.

Langkah pertama yang harus dilakukan dalam menyelesaikan ini adalah untuk mencari tau pola yang diminta melalui contoh yang diberikan.

1. $N = 5$ menghasilkan pola:

    ```
    0
    12
    345
    6789
    01234
    ```
2. $N = 7$ menghasilkan pola:

    ```
    0
    12
    345
    6789
    01234
    567890
    1234567
    ```

Dari contoh tersebut, perhatikan bahwa pada setiap pola terdapat karakteristik berikut:
1. Memiliki jumlah baris sebanyak $N$.
2. Baris ke-$i$ pada pola, memiliki panjang $i$ digit/karakter.
3. Digit-digit pada pola berurutan dari $0$ hingga $9$ lalu kembali lagi ke $0$.

---
Sehingga dalam mengimplementasi, manfaatkanlah karakteristik yang sudah diperoleh.

1. Buat perulangan untuk $N$ baris.

    ```c++
    for (int i = 1; i <= n; i++) {
    }
    ``` 

2. Buat perulangan sebanyak $i$ kali untuk setiap baris ke $i$.

    ```c++
    for (int i = 1; i <= n; i++) {
      for (int j = 1; j <= i; j++) {
      }
    }
    ```

2. Keluarkan digit berurutan dari $0$ hingga $9$.

    ```c++
    int digit = 0;
    for (int i = 1; i <= n; i++) {
      for (int j = 1; j <= i; j++) {
        cout << digit;
        digit = (digit + 1) % 10;
      }
      cout << '\n';
    }
    ```

---
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
  int digit = 0;
  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) {
      cout << digit;
      digit = (digit + 1) % 10;
    }
    cout << '\n';
  }
  return 0;
}
```
</details>

<!-- Tambahkan komentar apabila perlu

## Komentar
    
- Komentar I
- Komentar II

-->

<!-- Tambahkan referensi link materi yang berhubungan apabila perlu

## Materi Yang Berhubungan
    
- [Materi I](link-materi)
- [Materi II](link-materi)

-->

<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal I](link-soal)
- [Nama Soal II](link-soal)

-->
