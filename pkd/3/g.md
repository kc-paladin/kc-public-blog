# [Kualitas Baju](https://tlx.toki.id/courses/competitive/chapters/03/problems/G)

Author: Andreas Timothy

Pada problem ini kita diminta untuk mencari **median** dari $N$ buah bilangan. Untuk mencari nilai median, kita perlu mengurutkan bilangan-bilangan tersebut terlebih dahulu.

Perhatikan bahwa ada sesuatu yang unik pada batasan problem ini. Nilai $N$ yang besar tidak memungkinkan kita untuk menggunakan algoritma _sorting_ seperti yang sudah kita pakai sebelumnya. Tetapi yang unik adalah bilangan-bilangan inputnya hanya berkisar antara $1$ hingga $100$.

Terdapat algoritma _sorting_ yang kompleksitasnya bergantung pada rentang bilangan-bilangannya, yaitu _counting sort_. _Counting sort_ cocok digunakan pada problem ini karena rentang bilangan inputnya yang kecil.

Kompleksitas Waktu: $O(N + M)$

Kompleksitas Memori: $O(N + M)$

> Catatan: $M$ adalah rentang bilangan pada input.

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int n, a[100005], ftable[105];

int main() {
  cin >> n;
  for (int i = 0; i < n; i++) {
    cin >> a[i];
    ftable[a[i]]++;
  }

  int pos = 0;
  for (int i = 1; i <= 100; i++) {
    for (int j = 0; j < ftable[i]; j++) {
      a[pos] = i;
      pos++;
    }
  }

  if (n % 2 == 0) {
    double x = a[n / 2], y = a[n / 2 - 1];
    cout << setprecision(1) << fixed << (x + y) / 2 << "\n";
  } else {
    cout << a[n / 2] << ".0\n";
  }
}
```

</details>

## Komentar

- Selain menggunakan _counting sort_ kita juga dapat menggunakan algoritma pengurutan cepat lainnya seperti _merge sort_, _quick sort_, ataupun dengan bantuan `std::sort`. Tetapi algoritma-algoritma tersebut di luar dari scope editorial ini.
