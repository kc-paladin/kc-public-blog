# [H. Pola I](https://tlx.toki.id/courses/basic/chapters/06/problems/H)

Author: Eileen Camelia Limneus

Dalam soal ini, kita dapat lihat bahwa polanya adalah mengganti setiap kelipatan dari suatu bilangan $K$ dengan simbol `*`. Jika bukan kelipatan $K$, maka cukup kita cetak kembali bilangan tersebut.

Pertama, kita dapat menggunakan fungsi perulangan `for` untuk mengiterasi setiap bilangan dari $1$ hingga $N$.
Pada setiap iterasi, kita memeriksa apakah bilangan tersebut merupakan kelipatan dari $K$ menggunakan operator modulo `%`.
Sekali lagi, jika bilangan tersebut merupakan kelipatan dari K, kita mencetak karakter `*`. Jika tidak, kita mencetak bilangan itu sendiri.

Kedua, agar tidak terdapat spasi di akhir baris, kita dapat menggantinya dengan newline `\n` setelah bilangan terakhir menggunakan `if`.

Kompleksitas Waktu: $O(N)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  int n, k;
  cin >> n >> k;

  for (int i = 1; i <= n; i++) {
    if (i % k == 0) {
      cout << "* ";
    } else {
      cout << i << " ";
    }

    if (i == n) {
      cout << "\n";
    }
  }
}
```
</details>

## Komentar
    
- Ada cara lain untuk mengatur spasi dalam persoalan ini dan program di atas hanya salah satu caranya, jadi tidak harus sama persis ya.


## Materi Yang Berhubungan

- [C++ for Loop (With Examples)](https://www.geeksforgeeks.org/cpp-for-loop/)
- [Modulo Operator (%) in C/C++ with Examples](https://www.geeksforgeeks.org/modulo-operator-in-c-cpp-with-examples/)
