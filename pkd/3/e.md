# [E. Pertemuan Pak Dengklek](https://tlx.toki.id/courses/competitive/chapters/03/problems/E)

Author: Andreas Timothy

Pada problem ini kita diminta untuk mengurutkan $N$ buah string berdasarkan panjangnya. Jika panjangnya sama maka urutkan secara leksikografis.

Problem ini cukup mudah diselesaikan dengan _bubble sort_, kita hanya perlu memperhatikan _logic_ pengecekannya saja (lihat pada kode di bawah).

Kompleksitas Waktu: $O(N^2)$

Kompleksitas Memori: $O(\text{Total panjang string})$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int n;
string s[505];

int main() {
  cin >> n;
  for (int i = 1; i <= n; i++) cin >> s[i];
  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) {
      // Cek apakah s[j] harus diletakkan setelah s[j+1]
      if (s[j].length() > s[j + 1].length() ||
          (s[j].length() == s[j + 1].length() && s[j] > s[j + 1])) {
        swap(s[j], s[j + 1]);
      }
    }
  }
  for (int i = 1; i <= n; i++) {
    cout << s[i] << '\n';
  }
}
```

</details>

## Komentar

- Detail implementasi dari _bubble sort_ sendiri dapat bervariasi, tetapi hasilnya sama saja
- Selain _bubble sort_ juga terdapat metode pengurutan lainnya yang dapat digunakan
