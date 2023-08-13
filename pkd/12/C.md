# [C. Segitiga Bebek](https://tlx.toki.id/courses/competitive/chapters/12/problems/C)

Author: Evelyn

Pada soal ini, kita akan diberikan posisi $N$ ekor bebek, dengan bebek ke-$i$ $(1 \leq i \leq N)$ berada pada posisi $(x_i, y_i)$. Kemudian, kita diminta untuk mencari luas segitiga minimum yang dapat dibentuk oleh tiga ekor bebek, artinya semua segitiga lain harus memiliki luas yang lebih besar dan tidak ada segitiga lain yang memiliki luas yang sama dengan luas segitiga minimum.

Karena batas nilai $N$ yang cukup kecil (lihat pada bagian **Batasan**), kita bisa melakukan *brute force* untuk mencari semua kombinasi pasangan 3 titik yang akan kita gunakan untuk membentuk sebuah segitiga.

Untuk setiap pasangan 3 titik $(i, j, k)$, dengan $i \neq j \neq k$, kita hitung luas segitiga yang dibentuk oleh bebek ke-$i$, bebek ke-$j$, dan bebek ke-$k$.

Rumus luas segitiga yang biasanya kita ketahui adalah $\frac{1}{2} × a × t$, dengan $a$ adalah alas segitiga, dan $t$ adalah tinggi segitiga. Namun, di soal ini, kita tidak tahu bagian mana yang menjadi alas maupun tinggi dari segitiga.

Kita akan menghitung luasnya dengan metode *Shoelace Formula* (*Shoelace Algorithm*).

Apa itu *Shoelace Formula*?

Singkatnya, *Shoelace Formula* merupakan suatu metode untuk menghitung luas suatu bangun datar jika diberikan koordinat dari titik-titik sudut bangun datar tersebut.

Misalkan suatu bangun datar memiliki titik-titik sudut pada koordinat $(x_1, y_1)$, $(x_2, y_2)$, ..., $(x_n, y_n)$.

Luas bangun datar tersebut adalah:

$$\frac{1}{2} \left| (x_1y_2 + x_2y_3 + ... + x_{n - 1}y_n + x_ny_1) - (x_2y_1 + x_3y_2 + ... + x_ny_{n - 1} + x_1y_n) \right|$$

Dengan menggunakan metode ini, kita akan menghitung luas tiap segitiga yang dibentuk oleh 3 ekor bebek.

Luas segitiga yang dibentuk oleh bebek ke-$i$, bebek ke-$j$, dan bebek ke-$k$ adalah:

$$\frac{1}{2} \left| (x_iy_j + x_jy_k + x_ky_i) - (x_jy_i + x_ky_j + x_iy_k) \right|$$

Kita akan mencari luas semua segitiga yang dapat dibentuk. Kemudian, kita pilih luas segitiga minimum sebagai jawabannya. 

Ingat bahwa 3 ekor bebek yang kita pilih bisa saja membentuk satu garis lurus. Jika demikian, maka luas daerah yang dibentuk akan menjadi $0$. Untuk kasus ini, kita tidak boleh memperhitungkannya sebagai suatu segitiga.

Untuk mencetak luas segitiga minimum sebagai jawaban dengan dua desimal, kita akan menggunakan `fixed` dan fungsi `setprecision()` pada C++.

**Contoh**

```c++
float x = 3.14657;
cout << fixed << setprecision(3) << x;
```

Pada potongan *code* di atas, nilai $x$ akan dicetak sampai 3 desimal, yaitu 3.146.

Kemudian, untuk $N < 3$, jawabannya pasti `-1` karena untuk membentuk sebuah segitiga, kita membutuhkan minimal 3 ekor bebek.

Kompleksitas Waktu: $O(N^3)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
# include <bits/stdc++.h>
using namespace std;

int main() {
  int N;  cin >> N;

  double x[N + 1], y[N + 1];
  for(int i = 1; i <= N; i++) {
    cin >> x[i] >> y[i];
  }

  double ans = LLONG_MAX;
  bool same = true;

  for(int i = 1; i <= N - 2; i++) {
    for(int j = i + 1; j <= N - 1; j++) {
      for(int k = j + 1; k <= N; k++) {
        double area = abs((x[i] * y[j] + x[j] * y[k] + x[k] * y[i]) - (x[j] * y[i] + x[k] * y[j] + x[i] * y[k])) / 2;
        if(area > 0) {
          if(area < ans) {
            ans = area;
            same = false;
          } else if(area == ans) {
            same = true;
          }
        }
      }
    }
  }

  if(same) {
    cout << fixed << setprecision(2) << -1;
  } else {
    cout << fixed << setprecision(2) << ans;
  }

  return 0;
}
```
</details>

## Materi yang Berhubungan

- [Shoelace Formula](https://www.101computing.net/the-shoelace-algorithm/)

- [C++ fixed and setprecision()](https://www.simplilearn.com/tutorials/cpp-tutorial/cpp-setprecision)