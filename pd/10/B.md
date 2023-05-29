# [Tukang Sulap](https://tlx.toki.id/courses/basic/chapters/10/problems/B)

Author: Hamiz Ghani

Pada soal ini kita akan menerima dua buah array, sebut saja array $A$ dan array $B$ dengan index dari $1...N$. Kemudian kita akan menerima $T$ buah input dengan format :
```c++
P x Q y
```

untuk setiap input tersebut, kita tinggal melakukan swap pada array tipe $P$ index ke-$X$ dengan array tipe Q index ke-$Y$ dengan menggunakan fungsi `swap()`

Kompleksitas Waktu: $O(2×N+T)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
int n, t, x, y;
char p, q;
int a[1005];
int b[1005];
main() {
  cin >> n;
  for (int i = 1; i <= n; i++) cin >> a[i];
  for (int i = 1; i <= n; i++) cin >> b[i];
  cin >> t;
  for (int i = 1; i <= t; i++) {
    cin >> p >> x >> q >> y;
    if (p == 'A' && q == 'A') {
      swap(a[x], a[y]);
    } else if (p == 'A' && q == 'B') {
      swap(a[x], b[y]);
    } else if (p == 'B' && q == 'A') {
      swap(b[x], a[y]);
    } else if (p == 'B' && q == 'B') {
      swap(b[x], b[y]);
    }
  }
  for (int i = 1; i <= n; i++) {
    cout << a[i] << " ";
  }
  cout << endl;
  for (int i = 1; i <= n; i++) {
    cout << b[i] << " ";
  }
  cout << endl;
}

```
</details>



<!-- Tambahkan komentar apabila perlu

## Komentar
    
- Komentar I
- Komentar II

-->

<!-- Tambahkan referensi link materi yang berhubungan apabila perlu
-->
## Materi Yang Berhubungan
    
-  [swap() in C++](https://www.geeksforgeeks.org/swap-in-cpp/)


<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal 1](link-soal)
- [Nama Soal II](link-soal)

-->