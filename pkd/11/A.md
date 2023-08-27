# [A. Les Piano](https://tlx.toki.id/courses/competitive/chapters/11/problems/A)

Author: Joceline Araki

Di soal ini, kita diberikan suatu _weighted graph_ dengan $V$ nodes dan $E$ edges. Kita diminta untuk mencari _shortest path_ dari node $a$ ke node $b$.

Sebenarnya, solusi problem ini cukup straightforward. Kita akan menggunakan algo untuk menyelesaikan problem shortest path, yaitu _Dijkstra_.

Penjelasan algoritma Dijkstra:  
1. Buat array `dist[]` untuk menampung jarak dari node $a$ ke node-node yang lain. Awalnya, $dist[1..N] = \infty$ dan $dist[a] = 0$ (karena jarak dari $a$ ke $a = 0$ ).
2. Kalau di BFS kita menggunakan queue biasa, di Dijkstra kita menggunakan priority queue dengan non-decreasing order supaya kita bisa memproses node dengan jarak terdekat terlebih dahulu. Definisikan `pii` sebagai `pair<int, int>`. Kita akan membuat `priority_queue<pii, vector<pii>, greater<pii>>pq`. Isi dari pq tersebut adalah `{jarak node a ke x, x}`
3. Bagian ini mirip dengan algo BFS, yaitu kita coba proses satu persatu node yang terhubung dengan node yang terletak di _pq.top()_. Bedanya, di algo BFS kita menggunakan array **vis[N]** untuk menandai nodes yang sudah divisit. Di Dijkstra, kita harus mengecek apakah $(dist[nxt] > dist[cur] + w)$ dimana $w$ adalah panjang/cost dari node $cur$ ke node $nxt$. Jika syarat tersebut terpenuhi, maka kita akan meng-_update_ nilai $dist[nxt]$ menjadi $(dist[cur] + w)$, dan masukkan $\{dist[cur] + w, nxt\}$ ke dalam priority queue tadi.
4. Setelah pq nya sudah kosong, maka kita sudah mendapatkan shortest path dari node $a$ ke semua node $[1..N]$. 

Untuk solusi problem ini, kita cukup jalankan Dijkstra dari node $a$, dan output nilai $dist[b]$ (shortest path dari $a$ ke $b$).

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
#define pii pair<int, int>

using namespace std;

const int N = 2502;
vector<pair<int, int>> adj[N];
vector<int> dist(N, 1e9);

int dijkstra(int a, int b) {
  dist[a] = 0;
  priority_queue<pii, vector<pii>, greater<pii>> pq;
  pq.emplace(0, a);

  while (!pq.empty()) {
    auto[curW, u] = pq.top();
    pq.pop();
    for (auto & [ v, w ] : adj[u]) {
      if (dist[v] > curW + w) {
        dist[v] = curW + w;
        pq.emplace(dist[v], v);
      }
    }
  }

  return dist[b];
}

int main() {
  int n, e, a, b;
  cin >> n >> e >> a >> b;
  while (e--) {
    int u, v, w;
    cin >> u >> v >> w;
    adj[u].emplace_back(v, w);
    adj[v].emplace_back(u, w);
  }

  cout << dijkstra(a, b) << '\n';

  return 0;
}
```
</details>

## Materi Yang Berhubungan

- [GeeksForGeeks - Dijkstra using Priority Queue](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-priority_queue-stl/)

- [CP Algo - Dijkstra Algorithm](https://cp-algorithms.com/graph/dijkstra.html)

- [GeeksForGeeks - Priority Queue Min Heap and Max Heap](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)

## Soal Yang Berhubungan

- [CSES - Shortest Routes I](https://cses.fi/problemset/task/1671)
