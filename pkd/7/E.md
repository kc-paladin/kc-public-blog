# [E. Perkalian Matriks Bebek](https://tlx.toki.id/courses/competitive/chapters/07/problems/E)

Author: Ackhava Adam Malonda

Halo _guys_! Bagaimana perjalanan kalian mengerjakan _course_ di TLX? Kali ini kita akan lihat soal E dari bab 7 _course_ Pemprograman *Kompetitif* Dasar.

Soal ini bertema perkalian matriks, dan memang soal ini sepertinya bisa diperjelas lagi tentang beberapa sifat matriks yang bakalan kita butuh buat kerjain soalnya (meski bisa dicari juga).

Oke, mari kita mulai dengan definisi. Matriks adalah analog matematis dari _array_ 2-dimensi (_two-dimensional_ atau _2D_). Namun, matriks dikhususkan untuk angka, sehingga memiliki beberapa tambahan yang tidak dimiliki _array_ biasa di pemprograman. Tetapi, untuk soal ini isi matriksnya, ataupun algoritma untuk operasi-operasi yang ada, tidak berpengaruh.

Perkalian matriks adalah perbedaan yang paling signifikan untuk soal ini. Sebelum bisa membahas topik ini secara lebih formal (untuk menjadi solusi akhir), kita perlu sepakat dengan ukuran matriks. Pada kali ini, ukuran matriks yang dilambangkan $x$ akan ditulis dengan $R_x \times C_x$, dimana $R_x$ adalah jumlah baris dan $C_x$ adalah jumlah kolom (kita perlu beberapa matriks saat perkalian, sehingga perlu dibedakan).

Setelah itu, kita akan coba kalikan matriks $A$ dengan matriks $B$. Seperti di soal, perkalian hanya bisa dilakukan jika $C_A = R_B$. Perkalian ini akan menghasilkan matriks akhir berukuran $R_A \times C_B$. 

Perkalian ini memiliki sifat asosiatif juga, yaitu sifat dimana semua pengurutan operasi (tanda kurung) yang mungkin dan valid akan menghasilkan hasil yang sama. Contohnya, $(A \times B) \times C = A \times (B \times C)$ untuk tiga matriks sembarang $A, B, C$. Hal inilah yang memungkinkan para gajah untuk melakukan perkalin dengan cara yang efisien.

Pada soal, perkalian matriks $A$ dan $B$ membutuhkan $R_A \times R_B \times C_B$. 

Sebelum lanjut ke solusi lengkapnya, kita perhatikan bahwa cara masukan diberikan menjamin perkalian dapat dilakukan. Kita akan anggap masukan yang diberikan pada baris kedua adalah $D$ (_Dimensi_). 

Maka, dari definisi soal matriks ke-$x$ berukuran $D_x \times D_{x+1}$. 

Perhatikan bahwa ada tiga kemungkinan pertanyaan, meskipun $Q = 1$ dan $Q = 2$ memiliki DP yang sama. 

$Q = 3$ adalah yang paling mudah, dimana kita tidak perlu memikirkan ukuran matriks dan hanya jumlah matriks yang dikalikan. Anggap jawaban untuk $N$ matriks adalah $E(N)$. Maka, kita bisa pecah di bagian manapun yang kita inginkan. Kita akan pilih posisi perkalian terakhir yang dilakukan - anggap $i$ ($1 \leq i \leq N-1$) matriks dari kiri. 

Untuk bagian kiri kita memiliki $E(i)$ cara, dan ada $E(N-i)$ cara untuk bagian kanan. Alhasil, ada $E(i) \times E(N-i)$ cara untuk mendapatkan hasil matriks (tidak harus optimal). 

Saat dijumlah, $E(N) = E(1) \times E(N-1) + E(2) \times E(N-2) + \dots + (N-1) \times E(1)$. Ini bisa kita memoisasi dengan mudah sehingga menjadi DP. _Base case_ yang ada adalah $E(1) = 1$ dan $E(0) = 0$ (dengan cara perhitungan di atas, $E(0)$ tidak akan dipanggil, dan jika terpanggil maka terdapat _infinite recursion_ yang akan membuat _runtime error_ atau **RTE**).

Untuk $Q = 1$, kita akan definisikan sebuah fungsi $f(1, N)$ sebagai jawaban. Definisi $f(x, y)$ adalah banyak cara **optimal** untuk mengalikan matriks $x$ sampai $y$, inklusif. Kita bisa pecah menjadi kiri dan kanan, dengan $pos$ sebagai matriks terakhir yang masuk kedalam bagian kiri ($x \leq pos \lt y$). Maka butuh $f(x, pos) + f(pos + 1, y)$ operasi untuk mengalikan kedua sisi secara terpisah, dan $D_x \times D_{pos+1} \times D_{y+1}$ untuk mengalikan kedua belahan. Kita bisa minimalkan $f(x, pos) + f(pos + 1, y) + D_x \times D_{pos+1} \times D_{y+1}$ untuk semua $pos$ yang valid untuk mendapat:
$f(x, y) = min(f(x, pos) + f(pos + 1, y) + D_x \times D_{pos+1} \times D_{y+1}, x \leq pos \lt y)$

_Base case_ yang ada adalah $f(x, x) = 0$ ($y<x$ tidak mungkin).

Untuk $Q = 2$, hal yang sama dapat dilakukan, tetapi dengan membuat _array_ untuk menyimpan jumlah cara. Saat awal kita akan memeriksa semua $pos$, sehingga awalnya jawaban tak terhingga (bilangan besar) dan ada nol cara. Lalu, jika $pos$ saat ini lebih baik dari sebelumnya (lebih sedikit langkah), kita buat ini jawabannya dan banyaknya cara adalah perkalian banyaknya cara dari $f(x, pos)$ dan $f(pos+1, y)$. Jika solusi ini sama baiknya (jumlah langkah sama persis), kita hitung banyak cara yang mungkin dan tambahkan kedalam banyak cara sekarang. Jika solusi ini lebih buruk (lebih banyak langkah), ya kita abaikan saja. 

<details>
  <summary>Solution Code</summary>

```
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;  // long long adalah tipe data 64-bit di C++ - diperlukan
                       // untuk mencegah overflow

const ll MOD = 26101991;  // Modulo untuk soal 2

ll p[500];  // p adalah D di pembahasan
ll N;
ll Q;

namespace task12 {  // Pertanyaan 1 dan 2
ll memo[500][500];  // Memoisasi
ll cnt[500][500];   // Jumlah cara

ll dp(ll l, ll r) {  // dp adalah f di pembahasan
  if (l == r) {
    cnt[l][r] = 1;
    return 0;
  }

  ll &ans = memo[l][r];
  if (ans != -1) return ans;

  ans = 1E16;

  for (ll i = l; i < r; i++) {  // Iterasi (i adalah pos di pembahasan)
    ll c = p[l] * p[i + 1] * p[r + 1];
    c += dp(l, i) + dp(i + 1, r);

    if (ans > c) {  // Lebih baik
      cnt[l][r] = cnt[l][i] * cnt[i + 1][r];
      cnt[l][r] %= MOD;
      ans = c;
    } else if (ans == c) {  // Sama saja
      cnt[l][r] += cnt[l][i] * cnt[i + 1][r];
      cnt[l][r] %= MOD;
    }
    // Lebih buruk maka tidak akan dilihat :(
  }

  return ans;
}

void init() {
  memset(memo, -1, sizeof memo);
  memset(cnt, 0, sizeof cnt);
}
}

namespace task3 {  // Pertanyaan 3
ll memo[500];

ll dp(ll n) {  // dp adalah E di pembahasan
  if (n == 0) return 0;
  if (n == 1) return 1;

  ll &ans = memo[n];
  if (ans != -1) return ans;

  ans = 0;

  for (ll i = 1; i < n; i++) {  // Iterasi (i adalah pos di pembahasan)
    ans += dp(i) * dp(n - i);
    ans %= MOD;
  }

  return ans;
}

void init() { memset(memo, -1, sizeof memo); }
}

int main() {
  ios_base::sync_with_stdio(false);
  cin.tie(0);
  cout.tie(0);

  cin >> N;

  for (ll i = 1; i <= N + 1; i++) {
    cin >> p[i];
  }

  cin >> Q;

  if (Q == 1) {
    task12::init();
    cout << task12::dp(1, N);
  } else if (Q == 2) {
    task12::init();
    task12::dp(1, N);
    cout << task12::cnt[1][N];
  } else {
    task3::init();
    cout << task3::dp(N);
  }
}
```
</details>

## Komentar
- Tipe data `long long` digunakan pada implementasi. Tipe data ini adalah tipe data 64-bit yang dibutuhkan untuk mencegah _overflow_.
- Pada implementasi, _namespace_ digunakan untuk memisahkan kedua DP dan mencegah kebingungan.

## Materi Yang Berhubungan
- [Buku Pemprograman Kompetitif Dasar](https://osn.toki.id/arsip/download-pkd) (bab 7)
- [Perkalian Matriks](https://byjus.com/maths/matrix-multiplication/)
- [_Finite recursion_ dan _ininite recursion_](https://www.geeksforgeeks.org/finite-and-infinite-recursion-with-examples/)  
  * Berhubungan dengan [_Overflow_ (_Stack overflow_ secara spesifik)](https://www.geeksforgeeks.org/heap-overflow-stack-overflow/). Ini alasan program akan mendapat _runtime error_ (**RTE**) jika terjadi _infinite recursion_
- [_Namespace_ di C++ (cukup mendalam tentang aturan formal dari _namespace_ - mungkin dapat dibaca sekilas saja)](https://www.geeksforgeeks.org/namespace-in-c/)
- [Tipe data di C++ (lengkapnya di bagian "C++ Modified Data Types List" - tabel di awal lebih singkat)](https://www.programiz.com/cpp-programming/data-types)