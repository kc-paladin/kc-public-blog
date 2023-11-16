# [G. Jabat Tangan](https://tlx.toki.id/courses/competitive/chapters/07/problems/G)

Author : Benedict Presley

Hal yang dapat kita lakukan saat kita tidak tau cara "menyerang" suatu soal adalah mencari pola. Kita dapat mencoba beberapa nilai $N$ yang kecil. Dapat kita temukan bahwa saat nilai $N = 3$ atau $N = 5$, maka nilainya adalah $0$. Hal ini dapat kita buktikan, perhatikan bahwa setiap orang harus menjabat tangan seorang yang lain. Jika $N$ ganjil, akan terdapat $1$ orang yang tidak berjabat tangan dengan siapapun.

Untuk $N$ bernilai genap, tidak ada pola tertentu yang bisa kita manfaatkan. Mari kita perhatikan struktur dari soal ini. Misal terdapat $8$ orang. Kita coba memasangkan orang ke-$1$ dengan orang ke-$6$.

Perhatikan bahwa sekarang orang ke-$2$, ke-$3$, ke-$4$, dan ke-$5$ tidak dapat dipasangkan dengan orang ke-$7$ dan ke-$8$ karena akan bersilangan dengan orang ke-$1$ dan ke-$6$. Maka banyak cara memasangkan sisanya sama saja dengan banyak memasangkan $4$ orang dikali dengan banyak cara memasangkan $2$ orang.

Untuk menghitung semua kemungkinan, maka kita perlu mencoba memasangkan orang ke-$1$ dengan semua orang lain.

Misalkan $dp(N)$ = banyak cara melakukan "jabat tangan sempurna" dengan $N$ orang.

Untuk kemudahan, kita misalkan $dp(0) = 1$.

Jika $N$ ganjil, $dp(N) = 0$.

Selain itu
$$dp(N) = dp(0) \times dp(N - 2) \, + \, dp(1) \times dp(N - 3) \, + \, ... \, + \, dp(N-2) \times dp(0)$$.

Kompleksitas Waktu: $O(N^2)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <iostream>
using namespace std;

long long dp[51];

int main() {
  ios::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  int N;
  cin >> N;

  // Implementasi menggunakan DP bottom up;

  dp[0] = 1;
  for (int i = 1; i <= N; ++i) {
    if (i & 1) {  // Jika i bernilai ganjil
      dp[i] = 0;
    } else {
      for (int j = 0; j <= i - 2; ++j) {
        dp[i] += dp[j] * dp[i - j - 2];
      }
    }
  }

  cout << dp[N];

  return 0;
}
```

</details>