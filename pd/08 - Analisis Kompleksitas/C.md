# [C. Bilangan Agak Prima](https://tlx.toki.id/courses/basic/chapters/08/problems/C)

Author: Ackhava Adam Malonda

Soal ini adalah modifikasi minor dari pengecekan jumlah pembagi standar.

Algoritma utamanya sangat mirip (namun berbeda pada beberapa hal kecil), yakni seperti berikut untuk sebuah bilangan $X$:
- Lakukan perulangan untuk semua bilangan bulat dari $1$ sampai $\sqrt{X}$ dan anggap sebagai $i$. Lalu:
    - Cek apakah $X$ habis dibagi $i$. Jika ya, maka tambahkan jumlah pembagi dengan $1$. Hal ini guna untuk menghitung semua pembagi yang tidak lebih dari $\sqrt{X}$.
    - Perika apakah $\sqrt{X}=i$. Jika tidak, dan kondisi diatas terpenuhi, maka tambahkan jumlah pembagi dengan $1$. Hal ini adalah untuk menghitung pembagi yang lebih dari $\sqrt{X}$.

Untuk memeriksa kondisi yang melibatkan akar dari $X$, kuadratkan kedua sisi. Contohnya adalah $i\leq\sqrt{X}$ menjadi $i^{2}\leq X$.

Pada soal, bilangan "agak prima" memiliki tidak lebih dari $2$ faktor selain bilangan itu sendiri dan $1$. Sebagai hasilnya, jika $1$ dan $X$ dihitung juga maka ada maksimal $4$ faktor. Alhasil, jika jumlah pembagi lebih dari $4$ cetak `"TIDAK"`, dan selain itu cetak `"YA"`.

Kompleksitas Waktu: $O(N\sqrt{X_{max}})$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  cin.tie(0);
  cout.tie(0);
  ios_base::sync_with_stdio(false);

  int t;
  cin >> t;

  for (int i = 0; i < t; i++) {
    int x;
    cin >> x;

    int divisor = 1;  // Pembagi paling kecil
    int divs = 0;     // Banyak pembagi

    while (((divisor * divisor) <= x))  // Cari semua pembagi x
    {
      if ((x % divisor) == 0)  // Jika dapat dibagi
      {
        divs++;
        if ((divisor * divisor) != x)  // Jika bukan akar kuadrat, maka tambahkan x/divisor juga
        {
          divs++;
        }
      }

      divisor++;
    }

    if (divs <= 4) {
      cout << "YA\n";
    } else {
      cout << "BUKAN\n";
    }
  }
}
```
</details>

## Komentar
- Hati-hati saat `divisor` sama dengan akar kuadrat dari `x`. Kasus ini hanya dihitung sekali, karena `divisor` dan `x / divisor` memiliki nilai yang sama.

## Materi Yang Berhubungan
- [Find all divisors of a natural number](https://www.tutorialspoint.com/find-all-divisors-of-a-natural-number-set-2-in-cplusplus)
