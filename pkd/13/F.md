# [The Alien of Yogyakarta The Curse of The IFO](https://tlx.toki.id/courses/competitive/chapters/13/problems/F)

Author: Hamiz Ghani

Kita akan menerima $N × M$ buah petak. Petak tersebut berisi nilai-nilai kualitas cacing dan apabila nilai $a[i][j]=9999$ maka petak tersebut berisi batu. Batasan batu yang boleh diambil adalah $B$. Tentukan nilai maksimum kualitas cacing dan batu apabila pengambilan petak harus berbentuk persegi panjang sempurna.

Soal ini dapat diselesaikan dengan brute force kemungkinan persegi panjang, kemudian menghitung kualitas cacing dan batu yang ada di dalam area tersebut.

Kita dapat menghitung total kualitas cacing dan total batu yang ada di dalam suatu persegi panjang dengan menggunakan suatu prefiks dua dimensi.

```c++
for (int i = 1; i <= n; i++) {
  for (int j = 1; j <= m; j++) {
    cin >> a[i][j];
    prefb[i][j] = prefb[i - 1][j] + prefb[i][j - 1] - prefb[i - 1][j - 1];
    if (a[i][j] == 9999) prefb[i][j]++;
    prefq[i][j] = prefq[i - 1][j] + prefq[i][j - 1] - prefq[i - 1][j - 1];
    if (a[i][j] != 9999) prefq[i][j] += a[i][j];
  }
}
```

$prefq[i][j]$ menyimpan total nilai $a[x][y]$ yang bukan batu dimana $x \leq i$ dan $y \leq j$. Sedangkan $prefb[i][j]$ menyimpan total batu dimana $x \leq i$ dan $y \leq j$.

Apabila untuk suatu petak batu $a[i][j]=9999$, tambahkan nilai $prefb[i][j]$ dengan $1$. Selain itu tambahkan $prefq[i][j]$ dengan $a[i][j]$.

Kemudian lakukan for loop bertingkat untuk masing-masing kemungkinan persegi panjang. Serta, cek total qualitas cacingnya (saya menyimpannya dalam variabel $sum$) dan banyak batu yang terangkut (variabel $batu$). Suatu persegi panjang kita anggap invalid apabila banyak $batu>b$, Selain itu bandingkan nilai $sum$ dengan jawaban sebelumnya.

```c++
for (int i = 1; i <= n; i++) {
  for (int j = i; j <= n; j++) {
    for (int k = 1; k <= m; k++) {
      for (int l = k; l <= m; l++) {
        int sum = prefq[j][l] - prefq[i - 1][l] - prefq[j][k - 1] +
                  prefq[i - 1][k - 1];
        int batu = prefb[j][l] - prefb[i - 1][l] - prefb[j][k - 1] +
                   prefb[i - 1][k - 1];
        if (batu <= b) {  // persegi panjang dapat diambil
          if (sum > ans.fi) {
            ans.fi = sum;
            ans.se = batu;
          }
        }
      }
    }
  }
}
		
```
Kompleksitas Waktu: $O(N*M)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
#define pii pair<int, int>
using namespace std;
int n, m, b;
int a[55][55];
int prefq[55][55];
int prefb[55][55];
pii ans;
main() {
  cin >> n >> m >> b;
  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= m; j++) {
      cin >> a[i][j];
      prefb[i][j] = prefb[i - 1][j] + prefb[i][j - 1] - prefb[i - 1][j - 1];
      if (a[i][j] == 9999) prefb[i][j]++;
      prefq[i][j] = prefq[i - 1][j] + prefq[i][j - 1] - prefq[i - 1][j - 1];
      if (a[i][j] != 9999) prefq[i][j] += a[i][j];
    }
  }
  for (int i = 1; i <= n; i++) {
    for (int j = i; j <= n; j++) {
      for (int k = 1; k <= m; k++) {
        for (int l = k; l <= m; l++) {
          int sum = prefq[j][l] - prefq[i - 1][l] - prefq[j][k - 1] +
                    prefq[i - 1][k - 1];
          int batu = prefb[j][l] - prefb[i - 1][l] - prefb[j][k - 1] +
                     prefb[i - 1][k - 1];
          if (batu <= b) {
            if (sum > ans.fi) {
              ans.fi = sum;
              ans.se = batu;
            }
          }
        }
      }
    }
  }
  cout << ans.fi << " " << ans.se << endl;
}
```
</details>

## Materi Yang Berhubungan
    
- [Prefix Sum of 2D Array](https://www.geeksforgeeks.org/prefix-sum-2d-array/)