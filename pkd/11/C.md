# [C. Mengantar Pesanan](https://tlx.toki.id/courses/competitive/chapters/11/problems/C)

Author: Muhammad Hasan

Pada soal ini kita diberikan *weighted graph* dan diberikan $Q$ kota $P_1, P_2, \dots, P_Q$, kita perlu telurusi $Q$ kota tersebut dengan waktu minimal.

Didefinisikan $dist[U][V] =$ 
waktu minimal yang dibutuhkan untuk pergi dari $U$ ke $V$.

Maka solusi dari soal ini sebetulnya mudah saja, untuk setiap kota bersebalahan kita gunakan waktu minimal untuk mencapainya.

Lebih formalnya, jawaban dari persoalan ini adalah:

$$
\begin{align}
\text{Jumlah waktu minimal} &= \sum_{i=2}^{Q} dist[P_{i-1}][P_i]  \\
&= dist[P_1][P_2] + dist[P_2][P_3] + \cdots + dist[P_{Q-1}][P_Q]
\end{align}
$$

Sehingga permasalahan lain dari soal ini adalah bagaimana cara mendapatkan $dist$ tersebut.

Ini mudah kita dapatkan dengan beberapa algoritma *shortest graph* yang ada, namun perhatikan bahwa disini $N_{\max} = 200$ 
($N_{\max}$ bisa dibilang relatif kecil) oleh karena itu kita bisa gunakan algoritma [Floyd Warshall](https://cp-algorithms.com/graph/all-pair-shortest-path-floyd-warshall.html) untuk mendapatkan $dist$.

Kompleksitas Waktu: $O(N^3)$

Kompleksitas Memori: $O(N^2)$

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

  int n, m, q;
  cin >> n >> m >> q;
  vector<vector<int>> dist(n + 1, vector<int>(n + 1, INF));
  for (int i = 0; i < m; i++) {
    int u, v, w;
    cin >> u >> v >> w;
    dist[u][v] = min(dist[u][v], w);
    dist[v][u] = min(dist[v][u], w);
  }
  for (int u = 1; u <= n; u++) {
    dist[u][u] = 0;
  }
  for (int k = 1; k <= n; k++) {
    for (int i = 1; i <= n; i++) {
      for (int j = 1; j <= n; j++) {
        dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j]);
      }
    }
  }
  long long ans = 0;
  int lastNode = -1;
  while (q--) {
    int u;
    cin >> u;
    if (lastNode != -1) {
      ans += dist[lastNode][u];
    }
    lastNode = u;
  }
  cout << ans << '\n';

  return 0;
}
```
</details>

## Komentar
- Banyak algoritma *shortest graph* lain, masing-masing dengan *pros* dan *cons*-nya, disini Floyd Warshall biasanya hanya digunakan untuk *graph* yang kecil seperti pada soal.
- Direkomendasikan untuk mempelajari [Algoritma Dijkstra](https://cp-algorithms.com/graph/dijkstra_sparse.html) karena ini yang paling sering digunakan pada persoalan.

## Materi Yang Berhubungan
- [Floyd Warshall](https://cp-algorithms.com/graph/all-pair-shortest-path-floyd-warshall.html)
- [Dijsktra](https://cp-algorithms.com/graph/dijkstra_sparse.html)
- [Bellman Ford](https://cp-algorithms.com/graph/bellman_ford.html)
