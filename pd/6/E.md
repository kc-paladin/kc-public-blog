# [E. Dua Pangkat](https://tlx.toki.id/courses/basic/chapters/06/problems/E)

Author: Eileen Camelia Limneus

Untuk persoalan ini, kita perlu memeriksa apakah bilangan yang diinput dapat terus dibagi dengan 2 hingga menjadi 1 atau tidak. Jika bisa, maka bilangan tersebut merupakan bilangan "dua pangkat". Jika tidak, maka bukan bilangan "dua pangkat".

Perhatikan bahwa kita dapat menggunakan fungsi perulangan `while` disini karena kita tidak mengetahui jumlah pasti iterasi yang perlu dilakukan. 

Jika kita tahu jumlah pasti iterasi yang perlu dilakukan, maka fungsi perulangan `for` akan lebih cocok untuk digunakan.

Kompleksitas Waktu: $O(log N)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  int n;
  cin >> n;

  while (n % 2 == 0) {
    n = n / 2;
  }

  if (n == 1) {
    cout << "ya";
  } else {
    cout << "bukan";
  }
}
```
</details>

## Komentar
    
- Program ini dapat diselesaikan dengan cara lain juga seperti menggunakan sistem bilangan biner dan operasi bitwise `AND`. Caranya adalah dengan mengecek kondisi `n & (n-1) == 0` dimana hasil dari operasi tersebut akan selalu 0 pada bilangan "dua pangkat".

## Materi Yang Berhubungan
    
- [C++ While Loop](https://www.geeksforgeeks.org/cpp-while-loop/)
- [Bitwise Operators in C/C++](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)
- [Sistem bilangan biner](https://id.wikipedia.org/wiki/Sistem_bilangan_biner)
