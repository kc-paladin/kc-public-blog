# [G. Jawbreaker IV: Cari Terbesar 2 Langkah](https://tlx.toki.id/courses/competitive/chapters/04/problems/G)

Author: Yose Yehezkiel Maranata

Halo semua! :D

Di blog ini kita akan membuat AI yang lebih canggih lagi untuk permainan JawBreaker! **OMG!**

Pastikan dahulu kalian sudah `AC` soal [Jawbreaker III: Cari Terbesar dan Runtuhkan!](https://tlx.toki.id/courses/competitive/chapters/04/problems/F) dulu ya. Apakah kita hanya perlu menambahkan 1 kali floodfill lagi? Iya, tapi tidak bisa langsung. Untuk mengetahui lebih lanjut alasannya, bisa baca soalnya dengan lebih baik. 

Kita harus bruteforce klik pertama yang dilanjut dengan membruteforce klik kedua. Setelah klik yang pertama, kondisi grid kita harus berubah untuk membruteforce klik kedua. Simpanlah hasil kondisi grid yang sudah berubah pada array 2d lain agar kita masih memiliki kondisi grid pada mulanya. 

Perhatikan juga bahwa kita hanya bisa memilih apabila bola lebih dari 1. 

Kompleksitas Waktu: $O((N \times M)^2)$

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
vector<vector<int>> temp;
vector<vector<bool>> vis;
vector<vector<bool>> vis2;
int klik1(int i, int j, int warna) {
  vis[i][j] = 1;
  temp[i][j] = 0;
  int tot = 1;

  for (int k = 0; k < 4; k++) {
    int tr = i + dr[k], tc = j + dc[k];  // tr, tc  -> koordinat tujuan

    if (!inside(tr, tc)) continue;  // cek1 : (tr,tc) berada di dalam grid

    if (vis[tr][tc]) continue;  // cek2 : (tr,tc) belum pernah dikunjungi

    if (temp[tr][tc] != warna)
      continue;  // cek3 : warna (tr,tc) sama dengan koordinat asal

    tot += klik1(tr, tc, warna);
  }
  return tot;
}

int klik2(int i, int j, int warna) {
  vis2[i][j] = 1;
  int tot = 1;

  for (int k = 0; k < 4; k++) {
    int tr = i + dr[k], tc = j + dc[k];  // tr, tc  -> koordinat tujuan

    if (!inside(tr, tc)) continue;  // cek1 : (tr,tc) berada di dalam grid

    if (vis2[tr][tc]) continue;  // cek2 : (tr,tc) belum pernah dikunjungi

    if (temp[tr][tc] != warna)
      continue;  // cek3 : warna (tr,tc) sama dengan koordinat asal

    tot += klik2(tr, tc, warna);
  }
  return tot;
}

int coba(int x, int y) {
  vis2 = vector<vector<bool>>(n, vector<bool>(m, 0));
  temp = grid;
  int tot1 = klik1(x, y, grid[x][y]);

  if (tot1 <= 1) return 0;

  // runtuhkan
  for (int j = 0; j < m; j++) {
    int bottom = -1;
    for (int i = n - 1; i >= 0; i--) {
      if (temp[i][j] == 0 && bottom == -1)
        bottom = i;
      else if (temp[i][j] != 0 && bottom != -1) {
        temp[bottom][j] = temp[i][j];
        temp[i][j] = 0;
        bottom--;
      }
    }
  }
  int mx = 0;
  // bruteforce setiap kemungkinan kedua
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      if (vis2[i][j]) continue;
      if (temp[i][j] == 0) continue;
      int tot2 = klik2(i, j, temp[i][j]);
      mx = max(mx, tot2);
    }
  }
  return (tot1 * (tot1 - 1)) + (mx * (mx - 1));
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
  // bruteforce setiap kemungkinan pertama
  int mx = 0;
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      if (vis[i][j]) continue;
      mx = max(mx, coba(i, j));
    }
  }
  cout << mx << endl;
}
```
</details>

## Komentar
- kompleksitas yang lebih tepat adalah $O((N \times M) \times (\text{total kemungkinan klik pertama} \times \text{total kemungkinan klik kedua}))$ namun *worst-case*nya bisa mencapai $O((N \times M)^2)$

## Soal Yang Berhubungan
- [Jawbreaker V: Cari Optimal](https://tlx.toki.id/courses/competitive/chapters/13/problems/G)


