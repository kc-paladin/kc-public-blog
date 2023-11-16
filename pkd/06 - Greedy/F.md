# [F. Nomor Kandang](https://tlx.toki.id/courses/competitive/chapters/06/problems/F)

Author: Joceline Araki

_Welcome to soal paling ~~cancer~~ seru di Bab 6! :D_

Kita mulai dulu dengan beberapa observasi untuk soal ini. Untuk $2$ bilangan $a$ dan $b$, berlaku:  
1. Jika $\text{jumlah digit }a>\text{jumlah digit }b$, maka bisa dipastikan kalau $a > b$. 
Contoh: $1111 > 999$
2. Jika $\text{jumlah digit }a=\text{jumlah digit }b$, dan misalkan $i$ adalah index dimana digit $a$ dan $b$ tidak sama untuk pertama kalinya (dari kiri), maka jika $a_i > b_i$, bisa dipastikan kalau $a > b$.  
Contoh: $1989 > 1899$ $(a_2 > b_2)$

Dari observasi $1$, kita bisa mengetahui bahwa sebenarnya untuk mendapatkan nomor kandang yang maksimum, kita membutuhkan jumlah digit yang maksimum juga. Oleh karena itu, kita bisa menggunakan konsep _greedy_ dan membeli plat dengan harga termurah sebanyak-banyaknya supaya mendapatkan jumlah digit sebanyak mungkin. Misalkan jumlah plat maksimum yang bisa kita beli adalah $P$. Maka bisa disimpulkan bahwa:

$$P = \frac{M}{\text{Harga Plat Minimum}}$$.

Setelah kita mengetahui jumlah plat (digit) terbanyak yang bisa didapatkan, _next_ kita harus construct jawabannya (bagian cancernya :D). Dari observasi kedua, kita bisa menyimpulkan kalau digit-digitnya harus disusun dari terbesar ke terkecil. Oke, kalo gitu kita beli aja platnya dari angka 9 sampai 0? _Technically yes_, tapi ingat kalau kita harus bisa membeli $P$ buah plat!

Caranya simpel, kita harus tahu berapa jumlah plat yang bisa dibeli untuk setiap digit. Misalkan kita membeli plat $D$ sebanyak $X$ buah, dan uang yang tersisa adalah $M_{sisa}$, maka uang sisa tersebut _harus_ bisa dipakai untuk membeli digit lain sampai mencukupi $P$ digit.

Atau secara formal, $\displaystyle P = \frac{M_ {sisa}}{\text{Harga Plat Minimum}} + X$. Sambil kita mencari nilai $D$ dan $X$, kita juga harus menyimpan $50$ digit pertama dan terakhir yang bisa dibeli. Hal ini bisa dibantu dengan beberapa struktur data. Nilai $X$ bisa dicari dengan _math_ ataupun _binary search_. _Happy Implementing!_ 😈 

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
#define int long long

using namespace std;

int binser(int money, int price, int len, int cheapest) {
  int l = 0, r = money / price;
  int ret = 0;

  while (l <= r) {
    int mid = (l + r) / 2LL;
    int rem = money - (price * mid);
    if (rem / cheapest + mid >= len) {
      l = mid + 1LL;
      ret = mid;
    } else {
      r = mid - 1LL;
    }
  }

  return ret;
}

void printAns(deque<int>& ans) {
  while (!ans.empty()) {
    cout << ans.front();
    ans.pop_front();
  }

  cout << '\n';
}

int32_t main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);
  int n;
  cin >> n;
  vector<pair<int, int>> v(n + 1), tmp(n + 1);
  int mini = LLONG_MAX;

  for (int i = 0; i <= n; i++) {
    cin >> v[i].first;
    v[i].second = i;
    mini = min(mini, v[i].first);
  }

  int m;
  cin >> m;

  int len = m / mini;

  tmp = v;
  sort(tmp.begin(), tmp.end());
  if (tmp[0].second == 0) {
    if (n && m >= tmp[1].first) {
      len = (m - tmp[1].first) / mini + 1LL;
    } else {
      len = (m >= tmp[0].first);
    }
  }

  int ans = len;
  deque<int> ans1, ans2;
  bool zero = false;

  for (int i = n; i >= 0; i--) {
    int buy = binser(m, v[i].first, len, mini);
    m -= v[i].first * buy;
    len -= buy;

    while (ans1.size() < 50 && buy) {
      ans1.push_back(i);
      ans2.push_back(i);
      buy--;
      if ((ans1.size() == 1) && !i) {
        ans = 1;
        zero = true;
        break;
      }
    }

    if (zero) break;

    if (buy) {
      if (buy >= 50) {
        ans2.clear();
        for (int j = 1; j <= 50; j++) ans2.push_back(i);
      } else {
        for (int j = 1; j <= buy; j++) {
          ans2.pop_front();
          ans2.push_back(i);
        }
      }
    }
  }

  if (!ans) {
    cout << 0 << '\n';
    return 0;
  }

  cout << ans << '\n';
  printAns(ans1);
  printAns(ans2);

  return 0;
}
```
</details>

## Komentar
- Implementasi dan solusi diatas hanyalah salah satu cara untuk meng-_approach_ soal ini. Ada banyak approach dan solusi lain untuk mengerjakan soal ini. Misalnya, implementasi di atas menggunakan _binary search_ untuk mencari nilai $X$. Tapi sebenarnya ada approach lain yang hanya memanfaatkan _math_ saja :D. Jika kalian mempunyai approach yang berbeda, _don't hesitate to try it first!_ 
## Soal yang berhubungan
- [Addition and Multiplication 2 (AtCoder)](https://atcoder.jp/contests/abc257/tasks/abc257_e)