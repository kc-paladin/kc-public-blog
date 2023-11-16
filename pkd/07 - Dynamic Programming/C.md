# [C. Penukaran Emas](https://tlx.toki.id/courses/competitive/chapters/07/problems/C)

Author: Eileen Camelia Limneus

Halo teman - teman, sudah coba menyelesaikan soal ini belum?
Soal ini meminta kami untuk menghitung total berat emas maksimum dengan aturan yang telah tertera. Caranya bagaimana? 

**Solusi Rekursi**

1. Buatlah sebuah variable yang menampung hasil penukaran dalam sebuah fungsi. Dalam fungsi tersebut, cek jika berat emas sebelum penukaran lebih dari atau sama dengan perkiraaan berat emas setelah penukaran.
2. Jika ya, maka berat emas tersebut sudah yang paling maksimum sehingga tidak perlu memanggil fungsi proses penukaran lagi. Jika tidak, panggil fungsi proses penukaran.

**Solusi Dynamic Programming**

1. Buatlah sebuah array dan inisialisasi kasus dasarnya bernilai 0.
2. Pakai fungsi perulangan `for` untuk mengiterasi dari 1 sampai n.
3. Dalam setiap perulangan, inisialisasi array tersebut dengan berat maksimumnya. (Gunakan fungsi [max](https://www.geeksforgeeks.org/stdmax-in-cpp/))

<details>
  <summary>Solution Code - Recursive</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int tukar(int n) {
  int res = n / 2 + n / 3 + n / 4;

  if (n >= res) {
    return n;
  } else {
    return tukar(n / 2) + tukar(n / 3) + tukar(n / 4);
  }
}

int main() {
  int n;
  cin >> n;
  cout << tukar(n);
}
```
</details>

<details>
  <summary>Solution Code - Dynamic Programming</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  int n;
  cin >> n;

  int dp[n + 1];
  dp[0] = 0;

  for (int i = 1; i <= n; i++) {
    dp[i] = max(i, dp[i / 2] + dp[i / 3] + dp[i / 4]);
  }
  cout << dp[n];
}
```
</details>

## Komentar
    
- Dalam solusi rekursif, ketika menghitung tukar(n), terdapat banyak pemanggilan rekursif berulang untuk nilai yang sama dari n/2, n/3, dan n/4. Ini mengakibatkan banyak perhitungan yang berulang-ulang, mengurangi efisiensi program secara keseluruhan.
- Dalam solusi dengan pendekatan Dynamic Programming, kita menggunakan array dp untuk menyimpan hasil perhitungan secara iteratif, sehingga tidak perlu menghitung ulang nilai yang sama. Hal ini mengurangi kompleksitas waktu dan meningkatkan efisiensi.

## Materi Yang Berhubungan
    
- [Introduction to Recursion](https://www.geeksforgeeks.org/introduction-to-recursion-data-structure-and-algorithm-tutorials/)
- [Dynamic Programming](https://www.geeksforgeeks.org/dynamic-programming/)
