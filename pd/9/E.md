# [E. Perkalian Matriks](https://tlx.toki.id/courses/basic/chapters/09/problems/E)

Author: Evelyn

Pada soal ini, ktia akan diberikan dua buah matriks, yaitu matriks $A$ dan matriks $B$. Lalu, kita diminta untuk mengalikan kedua matriks tersebut dan mencetak matriks hasil perkalian tersebut.

Jadi, perkalian matriks itu seperti apa sih?

Kita punya dua buah matriks, yaitu matriks $A$ yang berukuran $N × M$ dan matriks $B$ yang berukuran $M × P$. Agar kedua matriks dapat dikalikan, maka jumlah kolom pada matriks $A$ harus sama dengan jumlah baris pada matriks $B$. Matriks akhir hasil perkalian tersebut akan menghasilkan matriks $C$ berukuran $N × P$.

$C[i][j]$ merupakan elemen pada baris $i$ dan kolom $j$ pada matriks $C$.

Definisi $C[i][j]$ untuk setiap $i$ $(1 \le i \le N)$ dan untuk setiap $j$ $(1 \le j \le P)$ adalah sebagai berikut:

$$C[i][j] = \Sigma_ {k = 1}^M A[i][k] × B[k][j]$$

Artinya

$$C[i][j] = A[i][1] × B[1][j] + A[i][2] × B[2][j] + A[i][3] × B[3][j] + ... + A[i][M] × B[M][j]$$

Dengan demikian, kita hanya perlu menggunakan perulangan `for`.

Kompleksitas Waktu: $O(NMP)$

Kompleksitas Memori: $O(NM + MP + NP)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  int N, M, P;  cin >> N >> M >> P;

  int A[N + 1][M + 1], B[M + 1][P + 1], C[N + 1][P + 1];

  for(int i = 1; i <= N; i++) {
    for(int j = 1; j <= M; j++) {
      cin >> A[i][j];
    }
  }

  for(int i = 1; i <= M; i++) {
    for(int j = 1; j <= P; j++) {
      cin >> B[i][j];
    }
  }

  memset(C, 0, sizeof(C));

  for(int i = 1; i <= N; i++) {
    for(int j = 1; j <= P; j++) {
      for(int k = 1; k <= M; k++) {
        C[i][j] += A[i][k] * B[k][j];
      }
    }
  }

  for(int i = 1; i <= N; i++) {
    for(int j = 1; j <= P; j++) {
      cout << C[i][j] << " ";
    }
    cout << "\n";
  }

  return 0;
}
```
</details>

## Materi yang Berhubungan

- [C++ Arrays](https://www.w3schools.com/cpp/cpp_arrays.asp)