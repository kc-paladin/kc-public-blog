# [Knapsack](https://tlx.toki.id/courses/competitive/chapters/07/problems/B)

Author: Hamiz Ghani

Diberikan $K$ batu. Masing-masing batu memiliki nilai $w[i]$ yaitu berat batu dan $h[i]$ harga batu. Kita ingin menampung batu tersebut dalam tas dengan kapasitas maksimal $N$ sehingga harga batu dalam tas menjadi maksimal. 

Definisikan sebuah fungsi $dp(x,y)$ adalah harga jual maksimal yang bisa kita dapatkan dengan kapasitas $x$ dengan memilih batu-batu dari $1,2,..,y$. Dapat disimpulkan kita bisa mendapatkan harga jual maksimal dengan memanggil $dp(n,k)$.

**Transisi**
- Apabila untuk suatu $dp(x,y)$ kita memilih untuk tidak mengambil batu $y$, kapasitas tas tidak berkurang dan kita akan mempertimbangkan batu selanjutnya yaitu $y-1$. Sehingga kita akan memanggil $dp(x,y-1)$
- Apabila untuk suatu $dp(x,y)$ kita memilih untuk mengambil batu ke-$y$, kapasitas tas akan berkurang menjadi $x-w[y]$. Perhatikan bahwa kita hanya dapat mengambil batu ke-$y$ apabila $w[y]<=x$ , Sehingga kita akan memanggil $dp(x-w[y],y-1)$

Kedua transisi di atas dapat kita tuliskan dalam pseudocode berikut :
```c++
if (x >= w[y])
    return max(dp(x, y - 1), dp(x - w[y], y - 1) + h[y]);
  else
    return dp(x, y - 1);
```

Pada fungsi $dp(x,y)$ kita sudah tidak bisa mengambil batu lagi apabila $y=0$ , sehingga kita akan melakukan `return 0`. Untuk mempercepat kompleksitas kita juga akan melakukan memoisasi sehingga kita akan menyimpan nilai $dp(x,y)$ dalam $memo[x][y]$ dan menyimpan suatu $boolean$ yang menandakan bahwa $dp(x,y)$ sudah pernah dipanggil sebelumnya.

```c++
if (vis[x][y]) return memo[x][y];
  vis[x][y] = 1;
  if (y == 0) return 0;
  if (x >= w[y])
    return memo[x][y] = max(dp(x, y - 1), dp(x - w[y], y - 1) + h[y]);
  else
    return memo[x][y] = dp(x, y - 1);
```

Sekarang kita sudah punya kumpulan nilai $dp(x,y)$ yang disimpan dalam $memo[x][y]$. Kita akan menggunakan fungsi $backtrack$ untuk menentukan dan menyimpan batu mana saja yang diambil dalam $dp(n,k)$.

Perhatikan bahwa apabila ada lebih dari 1 kemungkinan pengambilan yang menghasilkan harga jual maksimal, kita akan mengambil nomor batu yang lebih kecil, sehingga kita akan memperkecil $n$ dan $k$ dengan cara berikut :
```c++
while (n > 0) {
    if (dp(n, k) == dp(n - 1, k))
      n--;
    else
      break;
  }
  while (k > 0) {
    if (dp(n, k) == dp(n, k - 1))
      k--;
    else
      break;
  }
```

**Backtrack**

Fungsi *backtrack* kita berlaku sebagai berikut :

- Apabila $dp(x,y)=dp(x,y-1)$, maka batu ke-$y$ tidak akan kita ambil.
- Apabila $dp(x,y)=dp(x-w[y],y-1)+h[y]$, maka batu ke-$y$ akan kita ambil.

```c++
int backtrack(int x, int y) {
  if (y == 0) return 0;
  if (x < w[y]) return backtrack(x, y - 1);
  if (dp(x, y) == dp(x, y - 1)) return backtrack(x, y - 1);
  if (dp(x, y) == dp(x - w[y], y - 1) + h[y]) {
    ans.pb(y);
    return backtrack(x - w[y], y - 1);
  }
}
```


Kompleksitas Waktu: $O(NK)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
#define ll long long
#define fi first
#define sec second
#define pb push_back
#define pqueue priority_queue
#define pair <long long, long long> pii
#define int long long
using namespace std;
ll t, n, m, k;
int w[2005];
int h[2005];
int memo[2005][105];
bool vis[2005][105];
vector<int> ans;
int dp(int x, int y) {
  if (vis[x][y]) return memo[x][y];
  vis[x][y] = 1;
  if (y == 0) return 0;
  if (x >= w[y])
    return memo[x][y] = max(dp(x, y - 1), dp(x - w[y], y - 1) + h[y]);
}
int backtrack(int x, int y) {
  if (y == 0) return 0;
  if (x < w[y]) return backtrack(x, y - 1);
  if (dp(x, y) == dp(x, y - 1)) return backtrack(x, y - 1);
  if (dp(x, y) == dp(x - w[y], y - 1) + h[y]) {
    ans.pb(y);
    return backtrack(x - w[y], y - 1);
  }
}
main() {
  ios_base::sync_with_stdio(false);
  cin.tie(NULL);
  cout.tie(0);
  cin >> n >> k;
  for (int i = 1; i <= k; i++) {
    cin >> w[i] >> h[i];
  }
  dp(n, k);
  while (n > 0) {
    if (dp(n, k) == dp(n - 1, k))
      n--;
    else
      break;
  }
  while (k > 0) {
    if (dp(n, k) == dp(n, k - 1))
      k--;
    else
      break;
  }
  backtrack(n, k);
  sort(ans.begin(), ans.end());
  for (int i = 0; i < ans.size(); i++) {
    cout << ans[i] << endl;
  }
}
```
</details>



<!-- Tambahkan komentar apabila perlu
-->
## Komentar

- Total kompleksitas waktu adalah $O(NK)$ yaitu sebesar size dari array $memo$ 


<!-- Tambahkan referensi link materi yang berhubungan apabila perlu
-->



<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal 1](link-soal)
- [Nama Soal II](link-soal)

-->