# [I. Terpendek ke-K](https://tlx.toki.id/courses/competitive/chapters/03/problems/I)

Author: Andreas Timothy

Pada problem ini kita hanya diminta untuk mengurutkan bilangan-bilangan dari terkecil ke terbesar, lalu mengeluarkan bilangan pada urutan ke-$K$. Kita juga tidak dituntut untuk menggunakan algoritma _sorting_ tertentu. Saya akan menggunakan _bubble sort_ pada kode di bawah.

Kompleksitas Waktu: $O(N^2)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int n, k, a[1005];

int main() {
  cin >> n >> k;
  for (int i = 1; i <= n; i++) cin >> a[i];

  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) {
      if (a[j] > a[j + 1]) swap(a[j], a[j + 1]);
    }
  }

  cout << a[k] << '\n';
}
```

</details>

## Komentar

- Feel free untuk menggunakan algoritma _sorting_ yang kalian suka😊
