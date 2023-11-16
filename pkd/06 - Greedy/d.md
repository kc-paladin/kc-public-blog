# [D. Beli Cokelat](https://tlx.toki.id/courses/competitive/chapters/06/problems/D)

Author: Andreas Timothy

Solusi dari problem ini cukup _straightforward_; untuk memaksimalkan banyaknya bebek yang dapat dibuat senang, kita cukup **memprioritaskan** cokelat dengan harga termurah, lalu membeli setiap jenis cokelat dalam jumlah maksimum yang **_reasonable_**, yaitu $\displaystyle min\left(B_i, \frac{\text{sisa dana}}{H_i}\right)$.

Kompleksitas Waktu: $O(N \log N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
#define ll long long

const int maxn = 1e5 + 5;
int n;
ll d, quantity, ans;
pair<ll, ll> a[maxn];

int main() {
  cin >> n >> d;
  for (int i = 1; i <= n; i++) cin >> a[i].first >> a[i].second;
  sort(a + 1, a + n + 1);
  for (int i = 1; i <= n; i++) {
    quantity = min(a[i].second, d / a[i].first);
    ans += quantity;
    d -= a[i].first * quantity;
  }
  cout << ans << '\n';
}
```

</details>
