# [A. Parsel Telur Bebek](https://tlx.toki.id/courses/competitive/chapters/05/problems/A)

Author: Yose Yehezkiel Maranata

Halo semua! :v

Lagi-lagi Pak Dengklek dan bebek-bebeknya buat masalah... 

Ringkasnya kita diminta untuk: 
- diberikan array dengan $N$ bilangan dan juga sebuah bilangan $M$ 
- cari berapa banyak nilai $X$ yang mungkin dimana $X$ adalah bilangan yang mungkin agar  $M = \displaystyle\sum_{i=1}^{N} \frac{X}{ar[i]}$.
- $\displaystyle\sum_{i=1}^{N} \frac{X}{ar[i]}$ artinya adalah hasil penjumlahan dari $X$ dibagi dengan $ar[i]$ untuk semua $ 1 \le i \le N$.

Pertama-tama kita akan lihat dulu ke solusi naifnya. Kita cek satu-persatu nilai $X$ dan cari mana saja bilangan $X$ yang mungkin. Misalkan $T$ adalah hasil dari $\displaystyle\sum_{i=1}^{N} \frac{X}{ar[i]}$. Kita coba menggunakan tes sampel yang diberikan, maka kita dapatkan tabel berikut : 

[![image.png](https://i.postimg.cc/hPvrvKRV/image.png)](https://postimg.cc/hfFx3WjG)

Tentu saja solusi naif ini tidak akan mendapat verdict `AC` karena kompleksitas waktunya $O(N^2 \times M)$, hal ini dikarenakan kita harus mengecek nilai $X$ hingga $N \times M$ dan harus melakukan loop pada array yang sizenya $N$. 

Namun, kita dapat melihat dari tabel bahwa nilai $T$ selalu naik beriringan dengan naiknya nilai $X$. Maka optimisasi yang bisa kita lakukan adalah melakukan *Binary Search*! 

Lebih tepatnya disebut sebagai BSTA (*Binary Search The Answer*) dimana kita melakukan binary search kepada nilai $X$. Kita cari nilai $X$ mana sehingga nilai $T$ sama dengan $M$ Dengan memanfaatkan BSTA kita bisa mengoptimisasi pencarian nilai $X$ dari $O(N \times M)$ menjadi $O(\log(N \times M))$. 

Kompleksitas Waktu: $O(\log(N\times M) \times N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  int n, m;
  cin >> n >> m;

  long long ar[n + 5];
  for (int i = 0; i < n; i++) cin >> ar[i];
  long long l = 0, r = 1ll << 50;
  long long posr = l;
  // binary search most right possible answer
  while (l <= r) {
    long long mid = (l + r) / 2;
    long long t = 0;
    for (int i = 0; i < n; i++) {
      t += mid / ar[i];
    }
    if (t <= m)
      posr = mid, l = mid + 1;
    else
      r = mid - 1;
  }

  l = 0, r = 1ll << 50;
  long long posl = r;
  // binary search most left possible answer
  while (l <= r) {
    long long mid = (l + r) / 2;
    long long t = 0;
    for (int i = 0; i < n; i++) {
      t += mid / ar[i];
    }
    if (t < m)
      l = mid + 1;
    else
      posl = mid, r = mid - 1;
  }
  cout << max(0ll, posr - posl + 1);
}
```
</details>

## Komentar
    
- BSTA termasuk kedalam bab divide and conquer karena kita melakukan eliminasi pada pencarian yang tidak perlu. 
- Agar aman, $N\times M$ pada Solution Code dibuat $2^{50}$ atau `1ll << 50`.

## Soal Yang Berhubungan
    
- [Factory Machines](https://cses.fi/problemset/task/1620)
- [Maximum Median](https://codeforces.com/contest/1201/problem/C)
- [Array Division](https://cses.fi/problemset/task/1085/)


