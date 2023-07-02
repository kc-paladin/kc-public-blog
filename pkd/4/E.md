# [E. Jawbreaker II: Cari Terbesar](https://tlx.toki.id/courses/competitive/chapters/04/problems/E)

Author: Yose Yehezkiel Maranata


Halo semua! :D

Kita akan membuat AI(*Artificial-Inteligence*) simpel untuk game Jawbreaker! AI yang akan kita buat ini bertujuan untuk mencari solusi optimal di suatu saat permainan. Terdengar menarik bukan? 

Mungkin soal ini terdengar susah, tapi ternyata enggak kok! Pastikan dulu kalian udah `AC` soal [Jawbreaker I: Klik!](https://tlx.toki.id/courses/basic/chapters/13/) dulu ya. 

Karena bab ini bahas tentang bruteforce, jadi kita hanya perlu **membruteforce setiap kemungkinan floodfill** yang ada saja! Simpel kan? 

Tandai kotak mana saja yang sudah di cek, bisa gunakan array tambahan seperti `bool vis[N][M]`, bernilai `true` apabila sudah di cek, `false` apabila belum.

Kompleksitas Waktu: $O(N \times M )$

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

    if (!inside(tr, tc)) continue;  // cek1 : (tr,tc) berada di dalam grid

    if (vis[tr][tc]) continue;  // cek2 : (tr,tc) belum pernah dikunjungi

    if (grid[tr][tc] != warna)
      continue;  // cek3 : warna (tr,tc) sama dengan koordinat asal

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
  // tambahkan bruteforce untuk mengecek setiap floodfill yang dilakukan
  int mx = 0;
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      if (vis[i][j]) continue;
      int tot = klik(i, j, grid[i][j]);
      mx = max(mx, tot);
    }
  }
  int ans = mx * (mx - 1);
  cout << ans << endl;
}
```
</details>



## Materi Yang Berhubungan
    
- [Flood Fill USACO](https://usaco.guide/silver/flood-fill?lang=cpp)




## Soal Yang Berhubungan
    
- [Jawbreaker I: Klik!](https://tlx.toki.id/courses/basic/chapters/13/problems/G)
- [Jawbreaker III: Cari terbesar dan runtuhkan](https://tlx.toki.id/courses/competitive/chapters/04/problems/F)
- [Counting Rooms](https://cses.fi/problemset/task/1192)
- [Icy Perimeter](http://www.usaco.org/index.php?page=viewproblem2&cpid=895)


