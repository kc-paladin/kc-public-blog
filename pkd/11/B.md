# [B. Taman Bunga Beraroma](https://tlx.toki.id/courses/competitive/chapters/11/problems/B)

Author: Joceline Araki

Di soal ini, kita diberikan sebuah graph berisi $V$ nodes dan $E$ edges. Pak Dengklek ingin berjalan dari node $0$ ke $(V - 1)$ dengan menggunakan energi seminimal mungkin. Banyak energi yang dibutuhkan untuk melewati edge ke-$i$ adalah $C_i$. Jika $C_i$ bernilai negatif, maka Pak Dengklek mendapatkan tambahan energi sebesar $|C_i|$. Karena graphnya bisa saja memiliki cycle, maka jika graph tersebut memiliki _negative cycle_, Pak Dengklek akan terus menerus berputar di cycle itu karena mau menambah energi dan kita ingin menggunakan energi seminimal mungkin. 

Output dari soal ini ada $3$ jenis, yaitu:
- `"Pak Dengklek tidak mau pulang"` jika di dalam graph tersebut terdapat negative cycle.
- `"Tidak ada jalan"` jika node $0$ dan $(V - 1)$ tidak terhubung
- Banyak energi minimum yang diperlukan pak dengklek, atau ($-1$ * banyaknya energi berlebih).

Nah, bagaimana cara mengecek ada/tidaknya negative cycle? Gunakan algoritma Bellman-Ford!

Penjelasan algoritma Bellman-Ford:  
1. Misalkan ada variabel `dist[x]` yang menyimpan jarak terpendek dari node start ke x. Awalnya, set semua nilai $dist[0..V-1] = \infty$ dan $dist[s] = 0$.
2. Untuk setiap edge yang menghubungkan node $u$ ke $v$, jika $dist[v] > dist[u] + w$, maka update nilai $dist[v]$ dengan nilai $dist[u] + w$ dimana $w$ adalah cost dari node $u \rightarrow v$. Ulangi proses ini sebanyak $(V - 1)$ kali.
3. Sekarang, semua $dist[x]$ sudah menyimpan shortest path dari node start. Untuk mengecek ada/tidaknya negative cycle, kita bisa mengulangi proses looping tiap edge seperti di nomor $2$ lagi, tapi cukup jalankan $1$ kali saja. Jika masih ada nilai $dist[x]$ yang bisa diupdate, berarti graph tersebut memiliki negative cycle.

Kenapa kita cuma memerlukan $(V - 1)$ operasi? Misalkan node startnya adalah $A$.
- Pada operasi pertama, semua $dist[x]$ akan terupdate dimana $x$ bisa dicapai dari $A$ dengan menggunakan tepat $1$ edge.
- Pada operasi kedua, semua $dist[x]$ akan terupdate dimana $x$ bisa dicapai dari $A$ dengan menggunakan tepat $2$ edge.  
...
- Pada operasi $(V - 1)$, semua $dist[x]$ akan terupdate dimana $x$ bisa dicapai dari $A$ dengan menggunakan tepat $(V - 1)$ edge.  

Maka sebenarnya jumlah edges yang harus dilewati untuk mendapatkan shortest pathnya tidak akan lebih dari $(V - 1)$ edges. Jika kita menemukan jalan yang lebih pendek dimana edges yang dilewati lebih banyak dari $(V - 1)$, maka bisa dipastikan path tersebut pasti melewati suatu negative cycle.

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

struct Edge{
    int u, v, w;

    Edge(int _u, int _v, int _w){
        u = _u;
        v = _v;
        w = _w;
    }
};

void solve(){
    int v, e; cin >> v >> e;
    vector<Edge>a;
    vector<int>adj[v];
    vector<bool>vis(v, 0);

    for(int i = 0; i < e; i++){
        int u, v, w; cin >> u >> v >> w;
        a.push_back(Edge(u, v, w));
        adj[u].push_back(v);
    }

    queue<int>q; 
    q.push(0);
    vis[0] = true;

    while(!q.empty()){
        int now = q.front(); q.pop();

        for(auto &e: adj[now]){
            if(!vis[e]){
                vis[e] = true;
                q.push(e);
            }
        }
    }
    
    vector<int>dis(v, 1e9);
    dis[0] = 0;

    for(int i = 1; i <= v - 1; i++){
        for(auto &e: a){
            dis[e.v] = min(dis[e.v], dis[e.u] + e.w);
        }
    }

    for(auto &e: a){
        if((dis[e.v] > dis[e.u] + e.w) && vis[e.v]){
            cout << "Pak Dengklek tidak mau pulang" << endl;
            return;
        }
    }

    if(!vis[v - 1]){
        cout << "Tidak ada jalan" << endl;
        return;
    }

    cout << dis[v - 1] << endl;

    return;
}

int main(){
    int tc; cin >> tc;

    while(tc--){
        solve();
    }

    return 0;
}
```
</details>

## Materi Yang Berhubungan

- [CP Algo - Bellman Ford](https://cp-algorithms.com/graph/bellman_ford.html)

## Soal Yang Berhubungan
- [CSES - High Score](https://cses.fi/problemset/task/1673)
- [CSES - Cycle Finding](https://cses.fi/problemset/task/1197)


