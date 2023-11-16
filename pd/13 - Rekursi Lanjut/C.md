# [C. Permutasi Zig-Zag](https://tlx.toki.id/courses/basic/chapters/13/problems/C)

Author: Hamiz Ghani

Pada soal ini kita akan menuliskan setiap permutasi dari digit $1,2,\dots,N$ yang memenuhi kondisi berikut :

- Digit yang di tengah lebih kecil daripada kedua digit lainnya.
- Digit yang di tengah lebih besar daripada kedua digit lainnya.

Atau dapat kita tuliskan, untuk setiap $a[x]$ dimana $1≤x≤N-1$, $a[x]$ selalu memenuhi salah satu dibawah ini :
- $a[x-1]>a[x]$ dan $a[x]<a[x+1]$
- $a[x-1]<a[x]$ dan $a[x]>a[x+1]$

Apabila untuk suatu permutasiterdapat $a[x]$ ang tidak memenuhi kondisi diatas, maka dipastikan permutasi tersebut bukan permutasi zig-zag

Kita dapat menggunakan fungsi rekursi yang akan mencetak semua permutasi yang kita definisikan sebagai `perm(x,n)` dibawah ini:

```c++
void perm(int n, int x) {
  if (x == n) {
    for (int i = 0; i < n; i++) {
      cout << a[i];
    }
    cout << endl;
    return;
  }
  for (int i = 1; i <= n; i++) {
    if (!vis[i]) {
      vis[i] = true;
      a[x] = i;
      perm(n, x + 1);
      vis[i] = false;
    }
  }
}
```

Kemudian kita akan menambahkan suatu looping yang berguna untuk mengecek apakah permutasi itu zigzag atau bukan. Kita akan buat suatu kondisi yang apabila kondisi itu terpenuhi, maka permutasi tersebut bukan zigzag (kebalikan kondisi di atas).

- $a[i] > a[i - 1]$ dan $a[i] < a[i + 1]$
- $a[i] < a[i - 1]$ dan $a[i] > a[i + 1]$

untuk suatu $i$, $1≤i≤N$.

Sehingga didapatkan fungsi akhir `perm(n,x)` sebagai berikut:

```c++
void perm(int n, int x) {
  if (x == n) {
    for (int i = 1; i < n - 1; i++) {
      if ((a[i] > a[i - 1] && a[i] < a[i + 1]) ||
          (a[i] < a[i - 1] && a[i] > a[i + 1]))
        return;
    }
    for (int i = 0; i < n; i++) {
      cout << a[i];
    }
    cout << endl;
    return;
  }
  for (int i = 1; i <= n; i++) {
    if (!vis[i]) {
      vis[i] = true;
      a[x] = i;
      perm(n, x + 1);
      vis[i] = false;
    }
  }
}
```

`perm(n,x)` memiliki dua statement
- $n$, yaitu sampai bilangan ke berapa permutasi di-generate
- $x$, yaitu sudah sampai bilangan ke berapa di permutasi tersebut

Apabila $x=n$ maka kita akan melanjutkan ke pengecekan.


Kompleksitas Waktu: $O(N!)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
int m;
int a[15];
bool vis[15];
void perm(int n, int x) {
  if (x == n) {
    for (int i = 1; i < n - 1; i++) {
      if ((a[i] > a[i - 1] && a[i] < a[i + 1]) ||
          (a[i] < a[i - 1] && a[i] > a[i + 1]))
        return;
    }
    for (int i = 0; i < n; i++) {
      cout << a[i];
    }
    cout << endl;
    return;
  }
  for (int i = 1; i <= n; i++) {
    if (!vis[i]) {
      vis[i] = true;
      a[x] = i;
      perm(n, x + 1);
      vis[i] = false;
    }
  }
}
main() {
  cin >> m;
  perm(m, 0);
}
```
</details>



<!-- Tambahkan komentar apabila perlu
-->
## Komentar

- Kalian juga bisa menggunakan fungsi bawaan C++ yaitu `next_permutation()` untuk mempersingkat. 


<!-- Tambahkan referensi link materi yang berhubungan apabila perlu
-->
## Materi Yang Berhubungan
    
-  [next_permutation in C++](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/)


<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal 1](link-soal)
- [Nama Soal II](link-soal)

-->