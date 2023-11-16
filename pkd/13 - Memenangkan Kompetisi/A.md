# [A. Angka Sangar](https://tlx.toki.id/courses/competitive/chapters/13/problems/A)

Author : Benedict Presley

Misal banyak digit dari bilangan $C$ adalah $L$, $L$ digit terakhir dari $AC \times BC$ ditentukan sepenuhnya oleh $C \times C$. Supaya persamaan $AC \times BC = NC$ terpenuhi, maka $C$ harus merupakan *suffix* dari $C^2$.

Kita dapat melakukan prekomputasi di luar program dan mendapat bahwa bilangan $C$ yang memenuhi adalah

$C \in \{1, 5, 6, 25, 76, 376, 625, 9376, 90625, 109376, 890625, 2890625, 7109376, 12890625, 87109376, 212890625, 787109376\}$

Setelah mendapat semua nilai $C$ yang valid, kita bisa memfaktorisasi setiap bilangan $NC$ dan memeriksa apakah terdapat $A$ dan $B$ yang memenuhi.

Perhitungan kompleksitas waktu untuk solusi ini sulit untuk ditentukan. Dalam kebanyakan kasus, solusi ini akan berjalan cukup cepat karena kita hanya perlu mencari satu solusi yang memenuhi. Sehingga meski kompleksitas waktu tampak besar, kita tetap bisa mendapat AC.

Karena nilai $C$ bisa cukup besar, untuk memfaktorisasi $NC$ diperlukan kompleksitas waktu $O(\sqrt{NC})$. Dalam kasus terburuk kompleksitas waktunya sama dengan $O(\max(N, C))$, yaitu saat jumlah digit $C$ lebih besar atau sama dengan jumlah digit $N$. Kompleksitas totalnya adalah $O(|C|N)$ dengan $|C|=$ banyakanya bilangan unik pada $C$.

Kompleksitas Waktu: $O(|C|N)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

#define ll long long

ll concatenate(ll u, ll v) {
  ll temp = v;
  while (temp > 0) {
    u *= 10LL;
    temp /= 10LL;
  }
  return u + v;
}

ll remove_last(ll u, ll v) {
  while (v > 0) {
    u /= 10LL;
    v /= 10LL;
  }
  return u;
}

bool get_last(ll u, ll v) {
  if (u < v) {
    return 0;
  }
  while (v > 0) {
    if (u % 10LL != v % 10LL) {
      return 0;
    }
    u /= 10LL;
    v /= 10LL;
  }
  return 1;
}

int main() {
  ios::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  vector<ll> list_C = {1,         5,        6,       25,       76,
                       376,       625,      9376,    90625,    109376,
                       890625,    2890625,  7109376, 12890625, 87109376,
                       212890625, 787109376};

  ll N;
  cin >> N;

  for (ll C : list_C) {
    ll a = 1;
    while (1) {
      ll A = concatenate(a, C);
      ll B = concatenate(N, C) / A;
      if (B < A) {
        break;
      }
      if (concatenate(N, C) % A == 0 && concatenate(N, C) % B == 0 &&
          get_last(B, C) && B != C) {
        cout << "YA\n" << remove_last(A, C) << " " << remove_last(B, C) << " "
             << C;
        return 0;
      }
      a++;
    }
  }
  cout << "TIDAK";

  return 0;
}
```

</details>

## Komentar

Karena *test case* yang mungkin lemah. Kita hanya perlu mencari $C$ antara $1$ hingga $100,000$.