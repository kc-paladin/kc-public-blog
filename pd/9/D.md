# [D. Rotasi Matriks](https://tlx.toki.id/courses/basic/chapters/09/problems/D)

Author: Evelyn

Pada soal ini, kita diberikan sebuah matriks berukuran $N × M$ dan kita diminta untuk merotasikannya (memutarnya 90 derajat searah jarum jam).

$N$ menyatakan jumlah baris pada matriks dan $M$ menyatakan jumlah kolom pada matriks.

Kita akan menyimpan matriks dalam array dua dimensi, dengan $A[i][j]$ menyatakan elemen matriks pada baris ke-$i$ dan kolom ke-$j$.
```
A[1][1] A[1][2] A[1][3] ... A[1][M]
A[2][1] A[2][2] A[2][3] ... A[2][M]
.
.
A[N][1] A[N][2] A[N][3] ... A[N][M]
```

Matriks dibaca mulai dari kiri ke kanan pada baris pertama, lalu baris kedua, dan seterusnya hingga baris terakhir.

Setelah dirotasi, ukuran matriks akan berubah menjadi $M × N$.

Baris ke-1 akan diisi oleh elemen-elemen dari kolom ke-1 pada matriks awal. Urutan elemen dari kiri ke kanan berasal dari urutan elemen dari bawah ke atas pada matriks awal. Begitu pula untuk baris ke-2 hingga baris terakhir.

```
A[N][1] A[N - 1][1] A[N - 2][1] ... A[1][1]
A[N][2] A[N - 1][2] A[N - 2][2] ... A[1][2]
.
.
A[N][M] A[N - 1][M] A[N - 2][M] ... A[1][M]
```

**Contoh**

Matriks awal (Ukuran 3 × 2)
```
1 3
5 2
6 9
```

Matriks yang telah dirotasi (Ukuran berubah menjadi 2 × 3)
```
6 5 1
9 2 3
```

Jadi, kita hanya perlu mencetak matriks yang telah disimpan dengan urutan yang telah dirotasi.

Kompleksitas Waktu: $O(N × M)$

Kompleksitas Memori: $O(N × M)$


<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
int main() {
  int N, M;  cin >> N >> M;
  
  int A[N + 1][M + 1];

  for(int i = 1; i <= N; i++) {
    for(int j = 1; j <= M; j++) {
      cin >> A[i][j];
    }
  }

  for(int i = 1; i <= M; i++) {
    for(int j = N; j >= 1; j--) {
      cout << A[j][i] << " ";
    }
    cout << "\n";
  }

  return 0;
}
```
</details>

## Tambahan
Indeks terkecil pada array dimulai dari 0. Karena itu, ukuran array perlu ditambah sebesar 1 jika kita ingin memulai mengisi array dari indeks 1.

Kenapa begitu?

Misalnya, kita ingin menyimpan 5 buah data pada array. Jika kita mulai menyimpannya dari indeks 0, berarti kita menyimpan pada `arr[0]`, `arr[1]`, `arr[2]`, `arr[3]`, dan `arr[4]`. Kita bisa men-*set* ukuran array tersebut sebesar 5 (indeks 0 - 4).

Namun, jika kita ingin menyimpannya mulai dari indeks 1, kita harus men-*set* ukuran array tersebut sebesar 6 agar dapat menyimpan data-data tersebut pada `arr[1]`, `arr[2]`, `arr[3]`, `arr[4]`, dan `arr[5]`. Mengapa begitu? Jika kita men-*set* ukuran array tersebut sebesar 5, kita hanya bisa mengakses data pada indeks 0 - 4. Sedangkan ukuran 6 berarti kita bisa mengakses data pada indeks 0 - 5. Karena kita mulai dari indeks 1, maka kita akan membutuhkan indeks 5. Jadi, ukuran array yang diperlukan adalah 6.

Kalau kalian mau simpan matriksnya dari indeks 0 juga boleh ya :)

## Materi yang Berhubungan

- [C++ Arrays](https://www.w3schools.com/cpp/cpp_arrays.asp)