# [C. If Then Multi](https://tlx.toki.id/courses/basic/chapters/05/problems/C)

Author: Evelyn

Pada soal ini, kita akan diberikan sebuah bilangan bulat $N$. Jika $N$ merupakan bilangan bulat genap positif, maka kita perlu mencetak kembali bilangan tersebut. Jika bukan, maka kita tidak perlu mencetak apa-apa.

Untuk menyelesaikan soal ini, kita bisa menggunakan metode percabangan.

Pada C++, kita bisa menggunakan *keyword* berupa `if`.

Pertama, kita akan mengecek apakah $N$ merupakan bilangan bulat positif (lebih dari nol). Jika $N > 0$, maka kita harus mengecek apakah $N$ merupakan bilangan genap. Jika $N$ tidak lebih dari 0, maka kita tidak perlu melakukan pengecekan lebih lanjut.

Jika sebelumnya kita mengecek dan ternyata $N$ merupakan bilangan bulat positif, bagaimana caranya agar kita bisa mengetahui apakah $N$ merupakan bilangan genap?

Perhatikan bahwa jika suatu bilangan merupakan bilangan genap, maka bilangan tersebut akan habis dibagi (tanpa sisa) oleh 2. Lalu, bagaimana caranya mengetahui sisa bagi suatu bilangan dengan bilangan lain?

Kita akan menggunakan *modulo* ✨

Apa itu *modulo*?

Bagi yang belum tahu (mungkin tempe 😁), *modulo* yang biasanya disingkat dengan *mod* merupakan operasi untuk mencari sisa pembagian. Misalnya $5$ $mod$ $3$ hasilnya 2, karena 5 dibagi 3 akan bersisa 2. Nah, sudah paham kan?

Jadi, karena bilangan genap selalu habis dibagi 2, maka kita hanya perlu mengecek apakah $N$ $mod$ $2$ sama dengan 0 (nol).

Pada C++, *modulo* dilambangkan dengan tanda persen (%).

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
    if(N > 0) {
      if(N % 2 == 0) {
        cout << N;
      }
    }
    return 0;
  }
```
</details>

## Komentar

Kita menggunakan `if` di dalam `if` agar ketika kondisi pada `if` pertama terpenuhi, barulah `if` kedua akan dijalankan. Jika kondisi pada `if` pertama tidak terpenuhi, yang artinya $N$ tidak lebih dari nol, maka kita tidak perlu melanjutkan tahap berikutnya untuk mengecek apakah $N$ merupakan bilangan bulat genap.

## Materi yang Berhubungan

- [C++ If ... Else](https://www.w3schools.com/cpp/cpp_conditions.asp)