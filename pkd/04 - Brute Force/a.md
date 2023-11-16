# [Refleksi Matriks](https://tlx.toki.id/courses/competitive/chapters/04/problems/A)

Author: Hamiz Ghani

Pada soal ini kita akan menerima dua buah matriks yang memiliki ukuran $N × N$. Kita akan membandingkan kedua buah matriks tersebut apakah matriks pertama identik dengan matriks kedua atau merupakan refleksi dari matriks kedua dan sebaliknya. Refleksi bisa dengan sumbu vertikal, sumbu horizontal, sumbu diagonal ke kiri bawah, atau dengan sumbu diagonal ke kanan bawah. Apabila matriks pertama dan kedua tidak memenuhi semua kondisi di atas, maka kedua matriks tersebut tidak identik.

Berikut implementasi untuk masing-masing kondisi :

- Identik
```c++
bool identik = 1;
for (int i = 0; i < n; i++) {
  for (int j = 0; j < m; j++) {
    cin >> b;
    if (b != a[i][j]) {
      identik = 0;
    }
  }
}
```
- Sumbu Vertikal :
```c++
bool vertical = 1;
for (int i = 1; i < n; i++) {
  for (int j = 1; j < m; j++) {
    cin >> b;
    if (b != a[i][(m - 1) - j]) {
      vertikal = 0;
    }
  }
}
```
- Sumbu Horizontal
```c++
bool horisontal = 1;
for (int i = 1; i < n; i++) {
  for (int j = 1; j < m; j++) {
    cin >> b;
    if (b != a[(n - 1) - i][j]) {
      horisontal = 0;
    }
  }
}
```
- Sumbul Diagonal Kiri Bawah
```c++
bool diagonalkiribawah = 1;
for (int i = 0; i < n; i++) {
  for (int j = 0; j < m; j++) {
    cin >> b;
    if (b != a[(m - 1) - j][(n - 1) - i]) {
      diagonalkiribawah = 0;
    }
  }
}
```
- Sumbu Diagonal Kanan Bawah
```c++
bool diagonalkananbawah = 1;
for (int i = 0; i < n; i++) {
  for (int j = 0; j < m; j++) {
    cin >> b;
    if (b != a[j][i]) {
      diagonalkananbawah = 0;
    }
  }
}
```

Baris pertama dalam setiap code adalah tipe data $bool$ yang akan bernilai $TRUE$ apabila kondisi terpenuhi dan akan bernilai $FALSE$ apabila kondisi tidak terpenuhi. Apabila tidak ada kondisi yang terpenuhi maka output `tidak identik`

Kompleksitas Waktu: $O(N^2)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
int main() {
  int n, m;
  cin >> n >> m;
  int a[n][m];
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      cin >> a[i][j];
    }
  }
  bool identik = true;
  bool vertikal = true;
  bool horisontal = true;
  bool diagonalkananbawah = true;
  bool diagonalkiribawah = true;
  cin >> n >> m;
  int b;
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      cin >> b;
      if (b != a[i][j]) {
        identik = false;
      }
      if (b != a[i][(m - 1) - j]) {
        vertikal = false;
      }
      if (b != a[(n - 1) - i][j]) {
        horisontal = false;
      }
      if (b != a[j][i]) {
        diagonalkananbawah = false;
      }
      if (b != a[(m - 1) - j][(n - 1) - i]) {
        diagonalkiribawah = false;
      }
    }
  }
  if (identik) {
    cout << "identik" << endl;
  } else if (vertikal) {
    cout << "vertikal" << endl;
  } else if (horisontal) {
    cout << "horisontal" << endl;
  } else if (diagonalkananbawah) {
    cout << "diagonal kanan bawah" << endl;
  } else if (diagonalkiribawah) {
    cout << "diagonal kiri bawah" << endl;
  } else {
    cout << "tidak identik" << endl;
  }
}
```
</details>



<!-- Tambahkan komentar apabila perlu

## Komentar
    
- Komentar I
- Komentar II

-->

<!-- Tambahkan referensi link materi yang berhubungan apabila perlu
-->
## Materi Yang Berhubungan
    
-  [Two Dimensional Array in C++](https://www.digitalocean.com/community/tutorials/two-dimensional-array-in-c-plus-plus)


<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal 1](link-soal)
- [Nama Soal II](link-soal)

-->