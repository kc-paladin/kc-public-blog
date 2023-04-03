# [A. Maze](https://tlx.toki.id/courses/competitive/chapters/09/problems/A)

Author: Daniel Simanullang 

Prerequisite(s) : BFS

<!-- Masukkan penjelasan disini -->
Soal ini hanya soal klasik (BFS pada grid). Pada soal ini, kita hanya perlu untuk menggunakan algoritma BFS untuk mencari jalan keluar terpendek. Kita akan menggunakan array $dist$ untuk menyimpan jarak terpendek dari setiap titik ke titik awal.Array $dx$ dan $dy$ disini digunakan untuk arah gerak sumbu $x$ dan sumbu $y$. Untuk mencari jarak terpendek, kita hanya perlu membuat $dist[t.first + dx[i]][t.second + dy[i]] = dist[t.first][t.second] + 1$. Maksud dari persamaan ini ialah ketika kita ingin mencapai suatu titik, maka jalan terbaik hanya di dapat melalui titik sebelumnya yang berjarak $1$ dari titik tersebut. 

Kompleksitas Waktu: $O(N+M)$

Kompleksitas Memori: $O(N+M)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace __gnu_pbds;
using namespace std;

// defines
#define int long long
#define debug(x) cerr << "(" << #x << "=" << x << "," << __LINE__ << ")\n";
#define sz(x) ((int)x.size());
#define all(x) (x).begin(), (x).end();

// constants
const int dx[4]{1, 0, -1, 0}, dy[4]{0, 1, 0, -1};
const char dir[4]{'D', 'R', 'U', 'L'};
const int mod = 1e9 + 7;
const int maxn = 2e5 + 5;
const double eps = 1e-9;

// typedefs
typedef vector<vector<int> > vii;
typedef vector<int> vi;
typedef pair<int, int> pii;

// Template
template <class T>
using oset =
    tree<T, null_type, less<T>, rb_tree_tag, tree_order_statistics_node_update>;

// Mods
int mul(int a, int b, int MOD) { return ((a % MOD) * (b % MOD)) % MOD; }
int add(int a, int b, int MOD) { return (a + b) % MOD; }
int sub(int a, int b, int MOD) { return (MOD + a - b) % MOD; }

signed main() {
  ios_base::sync_with_stdio(false);
  cin.tie(NULL);
  int n, m;
  cin >> n >> m;
  vector<vector<int> > grid(n, vector<int>(m));
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      cin >> grid[i][j];
    }
  }
  int a, b;
  cin >> a >> b;
  a--, b--;
  vector<vector<int> > dist(n, vector<int>(m, INT_MAX));
  queue<pair<int, int> > q;
  vector<vector<bool> > vis(n, vector<bool>(m, 0));
  q.push({a, b});
  dist[a][b] = 1;
  vis[a][b] = 1;
  while (not q.empty()) {
    auto t = q.front();
    q.pop();
    for (int i = 0; i < 4; i++) {
      if (t.first + dx[i] >= 0 and t.first + dx[i] < n and
          t.second + dy[i] >= 0 and t.second + dy[i] < m and
          not vis[t.first + dx[i]][t.second + dy[i]] and
          grid[t.first + dx[i]][t.second + dy[i]] != -1) {
        q.push({t.first + dx[i], t.second + dy[i]});
        dist[t.first + dx[i]][t.second + dy[i]] = dist[t.first][t.second] + 1;
        vis[t.first + dx[i]][t.second + dy[i]] = 1;
      }
    }
  }
  int ans = INT_MAX;
  for (int i = 0; i < n; i++) {
    ans = min({ans, dist[i][0], dist[i][m - 1]});
  }
  for (int i = 0; i < m; i++) {
    ans = min({ans, dist[0][i], dist[n - 1][i]});
  }
  cout << ans << '\n';

  return 0;
}
```
</details>

<!-- Tambahkan komentar apabila perlu

## Komentar
    
- Komentar I
- Komentar II

-->


## Materi Yang Berhubungan
    
- [Link Materi BFS](https://usaco.guide/silver/graph-traversal?lang=cpp)




## Soal Yang Berhubungan
    
- [CSES Labyrinth](https://cses.fi/problemset/task/1193/)
