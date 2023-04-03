# [E. Luas Segitiga](https://tlx.toki.id/courses/basic/chapters/03/problems/E)

Author: Muhammad Kamal Shafi

<!-- Masukkan penjelasan disini -->
Pada soal ini Anda diminta untuk menghitung **luas segitiga** yang memiliki panjang alas $A$ cm dan tinggi $T$ cm.

Dengan menggunakan formula berikut, luas segitiga bisa diperoleh dengan mudah.

$$Luas = \frac{A \times T}{2}$$

Namun, perhatikan bahwa meskipun masukkan yang diberikan soal merupakan bilangan bulat, hasil perhitungan mungkin berbentuk bilangan desimal. 

Karena soal meminta anda untuk mengeluarkan hasil dengan 2 angka di belakang koma, anda perlu melakukan *formatting* terhadap keluaran.

---
Pada bahasa **_C++_**, setidaknya terdapat dua cara berikut untuk melakukan *formatting* angka dibelakang koma:
1. Menggunakan `printf`, contoh penggunaan:

    ```c++
    float PI = 3.1415;
    float tiga = 3;

    printf("%.2f\n", PI); // menuliskan "3.14"
    printf("%.3f\n", tiga); // menuliskan "3.000"
    ```
2. Menggunakan `setprecision`, contoh penggunaan:

    ```c++
    float PI = 3.1415;
    float tiga = 3;

    cout << fixed << setprecision(2); 
    cout << PI << '\n'; // menuliskan "3.14"
    cout << tiga << '\n'; // menuliskan "3.00"

    cout << fixed << setprecision(3); 
    cout << PI << '\n'; // menuliskan "3.141"
    ```

---
Kompleksitas Waktu: $O(1)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  float a, t;

  cin >> a >> t;
  cout << fixed << setprecision(2) << a * t / 2 << '\n';
  // printf("%.2f\n", a * t / 2); // alternatif

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
    
- Komentar I
- Komentar II

-->

<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal 1](link-soal)
- [Nama Soal II](link-soal)

-->
