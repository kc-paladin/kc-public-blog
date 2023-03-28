# [A. Kupon Berhadiah](https://tlx.toki.id/courses/competitive/chapters/03/problems/A)

Author: Andreas Timothy

Pada dasarnya problem ini hanya meminta kita untuk mencari kupon dengan selisih terkecil terhadap kupon $X$, apabila ada lebih dari 1 kupon yang memenuhi keluarkan kupon dengan nomor terkecil.

Untuk menyelesaikan problem ini, kita cukup mengecek selisih setiap kupon dengan kupon $X$ dan mengambil selisih yang terkcil. Apabila terdapat selisih yang sama maka pilih kupon dengan nomor terkecil.

Kompleksitas Waktu: $O(N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int n, x, pemenang, a[1005];

int main() {
  cin >> n >> x;
  for (int i = 1; i <= n; i++) {
    cin >> a[i];
    if (i == 1) {
      // inisialisiasi kupon pertama sebagai pemenang
      pemenang = i;
    } else {
      if (abs(a[i] - x) < abs(a[pemenang] - x) ||
          (abs(a[i] - x) == abs(a[pemenang] - x) && a[i] < a[pemenang])) {
        pemenang = i;
      }
    }
  }
  cout << a[pemenang] << '\n';
}
```

</details>

## Komentar

- Detail implementasi pada problem ini mungkin bisa bervariasi, tetapi pada intinya sama saja.
