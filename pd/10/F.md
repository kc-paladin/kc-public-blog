# [Teman Dekat](https://tlx.toki.id/courses/basic/chapters/10/problems/F)

Author: Hamiz Ghani

Pada soal ini kita akan menerima 2 buah array $X$ dan $Y$ yang dijadikan sebagai faktor acuan untuk $N$ buah murid. Kemudian didefinisikan $T[i][j] = abs(X[j]-X[i])^d + abs(Y[j]-Y[i])^d$ sebagai nilai kedekatan antara murid ke-i dan murid ke-j  dan $d$ merupakan konstanta yang ditentukan oleh Pak Dengklek

Kita dapat melakukan cek pada setiap $T[i][j]$ dimana $1≤i,j≤N$. Disini saya membuat 2 buah variabel baru yaitu $ansmin$ yang mencatat nilai paling minimal untuk $T[i][j]$ serta $ansmax$ yang mencatat nilai maksimalnya. Perlu diingat bahwa kita tidak akan melakukan pengecekan pada $T[i][j]$ untuk suatu $i=j$ karena tidak mungkin murid tersebut mempunyai nilai kedekatan dengan dirinya sendiri.

Kompleksitas Waktu: $O(N^2)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
int n, d;
int x[1005];
int y[1005];
int t[1005][1005];
int ansmin = 10000000;
int ansmax = 0;
int power(int x, int y) {
  int temp = 1;
  for (int i = 1; i <= y; i++) temp *= x;
  return temp;
}
main() {
  cin >> n >> d;
  for (int i = 1; i <= n; i++) {
    cin >> x[i] >> y[i];
  }
  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j++) {
      if (i == j) continue;
      t[i][j] = power(abs(x[i] - x[j]), d) + power(abs(y[i] - y[j]), d);
      ansmin = min(ansmin, t[i][j]);
      ansmax = max(ansmax, t[i][j]);
    }
  }
  cout << ansmin << " " << ansmax << endl;
}
```

</details>


Saya juga membuat suatu fungsi `power(x,y)` yang akan mengembalikan nilai dari $X^d$. Fungsi ini akan membantu untuk menghitung nilai dari $T[i][j] = abs(X[j]-X[i])^d + abs(Y[j]-Y[i])^d$



<!-- Tambahkan komentar apabila perlu
-->
## Komentar
    
- fungsi `abs()` merupakan fungsi yang mengembalikan nilai absolut, fungsi ini merupakan bawaan dari C++ sehingga kita tidak perlu mendefinisikanya lagi


<!-- Tambahkan referensi link materi yang berhubungan apabila perlu

## Materi Yang Berhubungan
    
-  [swap() in C++](https://www.geeksforgeeks.org/swap-in-cpp/)
-->

<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal 1](link-soal)
- [Nama Soal II](link-soal)

-->