# [B. Disconnected Graph](https://tlx.toki.id/courses/competitive/chapters/09/problems/B)

Author: Joceline Araki

Prerequisite: Tau DFS/BFS

Di problem ini, ada graph dengan $N$ nodes dan $E$ edges. Di antara $N$ nodes tersebut, ada $Q$ node khusus. Nah, kita juga diminta untuk menghilangkan $R$ edges dari $E$ edges yang tersedia. 

Pertama-tama, kita proses dulu cara menghilangkan $R$ edges yang diminta. Caranya, $E$ edges yang diberikan di input jangan langsung dimasukkan ke dalam adjacency list, tapi kita simpan dulu di dalam sebuah vector atau array of pairs `pair<int, int>edge[]`. Lalu, untuk semua $R$ edges yang mau dihilangkan, kita bisa mengganti nilai **edge[i]** dari $(u, v)$ menjadi $(-1, -1)$. Nah, setelah mengganti nilai $R$ edges tersebut kita bisa bikin adjacency listnya seperti biasa, tapi jangan lupa untuk skip edges yang nilainya $(-1, -1)$.

Untuk menghitung berapa banyak pasangan node khusus yang terhubung, kita bisa melakukan **DFS/BFS** untuk setiap **CC** _(connected component)_, dan hitung berapa banyak node khusus yang ada di dalam CC tersebut. Bisa dilihat bahwa semua node khusus yang berada di dalam $1$ CC terhubung. Kita definisikan `connected` sebagai jumlah node khusus di dalam $1$ CC, dan `disconnected` sebagai jumlah node khusus yang tidak berada di dalam CC  tersebut. Maka bisa diketahui bahwa $disconnected = Q - connected$. Untuk mencari tahu berapa banyak pasangan yang tidak terhubung, maka kita bisa langsung menghitung jumlah $(connected \times disconnected)$ di setiap CC. Jangan lupa untuk membagi $2$ hasil akhirnya untuk mengatasi _double counting_. 

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;
using ll = long long;

const int MAXN = 50002;
vector<int> adj[MAXN];
bool vis[MAXN], khusus[MAXN];

void init(int n) {
  for (int i = 1; i <= n; i++) {
    adj[i].clear();
    vis[i] = khusus[i] = false;
  }
}

ll dfs(int cur) {
  ll ret = khusus[cur];
  vis[cur] = true;

  for (auto &nxt : adj[cur]) {
    if (vis[nxt]) continue;
    ret += dfs(nxt);
  }

  return ret;
}

void solve() {
  int N, E, Q, R;
  cin >> N >> E >> Q >> R;
  init(N);

  vector<pair<int, int>> edge(E + 1);
  for (int i = 1; i <= E; i++) cin >> edge[i].first >> edge[i].second;
  for (int i = 1; i <= Q; i++) {
    int x;
    cin >> x;
    khusus[x] = true;
  }

  for (int i = 1; i <= R; i++) {
    int x;
    cin >> x;
    edge[x] = {-1, -1};
  }

  for (int i = 1; i <= E; i++) {
    if (edge[i].first == -1) continue;
    adj[edge[i].first].push_back(edge[i].second);
    adj[edge[i].second].push_back(edge[i].first);
  }

  ll ans = 0;
  for (int i = 1; i <= N; i++) {
    if (!vis[i]) {
      ll connected = dfs(i);
      ll disconnected = Q - connected;
      ans += connected * disconnected;
    }
  }

  ans /= 2LL;
  cout << ans << '\n';
}

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);
  int tc;
  cin >> tc;
  while (tc--) {
    solve();
  }

  return 0;
}
```
</details>

## Materi Yang Berhubungan
- [GeeksForGeeks - BFS For A Graph](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)
- [CP Algorithms - Search for Connected Components in a Graph](https://cp-algorithms.com/graph/search-for-connected-components.html)