# [D. Barisan Hewan Ternak](https://tlx.toki.id/courses/competitive/chapters/05/problems/D)

Author: Andreas Timothy

Untuk menyelesaikan problem ini, kita dapat membuat array _prefix sum_ dimana

$$
pref[i] = \displaystyle\sum_{j = 1}^i X[j]
$$

Perhatikan bahwa jenis hewan yang berada pada baris ke-$Y$ adalah nilai $i$ terkecil dimana $pref[i] \geq Y$. Kita dapat melakukan _binary search_ pada array $pref$ untuk mencari nilai $i$.

Kompleksitas Waktu: $O(Q log N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e5 + 5;
int n, x, pref[maxn], q, ki, ka, mid, res, y;

int main() {
  cin >> n;
  for (int i = 1; i <= n; i++) {
    cin >> x;
    pref[i] = pref[i - 1] + x;
  }
  cin >> q;
  while (q--) {
    cin >> y;
    ki = 1, ka = n;
    while (ki <= ka) {
      mid = (ki + ka) / 2;
      if (pref[mid] >= y)
        res = mid, ka = mid - 1;
      else
        ki = mid + 1;
    }
    cout << res << '\n';
  }
}
```

</details>

## Komentar

- Perhatikan pengisian array $pref[i] = pref[i - 1] + X[i]$, apabila untuk setiap $i$ kita melakukan iterasi ulang dari $1$ sampai $i$ maka program akan berjalan terlalu lambat dan hal ini justru mematikan purpose dari _prefix sum_.
- Solusi ini mendemonstrasikan penggunaan dasar dari _prefix sum_, tetapi nyatanya _prefix sum_ juga umum digunakan untuk permasalahan lain seperti _range query_, _brute force_, _dynamic programming_, dsb.

## Materi Yang Berhubungan

- [Prefix Sum Array - Implementation and Applications](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)
