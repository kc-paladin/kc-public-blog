# [E. Bahasa Dengklek](https://tlx.toki.id/courses/basic/chapters/11/problems/E)

Author: Daniel Mangaraja Simanullang

<!-- Masukkan penjelasan disini -->
Pada soal ini, kita hanya perlu mengganti huruf besar menjadi kecil dan kecil menjadi besar. Salah satu cara yang bisa digunakan adalah memanfaatkan tipe data _char_ yang bersifat seperti _int_. Untuk mengubah dari besar ke kecil kita hanya perlu menggunakan:

`S[i] = 'a' + S[i] - 'A'`

dan dari kecil ke besar:

`S[i] = 'A' + S[i] - 'a'`

Kompleksitas Waktu: $O(|S|)$

Kompleksitas Memori: $O(|S|)$

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
  for (int i = 0; i < sz(s); i++) {
    if (s[i] >= 'A' and s[i] <= 'Z') {
      s[i] -= 'A';
      s[i] += 'a';
    } else {
      s[i] -= 'a';
      s[i] += 'A';
    }
    cout << s[i];
  }
  cout << '\n';

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