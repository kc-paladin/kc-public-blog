# [G. Jawbreaker I: Klik!](https://tlx.toki.id/courses/basic/chapters/13/problems/G)

Author: Yose Yehezkiel Maranata

Halo semua :wave:

Di blog ini kita akan belajar membuat algorithm untuk permainan Jawbreaker! :hushed:

Untuk permulaan kita akan sama-sama mengimplementasikan fitur Klik memanfaatkan rekursi. 

Deskripsi pada soal sudah jelas kita harus melakukan apa, namun apabila belum jelas bisa klik [Flood Fill Visualizer](https://flood-fill-visualizer.netlify.app/). Algorithm yang akan kita buat ini lebih akrab dikenal sebagai Flood Fill.

[![image.png](https://i.postimg.cc/DZY168Nq/image.png)](https://postimg.cc/7G0CYYw6)

Seperti pada gambar, kita harus melakukan pengecekan seperti kotak warna biru, setelah itu kita bisa tentukan apakah kita perlu melakukan pengecekan lebih jauh kotak warna kuning, atau berhenti kotak warna hitam.

[![image.png](https://i.postimg.cc/ZRTmTLJL/image.png)](https://postimg.cc/2qXMGhbq)

Kotak yang perlu kita cek hanya sebelah-sebelahnya dari kotak sekarang. Tandai kotak mana saja yang sudah di cek, bisa gunakan array tambahan seperti `bool vis[N][M]`, bernilai `true` apabila sudah di cek, `false` apabila belum.

Jangan lupa untuk menghandle supaya pengecekan tidak dilakukan di luar area, cek gambar dibawah ini.

[![image.png](https://i.postimg.cc/jqnDBskd/image.png)](https://postimg.cc/NLYGHwcW)


Kompleksitas Waktu: $O(N \times M)$

Kompleksitas Memori: $O(N \times M)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int n, m;

int dr[4] = {0, 0, 1, -1};
int dc[4] = {1, -1, 0, 0};

bool inside(int x, int y) { return x >= 0 && x < n && y >= 0 && y < m; }
vector<vector<int>> grid;
vector<vector<bool>> vis;
int klik(int i, int j, int warna) {
  vis[i][j] = 1;
  int tot = 1;

  for (int k = 0; k < 4; k++) {
    int tr = i + dr[k], tc = j + dc[k];  // tr, tc  -> koordinat tujuan

    if (!inside(tr, tc)) continue;  // cek1 : kotak (tr,tc) berada di dalam grid

    if (vis[tr][tc]) continue;  // cek2 : kotak (tr,tc) belum pernah dikunjungi

    if (grid[tr][tc] != warna) continue;  // cek3 : warna kotak (tr,tc) sama dengan koordinat asal

    tot += klik(tr, tc, warna);
  }
  return tot;
}

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cin >> n >> m;
  grid = vector<vector<int>>(n, vector<int>(m));
  vis = vector<vector<bool>>(n, vector<bool>(m, 0));
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) cin >> grid[i][j];
  }
  int x, y;
  cin >> x >> y;
  int tot = klik(x, y, grid[x][y]);
  int ans = tot * (tot - 1);
  cout << ans << endl;
}
```
</details>


## Komentar
    
- Flood Fill algorithm yang baru saja diimplementasikan adalah Floodfill rekursif atau `DFS (Depth-First-Search)`, adapun Floodfill yang menggunakan queue dengan `BFS(Breadth-First-Search)` yang akan dibahas lebih lanjut pada Pemrograman Kompetitif Dasar bab Graph.


## Materi Yang Berhubungan
    
- [Flood Fill Algorithm GFG](https://www.geeksforgeeks.org/flood-fill-algorithm/) -> Note : terdapat BFS
- [Flood Fill USACO](https://usaco.guide/silver/flood-fill?lang=cpp)


## Soal Yang Berhubungan
    
- [Flood Fill](https://leetcode.com/problems/flood-fill/)
- [Jawbreaker II: Cari Terbesar](https://tlx.toki.id/courses/competitive/chapters/04/problems/E)

