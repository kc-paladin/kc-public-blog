# [D. Jalan Tol Menuju Roma](https://tlx.toki.id/courses/competitive/chapters/09/problems/D)

Author: Muhammad Hasan

Kita definisikan beberapa hal sebagai berikut:

- $S=$ nomor kota awal
- $E=$ nomor kota akhir.
- $dist_S(X)=$ jarak kota $S$ ke kota $X$, apabila tidak bisa mencapai maka $dist_S(X) = \infty$
- $dist_E(X)=$ jarak kota $E$ ke kota $X$, apabila tidak bisa mencapai maka $dist_E(X) = \infty$

Untuk menyelesaikan soal ini, dapat dilakukan algoritma sebagai berikut:

- Pada awalnya set $\text{ans} = dist_S[E] \rightarrow$ Alur yang digunakan adalah langsung saja $S \rightarrow E$  
- Untuk setiap pair $(U, V)$ yang merupakan sebuah ruas jalan tol maka kita bisa coba gunakan jalan tol ini:
  - $\text{ans} = \min(\text{ans}, dist_S[U] + 1 + dist_E[V]) \rightarrow$ Alur yang digunakan adalah $S \rightarrow U \rightarrow V \rightarrow E$
  - $\text{ans} = \min(\text{ans}, dist_S[V] + 1 + dist_E[U]) \rightarrow$ Alur yang digunakan adalah $S \rightarrow V \rightarrow U \rightarrow E$

Kita akan dapatkan $\text{ans}$ yang dibutuhkan dengan cara tersebut, 
kemudian untuk mendapatkan $dist_S$ maupun $dist_E$ bisa kita gunakan BFS.

Kompleksitas Waktu: $O(N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

const int INF = 1e9;

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  int n, l, t, s, e;
  cin >> n >> l >> t >> s >> e;
  vector<vector<int>> adj(n + 1);
  for (int i = 1; i <= l; i++) {
    int u, v;
    cin >> u >> v;
    adj[u].emplace_back(v);
    adj[v].emplace_back(u);
  }
  vector<pair<int, int>> p(t);
  for (int i = 0; i < t; i++) {
    cin >> p[i].first >> p[i].second;
  }

  auto getDist = [&](int x) -> vector<int> {
    vector<int> dist(n + 1, INF);
    dist[x] = 0;
    queue<int> q;
    q.emplace(x);
    while (!q.empty()) {
      int u = q.front();
      q.pop();
      for (int v : adj[u]) {
        if (dist[v] == INF) {
          dist[v] = 1 + dist[u];
          q.emplace(v);
        }
      }
    }
    return dist;
  };

  vector<int> distS = getDist(s);
  vector<int> distE = getDist(e);
  int ans = distS[e];
  for (auto [u, v] : p) {
    int cur = min(distS[u] + 1 + distE[v], distS[v] + 1 + distE[u]);
    ans = min(ans, cur);
  }
  cout << ans << '\n';

  return 0;
}
```
</details>

## Komentar
- Apabila pada *edge* tersebut ada *weight* kita bisa gunakan cara yang sama dengan catatan $dist_S$ dan $dist_E$ dibuat dengan menggunakan Dijsktra

## Materi Yang Berhubungan
- [BFS for A Graph](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)
- [Dijsktra](https://cp-algorithms.com/graph/dijkstra.html)