# [C. Wildcard](https://tlx.toki.id/courses/competitive/chapters/01/problems/C)

Author: Muhammad Hasan

Perhatikan bahwa dipastikan terdapat tepat $1$ karakter `'*'` pada string masukkan, sebut saja sebagai string $S$.

Misalkan $pos$ merupakan index pada $S$ sedemikian sehingga $S[pos] =$ `'*'`.

Maka, apabila diberikan string $P$, kita dapat mengecek apakah string $P$ dapat dicocokkan dengan string $S$ dengan cara sebagai berikut:

- Apabila panjang $P$ terlalu kecil atau $|P|<|S|-1$ maka $P$ tidak mungkin dicocokkan dengan string $S$.
- Dedifinisikan $X =$ (Prefix dari $P$ dengan panjang $pos - 1$) $+$ `"*"` $+$ (Suffix dari $P$ dengan panjang $|S|- pos)$
- Maka string $P$ dapat dicocokkan dengan string $S$ jika dan hanya jika $S=X$.
- Kita dapat gunakan utilitas `substr` pada C++ untuk mendapatkan prefix / suffix suatu string.

Kompleksitas Waktu: $O(|S| + T \times |P|)$ dengan $T = $ banyaknya kasus uji 

Kompleksitas Memori: $O(|S| + |P|)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  string s;
  cin >> s;
  int n = s.length();
  int pos = s.find('*');
  int tc;
  cin >> tc;
  while (tc--) {
    string p;
    cin >> p;
    int m = p.length();
    if (m < n - 1) {
      continue;
    }
    string cur = p.substr(0, pos) + "*" + p.substr(m - (n - pos - 1));
    if (cur == s) {
      cout << p << '\n';
    }
  }

  return 0;
}
```
</details>

## Komentar
    
- Dalam mencari prefix / suffix dari suatu string, kita juga bisa membuat fungsi sendiri tanpa menggunakan `substr`.
    
## Materi Yang Berhubungan

- [C++ Substring](https://cplusplus.com/reference/string/string/substr/)