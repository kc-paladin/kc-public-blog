# [A. Seleksi Olimpiade](https://tlx.toki.id/courses/competitive/chapters/01/problems/A)

Author: Muhammad Hasan

Untuk menyelesaikan persoalan ini, pada dasarnya kita perlu mengetahui peringkat peserta $ID$ yang diberikan. Jika peringkatnya kurang dari atau sama dengan $M$, maka kita kelurkan `YA` dan apabila tidak kita keluarkan `TIDAK`.

Salah satu cara untuk menyelesaikan soal ini adalah dengan menggunakan *metode pengurutan*.

Kita dapat mendefinisikan untuk setiap peserta $i$ ($1 \leq i \leq N$) sebagai $P_i$ di mana skor $P_i$ didefinisikan sebagai $(X_{i},Y_{i},Z_{i})$:

- $X_i$ = skor $P_i$ untuk sesi pertama
- $Y_i$ = skor $P_i$ untuk sesi kedua
- $Z_i$ = skor $P_i$ untuk sesi ketiga

Dari uraian soal kita dapat melihat bahwa **peringkat** $P_i$ $<$ **peringkat** $P_j$ jika hal berikut berlaku:

- $Z_i$ > $Z_j$
- $Z_i = Z_j$ dan $Y_i > Y_j$
- $Z_i = Z_j$ dan $Y_i = Y_j$ dan $X_i > X_j$

> **Catatan:** Perhatikan juga bahwa tidak ada $P_i = P_j$ untuk setiap $i \neq j$

Oleh karena itu, untuk mengatasi masalah ini, kita dapat melakukan hal berikut:

- Buat struktur peserta dengan `struct` dan *override* operator `<`.
- Masukkan semua skor-skor peserta ke dalam suatu `vector / array`
- Urutkan kumpulan peserta tersebut
- Iterasi setiap peserta dan periksa apakah peringkat peserta dengan $ID$ tersebut peringkatnya $\leq M$

Kompleksitas Waktu: $O(N \log N)$
Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

struct participant {
  string id;
  int x, y, z;

  bool operator<(const participant& other) {
    if (z == other.z) {
      if (y == other.y) {
        return x > other.x;
      }
      return y > other.y;
    }
    return z > other.z;
  };
};

void solve() {
  int n, m;
  cin >> n >> m;
  string id;
  cin >> id;
  vector<participant> p(n);
  for (int i = 0; i < n; i++) {
    cin >> p[i].id >> p[i].xs1 >> p[i].y s2 >> p[i].zs3;
  }
  sort(p.begin(), p.end());
  for (int i = 0; i < n; i++) {
    if (p[i].id == id) {
      int rank = i + 1;
      cout << (rank <= m ? "YA" : "TIDAK") << '\n';
      return;
    }
  }
}

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  int tc = 1;
  cin >> tc;
  for (int t = 1; t <= tc; t++) {
    solve();
  }

  return 0;
}
```
</details>

## Komentar
    
- Ada banyak cara lain untuk menyimpan informasi skor peserta, diantaranya menggunakan `class` ataupun `tuple` dalam C++.
- Cara lain dalam menyelesaikan soal ini adalah kita check untuk setiap peserta $i$ dan kita coba bandingkan dengan peserta lainnya, apabila terdapat $K$ peserta $j$ dengan $P_j < P_i$, maka kita bisa dapat bahwa peserta $i$ memiliki peringkat $K + 1$. Namun, cara ini memiliki kompleksitas waktu $O(N^2)$
    
## Materi Yang Berhubungan

- [C++ Struct](https://www.w3schools.com/cpp/cpp_structs.asp)
- [C++ Overloading Operator](https://www.tutorialspoint.com/cplusplus/cpp_overloading.htm )
    
<!-- Tambahkan soal yang berhubungan disini

## Soal Yang Berhubungan -->

