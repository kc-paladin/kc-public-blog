# [F. Jawbreaker III: Cari Terbesar dan Runtuhkan!](https://tlx.toki.id/courses/competitive/chapters/04/problems/E)

Author: Yose Yehezkiel Maranata

Halo semua! :D

Pastikan dahulu kalian sudah `AC` soal [Jawbreaker II: Cari Terbesar](https://tlx.toki.id/courses/competitive/chapters/04/problems/E) dan [Runtuh](https://tlx.toki.id/courses/competitive/chapters/01/problems/B) dulu ya. Sesuai judul soal, setelah menemukan yang terbesar kita akan runtuhkan! 

Lakukan hal yang sama dengan Cari terbesar yaitu bruteforce dahulu setiap kemungkinan floodfill.

Setelah itu hilangkan floodfill yang paling besar. Di contoh kode di bawah nilai dari `grid[x][y]` akan dirubah menjadi 0 artinya di petak tersebut sudah kosong petaknya.

Lalu Runtuhkan petak-petak yang kosong kita isi dengan petak-petak atasnya yang masih berisi. 

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

    if (!inside(tr, tc)) continue;  // cek1 : (tr,tc) berada di dalam grid

    if (vis[tr][tc]) continue;  // cek2 : (tr,tc) belum pernah dikunjungi

    if (grid[tr][tc] != warna)
      continue;  // cek3 : warna (tr,tc) sama dengan koordinat asal

    tot += klik(tr, tc, warna);
  }
  return tot;
}

void hilangkan(int i, int j, int warna) {
  vis[i][j] = 1;
  grid[i][j] = 0;
  for (int k = 0; k < 4; k++) {
    int tr = i + dr[k], tc = j + dc[k];  // tr, tc  -> koordinat tujuan

    if (!inside(tr, tc)) continue;  // cek1 : (tr,tc) berada di dalam grid

    if (vis[tr][tc]) continue;  // cek2 : (tr,tc) belum pernah dikunjungi

    if (grid[tr][tc] != warna)
      continue;  // cek3 : warna (tr,tc) sama dengan koordinat asal

    hilangkan(tr, tc, warna);
  }
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
  int mx = 0, x_mx, y_mx;
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      if (vis[i][j]) continue;
      int tot = klik(i, j, grid[i][j]);
      if (mx < tot) {
        x_mx = i, y_mx = j;
        mx = tot;
      }
    }
  }
  // hilangkan
  vis = vector<vector<bool>>(n, vector<bool>(m, 0));
  hilangkan(x_mx, y_mx, grid[x_mx][y_mx]);

  // runtuhkan
  for (int j = 0; j < m; j++) {
    int bottom = -1;
    for (int i = n - 1; i >= 0; i--) {
      if (grid[i][j] == 0 && bottom == -1)
        bottom = i;
      else if (grid[i][j] != 0 && bottom != -1) {
        grid[bottom][j] = grid[i][j];
        grid[i][j] = 0;
        bottom--;
      }
    }
  }

  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      if(grid[i][j]) cout << grid[i][j] << " ";
      else cout << ". "; 
    }
    cout << endl;
  }
}
```
</details>


## Soal Yang Berhubungan
    
- [Jawbreaker II: Cari Terbesar](https://tlx.toki.id/courses/competitive/chapters/04/problems/E)
- [Runtuh](https://tlx.toki.id/courses/competitive/chapters/01/problems/B)
- [Jawbreaker IV: Cari Terbesar 2 Langkah](https://tlx.toki.id/courses/competitive/chapters/04/problems/G)


