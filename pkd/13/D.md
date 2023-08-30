# [D. Raja Bebek](https://tlx.toki.id/courses/competitive/chapters/13/problems/D)

Author: Joceline Araki

Prerequisite: DP Knapsack

Di soal ini, kita diberikan suatu array $[A_1, A_2, ..., A_N]$ dan sebuah angka $Y$. Kita harus mencari berapa banyak elemen minimum agar jumlah dari elemen-elemen tersebut sama dengan $Y$. Secara formal, kita harus mencari suatu subsequence $S = [A_x, A_y, ..., A_z]$ dimana $sum(S) = Y$ dan $S.size()$ minimum.

Bisa dilihat bahwa problem ini bisa diselesaikan dengan cara DP Knapsack. Untuk setiap $A_i$, kita bisa mencari nilai minimum elemen yang dibutuhkan untuk tiap $sum = [0..Y]$.

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

const int N = 1002;
vector<int>w(N, 1e9);

int main(){ 
    ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
    int n, y; cin >> n >> y;
    w[0] = 0;

    for(int i = 1; i <= n; i++){
        int x; cin >> x;
        for(int j = y; j - x >= 0; j--){
            w[j] = min(w[j], w[j - x] + 1);
        }
    }

    if(w[y] == 1e9) cout << -1 << '\n';
    else cout << w[y] << '\n';

    return 0;
}
```
</details>

## Materi Yang Berhubungan
- [USACO - Knapsack](https://usaco.guide/gold/knapsack)
- [TLX - PKD Bab 7 (DP)](https://tlx.toki.id/courses/competitive/chapters/07/lessons/A)

## Soal Yang Berhubungan
- [AtCoder - Knapsack 1](https://atcoder.jp/contests/dp/tasks/dp_d)
- [AtCoder - Knapsack 2](https://atcoder.jp/contests/dp/tasks/dp_e)


