# [C. Perjalanan Teringan](https://tlx.toki.id/courses/competitive/chapters/13/problems/C)

Author : Benedict Presley

Kita dapat mengubah ladang menjadi graf berbentuk *grid*. Permasalahan ini mirip sekali dengan mencari shortest path pada graf. Perbedaannya adalah, saat melakukan perpinahan, kita bukan menjumlahkan bobot kedua petak tetapi mengambil maksimum dari bobot kedua petak.

Misal kita sedang berada di petak $(r_1, c_1)$ dan kita akan berpindah ke petak di sampingnya, yaitu $(r_2, c_2)$. Misal $u$ dan $v$ masing-masing adalah beban pada petak $(r_1, c_1)$ dan $(r_2, c_2)$. Jika $u < v$, maka kita perlu membawa beban tambahan sebesar $v - u$. Selain itu, kita tidak perlu membawa beban tambahan, atau membawa tamabahan sebesar $0$. Bisa dilihat bahwa graf di atas tidak memiliki *negative cycle* sehingga kita tetap dapat melakukan algoritma Dijkstra.

Catatan : Kita tidak perlu membuat edge pada graf tersebut secara eksplisit. Penjelasan di atas hanya untuk menunjukkan bahwa kita masih dapat menjalan algoritma Dijkstra.

Kompleksitas Waktu: $O(NM\log(NM))$

Kompleksitas Memori: $O(NM)$


<details>
  <summary>Solution Code</summary>

```
    #include<bits/stdc++.h>
    using namespace std;

    // Untuk mempermudah perpindahan dari petak ke petak sebelahnya
    int dx[4] = {1, -1, 0,  0};
    int dy[4] = {0,  0, 1, -1};

    int mp[1001][1001], dist[1001][1001];
    bool vis[1001][1001];

    int main(){
        ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);

        int R, C; cin >> R >> C;

        for(int i = 1; i <= R; ++i){
            for(int j = 1; j <= C; ++j){
                cin >> mp[i][j];
                dist[i][j] = 1e9; //awalnya dist[i][j] bernilai tak terhingga
            }
        }

        pair<int, int> st, ed;

        cin >> st.first >> st.second;
        cin >> ed.first >> ed.second;

        priority_queue<pair<int, pair<int, int>>> pq;

        pq.push({0, st}); // Ingat, beban pada titik awal tidak masuk perhitungan
        dist[st.first][st.second] = 0;

        while(!pq.empty()){
            int D = -pq.top().first; // jarak sejauh ini
            pair<int, int> cur = pq.top().second; // posisi saat ini
            pq.pop();

            if(vis[cur.first][cur.second]){
                continue;
            }
            vis[cur.first][cur.second] = 1;

            for(int k = 0; k < 4; ++k){
                int nx = cur.first + dx[k], ny = cur.second + dy[k];
                if(mp[nx][ny] == -1){ // petak tidak dapat dilewati
                    continue;
                }
                if(dist[nx][ny] > max(D, mp[nx][ny])){
                    dist[nx][ny] = max(D, mp[nx][ny]);
                    pq.push({-dist[nx][ny], {nx, ny}});
                }
            }
        }

        cout << dist[ed.first][ed.second];

        return 0;
    }    
```

</details>