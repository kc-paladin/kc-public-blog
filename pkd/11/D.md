# [D. Muka Bebek](https://tlx.toki.id/courses/competitive/chapters/11/problems/D)

Author: Joceline Araki

Di soal ini, kita diberikan sebuah _complete graph_ dan diminta untuk menghitung biaya minimum agar semua nodes bisa terhubung. Seperti soal-soal lain di bab ini, solusi untuk problem ini cukup straightforward. Kita hanya perlu mencari _Minimum Spanning Tree_ (MST) dari graphnya.

Penjelasan MST:  
Ada $2$ algoritma yang biasanya digunakan untuk mencari MST suatu graph, yairu *Prim* dan *Kruskal*.  

## Kruskal  
Kita akan memanfaatkan konsep greedy untuk mengimplementasikan algo Kruskal.   
1. Sort semua edges dari yang weight/costnya terkecil (non-decrasing)
2. Proses edges satu persatu. Misalkan ada suatu edge $E$ menghubungkan node $u$ ke $v$ dengan cost sebesar $w$. Jika sejauh ini node $u$ dan $v$ belum terhubung, maka kita bisa menambahkan node $E$ kedalam MST, dan $cost_{graph} $ += $w$. Sebaliknya, jika node $u$ dan $v$ sudah terhubung, maka kita tidak perlu untuk mencambahkan $E$ di MSTnya karena hasilnya tidak akan optimal (costnya bertambah tapi _connectivity_-nya tidak berubah).  
3. Ulangi proses kedua sampai semua nodes sudah terhubung (akan ada $(V - 1)$ edges)

Untuk mengecek apakah node $u$ dan $v$ udah terhubung, kita bisa memanfaatkan [*Disjoint Set Union* (DSU)](https://cp-algorithms.com/data_structures/disjoint_set_union.html).  

Time Complexity : $O(E \log{V})$  
Dimana $E$ = jumlah edges dan $V$  = jumlah node.

## Prim
Sebenarnya, algo Prim juga memanfaatkan konsep greedy. Bedanya, algo Kruskal memulai prosesnya dari suatu edge sedangkan Prim memulai prosesnya dari suatu node.  
1. Pilih suatu node $A$ random di graph.
2. Cari semua nodes $B$ yang terhubung dengan node $A$ yang belum terhubung atau belum ada di set. Masukkan node $B$ yang memiliki jarak/cost paling kecil diantara semua ke dalam set (masukkan edge yang menghubungkan $A$ dan $B$ ke dalam MST).
3. Ulangi step $2$ terus menerus sampai semua node sudah masuk ke dalam set.

Time Complexity: Tergantung edgesnya direpresentasi menggunakan apa
- Adjacency Matrix: $O(V^2)$
- Adjacency List & Binary Heap (priority queue): $O(E \log{V})$
- Adjacency list and Fibonacci heap: $O(E + V \log{V})$  
Dimana $E$ = jumlah edges dan $V$  = jumlah node.

_Biasanya_, algo Prim lebih efisien di _dense grahp_ (edgesnya sangat banyak) dan algo Kruskal lebih efisien di _sparse graph_ (nodesnya terpisah-pisah dan tidak terlalu padat).

Solution code dibawah mengimplementasikan algo Kruskal.

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

const int N = 102;
vector<tuple<int, int, int>>E;
int p[N];

int par(int x){
    return ((p[x] == x) ? (x) : (p[x] = par(p[x])));
}

void join(int a, int b){
    a = par(a);
    b = par(b);

    p[b] = a;
}

bool sameSet(int a, int b){
    return (par(a) == par(b));
}

void init(){
    for(int i = 0; i < N; i++) p[i] = i;
}

int main(){
    ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
    init();

    int n; cin >> n;
    for(int i = 1; i <= n; i++){
        for(int j = 1; j <= n; j++){
            int w; cin >> w;
            if(i == j) continue;
            E.emplace_back(w, i, j);
        }
    }

    int cost = 0;
    sort(E.begin(), E.end());

    for(int i = 0; i < E.size(); i++){
        auto &[w, u, v] = E[i];
        if(sameSet(u, v)) continue; //sudah terhubung
        join(u, v);                 //belum terhubung -> hubungkan
        cost += w;
    }

    cout << cost << '\n';

    return 0;
}
```
</details>

## Materi Yang Berhubungan
- [CP Algo - Disjoint Set Union](https://cp-algorithms.com/data_structures/disjoint_set_union.html)
- [Kruskal's Algorithm](https://www.javatpoint.com/kruskal-algorithm)
- [Prim's Algorithm](https://www.javatpoint.com/prim-algorithm)
- [GeeksForGeeks - Perbeedan Algo Prim dan Kruskal](https://www.geeksforgeeks.org/difference-between-prims-and-kruskals-algorithm-for-mst/)

## Soal Yang Berhubungan

- [CSES - Building Road](https://cses.fi/problemset/task/1666)