# [A. Membangun Jalan Antar Kandang](https://tlx.toki.id/courses/competitive/chapters/10/problems/A)

![Willy](https://cdn.discordapp.com/attachments/1023918533601661019/1093028579329187880/image.png)

Sebuah percakapan di *Errichto Server Official*

Author: Daniel Simanullang

Prerequisite(s) : Disjoint Set Union (DSU)

<!-- Masukkan penjelasan disini -->

Soal ini hanyalah soal DSU klasik. Kita hanya perlu menggunakan 2 operasi, yaitu $merge$ dan $connected$. Disini, $merge$ adalah operasi untuk menggabungkan 2 node (atau pada konteks soal ini yaitu kandang) dan $connected$ adalah operasi untuk mengecek apakah 2 node terhubung atau tidak. Operasi tambahan seperti $find$ digunakan untuk mencari parent dari suatu node.

Kompleksitas Waktu: $O$(log $N$)

Kompleksitas Memori: $O(N)$

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

struct UnionFind {
  vector<int> par, sz;
  UnionFind(int n) {
    par.resize(n + 1);
    sz.resize(n + 1, 1);
    for (int i = 1; i <= n; i++) {
      par[i] = i;
    }
  }
  int find(int x) { return (par[x] == x ? x : par[x] = find(par[x])); }
  bool merge(int x, int y) {
    int a = find(x);
    int b = find(y);
    if (a == b) {
      return 0;
    }
    if (sz[a] < sz[b]) {
      swap(a, b);
    }
    sz[a] += sz[b];
    par[b] = a;
    return 1;
  }
  bool connected(int x, int y) { return find(x) == find(y); }
};
signed main() {
  ios_base::sync_with_stdio(false);
  cin.tie(NULL);
  int n, m;
  cin >> n >> m;
  UnionFind DSU(n + 1);
  for (int i = 0; i < m; i++) {
    int operation, a, b;
    cin >> operation >> a >> b;
    if (operation == 1) {
      DSU.merge(a, b);
    } else {
      cout << (DSU.connected(a, b) ? "Y" : "T") << '\n';
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

## Materi Yang Berhubungan
    
- [Tutorial DSU](https://cp-algorithms.com/data_structures/disjoint_set_union.html)



## Soal Yang Berhubungan
    
- [D. Secret Passwords](https://codeforces.com/problemset/problem/1263/D)
