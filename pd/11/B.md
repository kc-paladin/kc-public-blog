# [B. Pembuangan String](https://tlx.toki.id/courses/basic/chapters/11/problems/B)

Author: Daniel Simanullang

<!-- Masukkan penjelasan disini -->
Pada soal ini, kita hanya perlu melakukan apa yang soal perintahkan, yaitu membuang setiap kemunculan terkiri string $T$ pada $S$. Kita dapat menggunakan $erase$ yang ada di c++. string::npos pada kode berfungsi untuk mengecek apakah masih ada string $T$ pada $S$.

Kompleksitas Waktu: $O(S.length()^3)$

Kompleksitas Memori: $O(S.length())$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace __gnu_pbds;
using namespace std;

//defines
#define int long long
#define debug(x) cerr << "(" << #x << "=" << x << "," << __LINE__ << ")\n";
#define sz(x) ((int)x.size());
#define all(x) (x).begin(),(x).end();

//constants
const int dx[4]{1, 0, -1, 0}, dy[4]{0, 1, 0, -1}; 
const char dir[4]{'D','R','U','L'};
const int mod=1e9+7;
const int maxn=2e5+5;
const double eps=1e-9;

//typedefs
typedef vector<vector<int>> vii;
typedef vector<int> vi;
typedef pair<int,int> pii;

//Template
template<class T> using oset=tree<T, null_type, less<T>, rb_tree_tag,tree_order_statistics_node_update>;

//Mods
int mul(int a,int b,int MOD)
{
    return ((a%MOD)*(b%MOD))%MOD;
}
int add(int a,int b,int MOD)
{
    return (a+b)%MOD;
}
int sub(int a,int b,int MOD)
{
    return (MOD+a-b)%MOD;
}


signed main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    string a,b;
    cin >> a >> b;
    int n=a.size(),m=b.size();
    while(a.find(b)!=string::npos)
    {
        a.erase(a.find(b),m);
    }
    cout << a << '\n';
    
    return 0;
}
```
</details>


## Komentar
    
- erase($find$,$length$) = cari posisi string yang dicari 
dan hapus sepanjang $length$.

## Materi Yang Berhubungan
    
- [Dokumentasi fungsi $erase$](https://cplusplus.com/reference/string/string/erase/)


<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal I](link-soal)
- [Nama Soal II](link-soal)

-->