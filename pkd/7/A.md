# [A. Uang Kembalian](https://tlx.toki.id/courses/competitive/chapters/07/problems/A)

Author: Muhammad Hasan

Pada soal ini kita diberikan $N$ buah koin bernilai $C_1, C_2, \dots, C_N$. Kemudian, kita disuruh untuk mencari banyaknya koin minimal yang diperlukan untuk mendapatkan nilai kembalian $K$.

Dalam mengerjakan soal-soal yang berhubungan dengan **Dynamic Programming** (DP), penting untuk kita tau, **definisi dari DP** yang ingin kita buat, **state-state awal** dan **transisi** yang dapat terjadi pada DP. Pada soal ini akan kita lihat demonstrasi pengerjaan soal DP.

Kemudian, disini akan dibahas $2$ solusi yang diharap bisa membantu pembaca memahami cara melakukan optimisasi DP.

**Catatan**:
- Solusi $1$ tidak cukup untuk batas **memory limit** yang diberikan, sehingga apabila ingin melihat solusi yang AC bisa melihat pada Solusi $2$.
- Solusi $1$ dan Solusi $2$ diberikan agar pembaca bisa melihat langkah observasi dan optimisasi yang dilakukan.

## Solusi $1$ - Dynamic Programming $2$ State

Kita dapat menggunakan Dynamic Programming (DP) $2$ State. 

Yang pertama perlu dilakukan adalah mencari definisi DP yang tepat. 

Dengan membaca dan menteliti soal, kita bisa membuat definisi DP sebagai berikut:

- $dp[i][j]=$ banyaknya koin kembalian minimal yang bisa didapat untuk nilai kembalian $j$ dan kita sudah bisa memakai koin $1$ sampai $i$.

Contohnya, apabila kita mempunyai koin seperti soal $[1,2,5,6]$, beberapa contoh nilai yang kita ekspektasi:

- $dp[1][2] = 2 \rightarrow$ Kita dapat mengambil koin berupa $1$ dan $1$.
- $dp[1][3] = 3 \rightarrow$ Kita dapat mengambil koin berupa $1$, $1$, dan $1$.
- $dp[2][2] = 1 \rightarrow$ Kita dapat mengambil koin berupa $2$.
- $dp[2][3] = 2 \rightarrow$ Kita dapat mengambil koin berupa $1$ dan $2$.

Kemudian, kita dapat mendefinisikan **state awal** kita dengan $dp[0][0]=0$, karena pada awalnya, kita tidak perlu memiliki koin apapun untuk nilai kembalian $0$ (hanya butuh tepat $0$ koin). 

Kemudian, untuk *state* awal lainnya, kita bisa asumsikan $dp[i][j]=\infty$ disini kita gunakan $\infty$ untuk menandakan bahwa $dp[i][j]$ mustahil untuk dilakukan
(atau dengan kata lain, tidak mungkin mendapatkan nilai tepat kembalian $j$ dengan memakai koin $1$ sampai koin $i$).

Terakhir, kita perlu mencari transisi DP yang tepat untuk soal ini.

Setelah menelaah, meriset, dan berpikir lama, maka bisa kita dapatkan transisi sebagai berikut:

- $dp[i][j] = \min(dp[i][j], dp[i-1][j]) \rightarrow$ Kita bisa tidak menggunakan nilai koin $C_i$ sama sekali
- $dp[i][j] = \min(dp[i][j], 1 + dp[i][j - c[i]]) \rightarrow$ Kita gunakan nilai koin $C_i$ **apabila** $j \geq C_i$.

Akhirnya, bisa kita dapatkan jawaban yang kita inginkan adalah $dp[N][K]$.

Kompleksitas Waktu: $O(NK)$

Kompleksitas Memori: $O(NK)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

const int INF = 1e9;
const int K = 5e4 + 5;

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  int n;
  cin >> n;
  vector<vector<int>> dp(n + 1, vector<int>(K, INF));
  dp[0][0] = 0;
  for (int i = 1; i <= n; i++) {
    int x;
    cin >> x;
    for (int j = 0; j < K; j++) {
      dp[i][j] = min(dp[i][j], dp[i - 1][j]);
      if (j >= x) {
        dp[i][j] = min(dp[i][j], 1 + dp[i][j - x]);
      }
    }
  }
  int k;
  cin >> k;
  cout << dp[n][k] << '\n';

  return 0;
}
```
</details>

## Solusi $2$ - Dynamic Programming $1$ State

Perhatikan bahwa, pada transisi sebelumnya hanya terjadi transisi antara $i$ dengan $i - 1$, biasanya soal-soal seperti ini bisa kita *optimize* menjadi **DP $1$ State** saja. Bagaimana cara optimisasinya? Mari kita lihat.

Kita akan lakukan hal yang mirip dengan penjelasan sebelumnya. 

Yang pertama perlu dilakukan adalah mencari definisi DP yang tepat. 

Kita bisa membuat definisi DP sebagai berikut:

- $dp[j]=$ banyaknya koin kembalian minimal yang bisa didapat untuk nilai kembalian $j$ dari koin yang sudah diproses.

Kemudian, kita dapat mendefinisikan **state awal** kita dengan $dp[0]=0$, lalu untuk *state* awal lainnya, kita bisa asumsikan $dp[j]=\infty$.

Pada solusi ini, saat kita *iterate* / proses koin $1$ sampai dengan koin $i$, kita akan melakukan transisi DP sebagai berikut:

- $dp[j] = \min(dp[j], 1 + dp[j - c[i]]) \rightarrow$ Kita gunakan nilai koin $C_i$ **apabila** $j \geq C_i$.

Akhirnya, bisa kita dapatkan jawaban yang kita inginkan adalah $dp[K]$.

Kompleksitas Waktu: $O(NK)$

Kompleksitas Memori: $O(K)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

const int INF = 1e9;
const int K = 5e4 + 5;

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  int n;
  cin >> n;
  vector<int> dp(K, INF);
  dp[0] = 0;
  for (int i = 1; i <= n; i++) {
    int x;
    cin >> x;
    for (int j = x; j < K; j++) {
      dp[j] = min(dp[j], 1 + dp[j - x]);
    }
  }
  int k;
  cin >> k;
  cout << dp[k] << '\n';

  return 0;
}
```
</details>

## Komentar
- Dengan optimisasi yang dilakukan kita bisa menghemat kompleksitas memori yang digunakan dan biasanya waktu eksekusi juga akan semakin cepat (walau terlihat harusnya sama).
- Pada solusi ini, penggunaan $\infty$ juga memudahkan kita dalam mencari nilai minimal, namun perlu diperhatikan juga untuk menjaga terjadinya *overflow*.
- Hasil dari jawaban tidak selalu nilai satu DP tertentu, bisa saja nilai minimum/maksimum dari DP yang kita dapatkan, bisa saja nilai jumlah dari DP yang kita dapatkan, oleh karena itu harus dibiasakan untuk latihan soal DP agar bisa menjawab apa yang diperlukan.
- Solusi-solusi DP biasanya terlihat *simple*, namun memang butuh banyak latihan soal agar bisa memiliki intuisi yang baik dalam mencari solusi tersebut, sehingga coba-coba terus saja untuk latihan DP.

## Materi Yang Berhubungan
- [Solving Minimum Coin Change Problem - Medium](https://trykv.medium.com/how-to-solve-minimum-coin-change-f96a758ccade)
- [Beginner Friendly Series on Dynamic Programming - CodeForces](https://codeforces.com/blog/entry/80064)
- [DP Tutorial and Problem List - CodeForces  ](https://codeforces.com/blog/entry/67679)


## Soal Yang Berhubungan
- [Coin Change - LeetCode](https://leetcode.com/problems/coin-change/)
- [Coin Change II - LeetCode](https://leetcode.com/problems/coin-change-ii/)
