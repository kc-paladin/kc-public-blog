# [C. Caesar Cipher](https://tlx.toki.id/courses/basic/chapters/11/problems/C)

Author: Daniel Simanullang

<!-- Masukkan penjelasan disini -->

Soal ini hanya meminta kita untuk menerapkan soal klasik. Inti dari soal ini adalah kita harus menggeser suatu karakter dari string sepanjang $k$. Contohnya kita memiliki sebuah karakter __A__ pada string. Maka untuk menggeser __A__ sejauh 1 karakter kita harus mengubahnya menjadi __B__. Apabila suatu pergeseran melebihi batas (contohnya seperti menggeser __Z__), maka kita harus balik ke posisi awal, yaitu __A__. Kita dapat menggunakan operasi $S_i$ = $S_i$ + $k$ atau $S_i$ = $S_i$ + $k$ - 26 jika melebihi batas, dimana $S$ adalah string dari input.

Kompleksitas Waktu: $O(S.length())$

Kompleksitas Memori: $O(S.length())$

<details>
  <summary>Solution Code</summary>

```c++
// Copy paste solution code yang sudah diformat
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace __gnu_pbds;
using namespace std;

// defines
#define int long long
#define debug(x) cerr << "(" << #x << "=" << x << "," << __LINE__ << ")\n";
#define sz(x) ((int)x.size());
#define all(x) (x).begin(), (x).end();

// constants
const int dx[4]{1, 0, -1, 0}, dy[4]{0, 1, 0, -1};
const char dir[4]{'D', 'R', 'U', 'L'};
const int mod = 1e9 + 7;
const int maxn = 2e5 + 5;
const double eps = 1e-9;

// typedefs
typedef vector<vector<int>> vii;
typedef vector<int> vi;
typedef pair<int, int> pii;

// Template
template <class T>
using oset =
    tree<T, null_type, less<T>, rb_tree_tag, tree_order_statistics_node_update>;

// Mods
int mul(int a, int b, int MOD) { return ((a % MOD) * (b % MOD)) % MOD; }
int add(int a, int b, int MOD) { return (a + b) % MOD; }
int sub(int a, int b, int MOD) { return (MOD + a - b) % MOD; }

signed main() {
  ios_base::sync_with_stdio(false);
  cin.tie(NULL);
  string s;
  cin >> s;
  int k;
  cin >> k;
  int n = s.size();
  for (int i = 0; i < n; i++) {
    int dist = ((int)s[i] + k);
    if (dist > (int)'z') {
      dist -= 26;
    }
    cout << (char)dist;
  }

  return 0;
}
```
</details>

<!-- Tambahkan komentar apabila perlu

## Komentar
    
- Komentar I
- Komentar II

-->

<!-- Tambahkan referensi link materi yang berhubungan apabila perlu

## Materi Yang Berhubungan
    
- [Materi I](link-materi)
- [Materi II](link-materi)

-->

<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal I](link-soal)
- [Nama Soal II](link-soal)

-->