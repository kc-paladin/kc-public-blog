# [D. Menutup Tiang](https://tlx.toki.id/courses/competitive/chapters/12/problems/D)

Author: I Nyoman Narayan Kitas Utama

_This Recording is Private. Do Not Disclose This to Anyone Without Permission from The Council._

_Recording Started_

"Selamat siang, ini dengan siapa ya?"

"Halo bang, ini temennya Anon, Unkno. Saya mau minta bantuan."

"Oh, Unkno ternyata. Ada apa bang?"

"Jadi gini, pagi ini **[REDACTED]** datang ke rumah saya untuk meminta bantuan. Bapaknya kan lagi masang beberapa tiang bendera, terus di cat. Tiba tiba, setelah selesai di cat langitnya mendung, padahal catnya belum kering. Jadinya bapaknya mau beli terpal. Tak kira saya disuruh beli terpal, eh ternyata bapaknya cuman nanya panjang minimum terpal yang perlu dibeli."

"Gak nanyak lebar terpalnya?"

"**[REDACTED]** gak peduliin itu. Bapaknya cuman nanyak panjang terpalnya. Untungnya cuman $5$ tiang, jadinya bisa tak hitung pake gambaran kertas."

"Lah, terus apa masalahnya?"

"Gini, karena saya berhasil membantu **[REDACTED]**, bapaknya malah nyuruh 14 **[REDACTED]** buat nelpon saya buat bantuin **Menutup Tiang** (jeng jeng jeng). Mana lagi ada yang mau nutup $100000$ tiang lagi :/"

"Bentar, $100000$?"

"**[EXPUNGED]**"

"Dimengerti. Lalu, bagaimana dengan proyek **[REDACTED]**?"

"**[REDACTED]**"

_Recording Ended_

Nampaknya Unkno lagi dalam masalah. Ayo kita bantu dia! ~~Totally bukan untuk proyek elit yang sangat rahasia~~.

### Solusi (_Convex Hull_, Implementasi _Stack_, dan Cara Mengakali _Floating Point Error_)

Baiklah, ayo kita mulai bantu Anon. Jadi, sebelum kita memulai pengkodean, kita akan mempelajari tentang konsep dari soal ini, yaitu _Convex Hull_. Cara memahami konsep ini adalah dengan menganggap konsep ini sebagai mengelilingi kumpulan peniti dengan tali. Jadi, konsep tersebut bisa divisualisasikan seperti ini:

```
Kita punya N peniti di suatu dinding. Terus, ambil suatu tali dan taruh tali tersebut mengelilingi peniti paling "luar" sehingga saat ujung tali tersebut menemui ujung tali yang lain, semua peniti berada di dalam daerah yang dikelilingi oleh tali tersebut.
```

Kalo masih gak ngerti, pengertian beserta visualisasinya bisa dilihat [di sini](https://en.wikipedia.org/wiki/Convex_hull)

Sekarang, untuk penyelesaiannya, akan digunakan prinsip dari struktur data _stack_ dan gradien.

"Hah, kok malah _stack_?"

Jadi gini. Kan di prinsip _convex hull_ itu terkadang ada beberapa peniti yang tidak kedapetan untuk kena pinggiran talinya. Nah, ini kasusnya sama juga. Kan bisa aja ada tiang yang bukan menjadi penyangga terpalnya. Nah, berarti kan kita perlu cari tiang mana saja yang jadi tiang penyangganya. Untuk itu, maka kita perlu tau prinsip dari pembentukan _convex hull_, yaitu seperti ini:

- Misalkan ada titik $A(x_A,y_A)$, $B(x_B,y_B)$, $C(x_C,y_C)$ dengan $x_A < x_B < x_C$. Jika gradien dari garis yang melalui $BC$ lebih besar daripada gradien dari garis yang melalui $AB$, maka titik $B$ tidak akan dilalui oleh garis _convex hull_ bagian atas itu.

Perhatikan bahwa setiap kali kita membuat _convex hull_ dalam suatu bidang $2$ dimensi, kita mencoba untuk membuat suatu keliling sehingga semua "peniti" berada di dalam keliling tersebut (untuk bagian atas _convex hull_, semua titik berada di bawah keliling). Nah, ini artinya kalau gradien dari garis yang melalui $BC$ lebih besar daripada gradien dari garis yang melalui $AB$, maka _convex hull_ bagian atas itu sama saja seperti menarik tali itu ke dalam (atau bawah) untuk mengenai peniti $B$, yang pastinya akan membuat tali lebih panjang. Padahal, konsep dari _convex hull_ itu sendiri adalah keliling minimal agar semua "peniti" tersebut berada di dalam daerah "tali" tersebut.

Dari sini, bisa disimpulkan bahwa implementasi dari _stack_ untuk soal ini dapat dilakukan sebagai berikut:

- Misalkan ada dua tiang tambahan dengan $X=S+\frac{D}{2}$ dan $H=0$, serta $X=F-\frac{D}{2}$ dan $H=0$. Kita misalkan tiang ini sebagai $t_0=(X_0,H_0)$ dan $t_{N+1}=(X_{N+1},H_{N+1})$. Urutkan semua tiang (termasuk kedua tiang tersebut) menurut posisi dan buat suatu $stack$ yang format anggotanya berisi $pair$ yang mendefinisikan posisi tiang penyangga serta tinggi tiang penyangga tersebut (bisa dibilang koordinat puncak tiang penyangga). Misalkan tiang ke-$i$ dari sebelah kiri adalah $t_i$. Perhatikan bahwa jika kita hanya mengambil kumpulan $i$ tiang berurutan dari posisi paling kiri untuk dipasang terpal, $t_i$ pasti menjadi salah satu tiang penyangga. Untuk $t_{i+1}$, cek apakah gradien puncak $t_{i+1}$ dengan puncak tiang $top$ (dimana $top$ merupakan tiang penyangga paling kanan sementara) lebih besar daripada gradien puncak tiang $top$ dengan puncak tiang penyangga tepat di sebelah kiri tiang $top$. Jika iya, hilangkan tiang $top$ dari anggota tiang penyangga, jadikan tiang penyangga tepat di sebelah kiri tiang $top$ sebelumnya menjadi tiang $top$, dan ulangi. Jika tidak atau hanya tersisa lagi satu tiang penyangga, hentikan dan jadikan $t_{i+1}$ sebagai tiang penyangga.

"Manuk akal!" - Unkno (2023)

Dari proses ini, dapat dipastikan bahwa kita bisa mendapat semua kumpulan tiang yang puncaknya mengenai terpal. Untuk kemudahan diskusi, mulai saat ini anggap tiang yang ada hanyalah kumpulan tiang penyangga tersebut.

Untuk panjang terpal, dapat dilihat bahwa karena ujung terpal tersebut pasti mulai dan berakhir di $H=0$, maka terdapat sebuah tiang dimana terpalnya mengenai seluruh area puncaknya, sehingga diameternya tetap harus dihitung. Selain itu, perhatikan bahwa untuk semua tiang di sebelah kiri tiang tersebut, hanya pojok kiri tiang yang terkena terpal. Untuk semua tiang di sebelah kanan tiang tersebut, hanya pojok kanan tiang yang terkena terpal. Karena diameter setiap tiang itu sama saja, maka panjang terpal penghubung dua tiang berdampingan sama saja dengan _euclidian distance_ dari kedua posisi puncak tiang, yaitu $\sqrt{(\Delta H)^2+(\Delta pos)^2}$ dimana $\Delta H$ adalah perbedaan ketinggian kedua tiang dan $\Delta pos$ adalah jarak antara kedua tiang. Dengan cara ini, perhitungan dapat dilakukan dengan konstan kompleksitas yang lebih kecil. Untuk mengakali _floating point error_, gunakan `std::sqrtl` untuk hasil yang lebih presisi (tapi ganti terlebih dahulu nilai $(\Delta H)^2+(\Delta pos)^2$ menjadi tipe `long double` sebelum dimasukkan ke dalam `std::sqrtl`).

Kompleksitas Waktu: $O(N \log N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Kode (C++ iostream Library)</summary>

```c++
#include <iostream>
#include <iomanip>    // for std::fixed and std::setprecision
#include <algorithm>  // for std::sort
#include <stack>      // for std::stack
#include <utility>    // for std::pair
#include <cmath>      // for std::sqrtl

using namespace std;

typedef long long int ll;
typedef long double ldub;

// untuk menampung data tiang (nanti diurutkan)
pair<ll, ll> tiang[100001];
// untuk menampung data tiang penyangga
stack<pair<ll, ll> > penyangga;

int main() {
  int S, F, N, D;
  // input
  cin >> S >> F >> N >> D;
  for (int i = 0; i < N; i++) cin >> tiang[i].first >> tiang[i].second;
  // solution
  sort(tiang, tiang + N);
  tiang[N] = {F - D / 2, 0};
  // masukkan tiang ke-0 ke dalam stack
  penyangga.push({S + D / 2, 0});
  // masukkan tiang selanjutnya
  penyangga.push(tiang[0]);
  pair<ll, ll> tiangTop;
  // jalankan algoritma stack
  for (int i = 1; i <= N; i++) {
    // tips: untuk menghindari floating point error dalam membandingkan pecahan
    // a/b dan c/d, kita dapat mengakalinya dengan membandingkan a*d dengan b*c.
    // Namun untuk melakukan hal ini, long long int wajib digunakan
    tiangTop = penyangga.top();
    penyangga.pop();
    while (!penyangga.empty() && (tiang[i].second - tiangTop.second) * (tiangTop.first - penyangga.top().first) > (tiangTop.second - penyangga.top().second) * (tiang[i].first - tiangTop.first)) {
      tiangTop = penyangga.top();
      penyangga.pop();
    }
    penyangga.push(tiangTop);
    penyangga.push(tiang[i]);
  }
  ldub terpal = D;
  tiangTop = penyangga.top();
  penyangga.pop();
  while (!penyangga.empty()) {
    terpal += sqrtl((ldub)((tiangTop.first - penyangga.top().first) * (tiangTop.first - penyangga.top().first) + (tiangTop.second - penyangga.top().second) * (tiangTop.second - penyangga.top().second)));
    tiangTop = penyangga.top();
    penyangga.pop();
  }
  cout << fixed << setprecision(3) << terpal << endl;
}
```
</details>

## Komentar
    
- Salah satu kelemahan dari penggunaan `std::stack` adalah satu-satunya elemen yang bisa diakses di dalam kontainer hanyalah elemen paling belakang (atau yang paling atas), sehingga untuk mengetahui gradien antara tiang penyangga $top$ dengan tiang penyangga tepat di sebelah kiri $top$, kita harus "melepas" tiang penyangga $top$ dari $stack$ kemudian membandingkan tiang tersebut dengan tiang penyangga $top$ sekarang setelah $top$ sebelumnya dilepas dari $stack$ (menggunakan `stack::top` untuk mengambil informasi tiang penyangga $top$ kemudian `stack::pop` untuk melepas $top$). Setelah itu, kembalikan $top$ ke dalam $stack$ saat proses eliminasi tiang telah selesai. Hal ini menyebabkan beberapa perubahan di dalam kode, seperti hentikan saat isi $stack$ sudah kosong daripada hentikan saat hanya tersisa satu elemen di dalam $stack$.

- Tipe pengurutan yang digunakan di dalam kode solusi adalah [_intro sort_](https://www.geeksforgeeks.org/introsort-cs-sorting-weapon/) (tipe pengurutan dari `std::sort`) yang mempunyai kompleksitas waktu $O(N \log N)$. Hal ini dikarenakan walaupun batasan yang tertulis di soal adalah $1 \leq N \leq 1000$, terdapat sebuah tes kasus dimana $N=100000$ yang menyebabkan _verdict_ **TLE** (_Time Limit Exceeded_) jika menggunakan algoritma pengurutan $O(N^2)$ (seperti _insertion sort_, _selection sort_, dll) ~~mungkin biar rage quit yang make pengurutan itu karena hampir dapet **AC** awokwkwkwk~~.

- Kompleksitas waktu alternatif dari solusi ini adalah $O(F+N)$ jika pada saat melakukan pengurutan tiang menurut posisi, kita menggunakan tipe pengurutan [_counting sort_](https://www.geeksforgeeks.org/counting-sort/). Hal ini dapat dilakukan dan di bawah batasan waktu karena $X_i < F \leq 250000$ dan $X_i \neq X_j$ untuk $1\leq i < j\leq N$ (batasan ini juga berlaku jika $0\leq i < j\leq N+1$ dimana kita masukkan kedua tiang tambahan tersebut ke dalam kumpulan tiang). Triknya adalah dengan cara membuat sebuah array $T$ dimana $T[k]=H_i$ jika $k=X_i$ untuk suatu indeks $i$ (dapat dipastikan tidak ada dua tiang di posisi yang sama menurut batasan soal) dan $T[k]=0$ jika tidak. Kemudian iterasikan secara menaik dari $0$ sampai $F$ untuk mengurutkan tiang tersebut. Jika $T[k]\neq 0$ untuk suatu $0\leq k\leq F$, masukkan ke dalam array $tiang$ dalam bentuk $(k,T[k])$ dari belakang/atas. Jika tidak, jangan masukkan. Akan tetapi, trik pengurutan ini lebih baiknya digunakan untuk mempercepat hanya jika $N\geq 2\cdot 10^4$ (seperti satu tes kasus di soal dimana $N=100000$) agar optimal untuk setiap nilai $F$.
