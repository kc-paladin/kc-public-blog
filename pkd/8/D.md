# [D. Barisan Intip](https://tlx.toki.id/courses/competitive/chapters/08/problems/D)

Author: Joceline Araki

Di problem ini, ada $N$ bebek yang sedang berbaris dengan urutan bebek ke-$1$ berada di paling depan dan bebek ke-$N$ berada di paling belakang. Bebek ke-$i$ bisa mengintip dirinya sendiri dan bebek yang ada di depannya $(1, 2, ...,  i-1)$ yang tingginya tidak lebih dari tinggi bebek ke-$i$. 

Mari kita coba dari solusi _naive_ nya :D. Jawaban dari problem ini bisa didapatkan dengan cara yang _straightforward_, yaitu untuk setiap bebek $i$, kita coba loop dari $(i - 1, i - 2, ..., 1)$, dan coba cari index $j$ dimana $H_i < H_j$ untuk pertama kalinya (kita mencari index bebek pertama sebelum $i$ yang lebih tinggi daripada bebek ke-$i$). Tapi, kompleksitas solusi ini adalah $O(N^2)$ :(. Dari solusi ini, apakah ada observasi yang bisa diambil?

Misalkan untuk kasus seperti ini (assume yang warna kuning itu bebek ~~dan $\pi$ = $5$~~):
[![Screenshot-2023-08-06-at-09-16-46.png](https://i.postimg.cc/GmNT3xhk/Screenshot-2023-08-06-at-09-16-46.png)](https://postimg.cc/DSrwBsGZ)

Maka pengintipan bebek-bebeknya adalah:
[![Screenshot-2023-08-06-at-09-24-40.png](https://i.postimg.cc/Y979jncm/Screenshot-2023-08-06-at-09-24-40.png)](https://postimg.cc/qtm05Gvk)
Penjelasan: Misalkan garis hitam yang ada di atas bebek ke-$3$ sampai bebek ke-$6$ menandakan bahwa bebek ke $6$ bisa mengintip bebek ke $(6, 5, 4, 3)$.

Misalkan ada 2 bebek dengan index $i$ dan $j$ dimana $i > j$, dan $H_i >= H_j$,  maka semua bebek yang bisa diintip oleh bebek $j$ juga pasti bisa diintip oleh bebek ke $i$. Oleh karena itu, sebenarnya bebek-bebek tersebut bisa dikelompokkan/digabung. Misalkan, bebek di index $6$ bisa digabungkan dengan bebek di index ke-$5$ (yang sudah tergabung dengan bebek ke $2$,$3$, dan $4$). Jadi, total bebek yang bisa diintip oleh bebek ke-$6$ adalah $1 + 3 = 4$. 

Intinya, untuk suatu $i$ dan $j$ dimana $i > j$, kita bisa menggabung kedua index tersebut selama $H_i >= H_j$. Kita berhenti mengelompokkan kedua index di index $j$ paling kanan dimana $H_i < H_j$. Caranya gimana? Kita bisa menggunakan stack! Stack kita harus menyimpan $2$ informasi, yaitu `{tinggi bebek, jumlah bebek yang bisa diintip}`. Saat kita sedang memproses bebek ke-$i$, dan ternyata bebek ke-$i$ bisa mengintip bebek yang berada _on the top of the stack_, berarti bebek ke-$i$ pasti bisa mengintip semua bebek yang bisa diintip oleh bebek yang ada di atas stack tersebut. Sambil kita mengupdate stacknya, jangan lupa untuk menghitung jawaban (sum) yang diminta :D

<details>
<summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;
using ll = long long;

int main(){
    ll n, sum = 0; cin >> n;
    stack<pair<ll, ll>>s;

    for(ll i = 0; i < n; i++){
        ll h; cin >> h;         
        ll tmp = 1;

        while(!s.empty() && s.top().first <= h){
            tmp += s.top().second;
            s.pop();
        }

        sum += tmp;
        s.push({h, tmp});
    }

    cout << sum << endl;

    return 0; 
}
```
</details>

## Komentar
    
- Untuk implementasi stack dan queue, biasakan untuk mengecek apakah stack/queue tersebut kosong atau tidak sebelum mencoba untuk mengakses/menghapus elementnya untuk menghindari error.   
Contoh: while(!s.empty() && ...) akan mengecek apakah stack tersebut sedang kosong atau tidak. Jika s sedang kosong, maka penyataan selanjutnya tidak akan dicheck kebenarannya. Jika kita mencoba mengakses s.top() saat s sedang kosong, maka kita akan mendapatkan verdict Runtime Error.

