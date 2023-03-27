# [D. Palindrom](https://tlx.toki.id/courses/competitive/chapters/07/problems/D)

Author: Ackhava Adam Malonda

Soal ini dapat dikerjakan dengan DP(*dynamic programming*) *2-state*.

Anggap $S[i]$ adalah karakter pada *index* ke $i$ (zero-based), $L$ adalah panjang dari $S$, serta $L_{max}$ adalah nilai maksimal $L$ untuk semua kasus. Lalu, anggap $dp(x,y)$ adalah jawaban soal tersebut untuk *substring* $S[x],S[x+1],\ldots,S[y-1], S[y]$. Untuk memecahkan masalah ini menjadi *subproblem*, ada dua kasus:
- $S[x]=S[y]$

    Dalam kasus ini, cara paling efektif untuk mendapat palindrom terpanjang adalah untuk mengambil kedua karakter secara sekaligus. Alhasil, jawabannya adalah $dp(x+1, y-1)+2$.

- $S[x]\neq S[y]$

    Dalam kasus ini, kita dapat mengabaikan $S[x]$ _atau_ $S[y]$. Karena kita belum tahu pilihan yang akan mendapatkan jawaban terbesar, jalankan kedua kasus saja. Maka jawabnnya adalah $\min(dp(x+1,y), dp(x,y-1))$.

Selain rekursinya, ada 2 *base case* yang perlu dibuat juga:
- $x=y$

    Untuk kasus ini akan hanya terdapat satu karakter. Sebab satu karakter selalu palindrom, maka jawabannya $1$.

- $x\gt y$

    Jika ini terjadi, maka *substring* sudah kosong. Maka dari itu, panjang maksimal yang dapat dibuat adalah 0, sebab *string* kosong juga palindrom.

Untuk jawaban akhirnya dapat didapat dari $dp(0,L-1)$.

Kompleksitas Waktu: $O(NL_{max}^2)$, dimana ada $N$ kasus uji.

Kompleksitas Memori: $O(L_{max}^2)$ untuk *array* memoisasi.

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;

ll N;
string s;
ll memo[200][200];

ll dp(ll x, ll y) {
  if (x > y) return 0;

  if (x == y) return 1;

  ll &ans = memo[x][y];

  if (ans == -1)

    if (s[x] == s[y]) {
      ans = dp(x + 1, y - 1) + 2;
    } else {
      ans = max(dp(x, y - 1), dp(x + 1, y));
    }

  return ans;
}

int main() {
  ios_base::sync_with_stdio(false);
  cin.tie(0);
  cout.tie(0);

  cin >> N;

  for (ll i = 0; i < N; i++) {
    memset(memo, -1, sizeof memo);
    cin >> s;
    cout << dp(0, s.size() - 1) << '\n';
  }
}
```
</details>

## Komentar
- Meskipun `long long` digunakan dalam kasus ini, hal tersebut mungkin tidak mutlak diperlukan, mengingat batasan soal, dan `int` dapat memumpuni (penulis belum menguji ataupun memverifikasi hal tersebut, sehingga dapat dicoba oleh pembaca).
