# [F. Gaya Penulisan Variabel](https://tlx.toki.id/courses/basic/chapters/11/problems/F)

![Project sekai lul](https://cdn.discordapp.com/attachments/1023918533601661019/1099913076733640724/image.png)

Emu Otori mengucapkan selamat kepada yang telah menyelesaikan string di TLX <3

Author: Daniel Mangaraja Simanullang

<!-- Masukkan penjelasan disini -->
Pada soal ini, kita hanya perlu mengimplementasikan apa yang diminta soal. Untuk mengubah suatu karakter dari string dari kecil ke besar dan sebaliknya dapat dibaca di editorial [E. Bahasa Dengklek](https://tlx.toki.id/courses/basic/chapters/11/problems/E). Untuk mengubah gaya penulisan dari _snake_ ke _camel_, kita harus menghilangkan _underscore_ dan mengubah dari kecil ke besar. Kita bisa menghilangkan karakter tersebut dengan cara "melompat" (bisa dilihat di kode nanti). Untuk mengubah dari _camel_ ke _snake_, kita bisa mengeluarkan _underscore_ terlebih dahulu dan mengubah huruf besar ke kecil setelahnya.

Kompleksitas Waktu: $O(S.length())$

Kompleksitas Memori: $O(S.length())$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace __gnu_pbds;
using namespace std;

// defines
#define int long long
#define debug(x) cerr << "(" << #x << "=" << x << "," << __LINE__ << ")\n";
#define sz(x) (int)(x).size()
#define all(x) begin(x), end(x)
#define rep(i, a, b) for (int i = a; i < (b); i++)

// constants
const int dx[4]{1, 0, -1, 0}, dy[4]{0, 1, 0, -1};
const char dir[4]{'D', 'R', 'U', 'L'};
const int mod = 1e9 + 7;
const int maxn = 2e5 + 5;
const double eps = 1e-9;

// typedefs
typedef long long ll;
typedef pair<int, int> pii;
typedef vector<int> vi;

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
  int n = sz(s);
  for (int i = 0; i < n; i++) {
    if (s[i] == '_') {
      s[i + 1] -= 'a';
      s[i + 1] += 'A';
      cout << s[i + 1];
      i++; // lompat
      continue;
    } else if (s[i] >= 'A' and s[i] <= 'Z') {
      cout << "_";
      s[i] -= 'A';
      s[i] += 'a';
      cout << s[i];
    } else {
      cout << s[i];
    }
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