# [B. Petak Menarik](https://tlx.toki.id/courses/competitive/chapters/03/problems/B)

Author: Andreas Timothy

Pada problem ini kita diminta untuk mencari petak yang hasil perkalian dari tetangga-tetangganya sama dengan $K$.

Mirip seperti soal A sebelumnya, kita cukup melakukan linear search, yaitu mengecek hasil perkalian tetangga-tetangga dari setiap petak.

> **Disclaimer:** Pada kode dibawah saya menggunakan `std::pair` untuk mempermudah perbandingan 2 bilangan, tetapi hal itu tidak wajib.

Kompleksitas Waktu: $O(NM)$

Kompleksitas Memori: $O(NM)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int n, m, k, val, a[105][105];
pair<int, int> ans;

int main() {
  cin >> n >> m >> k;
  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= m; j++) {
      cin >> a[i][j];
    }
  }
  // inisialisasi ans
  ans = {1000, 1000};
  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= m; j++) {
      val = 1;
      if (i > 1) val *= a[i - 1][j];
      if (i < n) val *= a[i + 1][j];
      if (j > 1) val *= a[i][j - 1];
      if (j < m) val *= a[i][j + 1];

      // trik simple untuk komparasi
      // pair akan mengambil yang nilai firstnya terkecil
      // apabila nilai firstnya sama maka yang nilai secondnya terkecil akan
      // diambil
      // oleh karena itu kita set kolom sebagai first, baris sebagai second
      if (val == k) ans = min(ans, make_pair(j, i));
    }
  }
  // apabila tidak ada jawaban
  if (ans == make_pair(1000, 1000)) ans = {0, 0};
  cout << ans.second << ' ' << ans.first << '\n';
}
```

</details>

## Komentar

- Kita bisa saja menambahkan conditional tanpa menggunakan `pair`, tetapi dapat dilihat bahwa `pair` akan sangat memudahkan kita dalam banyak situasi, contohnya pada problem ini.

## Materi Yang Berhubungan

- [C++ Pair](https://www.geeksforgeeks.org/pair-in-cpp-stl/)
