# [B. Group Piala Dunia](https://tlx.toki.id/courses/competitive/chapters/04/problems/B)

Author: Muhammad Hasan

Misalkan $S$ merupakan himpunan dari pasangan setiap $N$ tim. Sebagai contoh apabila terdapat $N=4$ tim maka:

- $S = \{(1,2),(1,3),(1,4),(2,3),(2,4),(3,4)\}$

Kita akan dapatkan bahwa:

$$|S| = \binom{N}{2} = \frac{N \times (N - 1)}{2}$$

Karena $N \leq 5$ kita dapatkan $|S| \leq 10$, sehingga $|S|$ bisa dibilang relatif kecil dan bisa kita manfaatkan.

Perhatikan bahwa skor setiap tim dihasilkan dari hasil pertandingan pada $S$.

Untuk setiap $(i, j)$ pada $S$ kita bisa dapatkan tiga kemungkinan:

- Tim $i$ menang, maka skor tim $i$ ditambah $3$.
- Tim $j$ menang, maka skor tim $j$ ditambah $3$.
- Seri, maka skor tim $i$ dan tim $j$ ditambah $1$

Oleh karena itu kita bisa mencoba simulasi semua kemungkinan hasil skor $N$ tim untuk setiap $2 \leq N \leq 5$.

Untuk setiap $(i, j)$ pada $S$ kita coba semua $3$ kemungkinan yang mungkin, kita akan dapatkan kompleksitas waktu $O(3^{|S|})$, karena tadi $|S| \leq 10$ ini masih memungkinkan.

Untuk setiap hasil skor kita dapat masukkan ke dalam suatu `set` dan kemudian apabila diberikan hasil skor, kita cukup cek apakah hasil skor tersebut ada dalam `set` hasil skor yang memungkinkan.

Kompleksitas Waktu: $O\left(3^{N^2} + T \times \left(N + \log \left(3^{N^2}\right)\right)\right)$, dengan $T=$ banyaknya kasus uji.

Kompleksitas Memori: $O\left(N+3^{N^2}\right)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

set<vector<int>> st;
vector<int> res;
vector<pair<int, int>> p;

void gen(int pos) {
  if (pos >= p.size()) {
    st.emplace(res);
    return;
  }
  int x = p[pos].first;
  int y = p[pos].second;
  // win
  {
    res[x] += 3;
    res[y] += 0;
    gen(pos + 1);
    res[x] -= 3;
    res[y] -= 0;
  }
  // draw
  {
    res[x] += 1;
    res[y] += 1;
    gen(pos + 1);
    res[x] -= 1;
    res[y] -= 1;
  }
  // lose
  {
    res[x] += 0;
    res[y] += 3;
    gen(pos + 1);
    res[x] -= 0;
    res[y] -= 3;
  }
}

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  for (int x = 2; x <= 5; x++) {
    res.clear();
    p.clear();
    res.assign(x, 0);
    for (int i = 0; i < x; i++) {
      for (int j = i + 1; j < x; j++) {
        if (i == j) {
          continue;
        }
        p.emplace_back(i, j);
      }
    }
    gen(0);
  }

  int tc;
  cin >> tc;
  while (tc--) {
    int n;
    cin >> n;
    vector<int> a(n);
    for (int i = 0; i < n; i++) {
      cin >> a[i];
    }
    if (st.find(a) == st.end()) {
      cout << "NO" << '\n';
    } else {
      cout << "YES" << '\n';
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