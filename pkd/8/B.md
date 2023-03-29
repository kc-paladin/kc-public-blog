# [B. Modified Queue](https://tlx.toki.id/courses/competitive/chapters/08/problems/B)

Author: I Nyoman Narayan Kitas Utama

Kali ini, kita akan membahas tentang soal kedua di struktur data dasar, yaitu Modified Queue. Eits, tapi sebelum kita mulai analisa soal ini, ayo kita jawab beberapa pertanyaan dari Anon.

Q: "Queue itu emangnya apa sih?"

A: "Singkatnya, struktur data Queue itu adalah array dinamis yang bersifat FIFO (_First In First Out_). Artinya, setiap kali kita memasukkan atau _push_ suatu data ke dalam Queue, data tersebut akan ditaruh di belakang array (atau barisan karena ini merupakan konsep dari Queue) dan setiap kali kita mengeluarkan atau _pop_ suatu data dari Queue, data yang berada di paling depan Queue tersebut akan hilang dari Queue."

Q: "Jadi memang kayak barisan gitu ya?"

A: "Bahasa Indonesia dari Queue aja itu antrean. Tapi kan kalo namanya kita ubah jadi Antrean kan nggak kedengeran keren jadinya :)))"

Q: "Kalo gitu kenapa nama soal ini Modified Queue?"

A: "Itu karena kita bukan _push_ atau _pop_ data sebuah elemen per perintah seperti biasa, tetapi kita _push_ elemen ke dalam Queue dengan nilai $X$ sebanyak $Y$ kali (dengan _syntax_ `add X Y`) atau kita _pop_ elemen dari Queue sebanyak $Y$ kali (dengan _syntax_ `del Y`). ~~Emang sih sementara gak ada perubahan banyak~~. Tapi, yang membuat soal ini spesial adalah _syntax_ `rev` yang membalikkan urutan data di dalam Queue. Perintah atau _syntax_ ini mirip sama soal [B. Balik Daftar](https://tlx.toki.id/courses/basic/chapters/09/problems/B) tapi bisa dilakukan berulang kali."

Q: "Waduh, kenapa Pak Dengklek malah nanya ke saya? Kenapa gak dikerjain sendiri aja?"

A: "Kan katanya mau ikut pemrograman kompetitif, jadinya Pak Dengklek nyuruh Anon karena Pak Dengklek ~~lagi males kerjain sendiri~~ pingin Anon biar bisa pinter di pemrograman kompetitif."

Q: "Tolong saya :')"

A: "Oke!"

Nah, sekarang karena semua pertanyaan sudah dijawab, waktunya kita tackle soal ini.

Kalo misalnya kita coba cara manual (alias brute force), kita dapat kompleksitas waktu $O(Y)$ setiap kali kita manggil `add` atau `del`. Jika semua _syntax_ adalah `add` atau `del`, maka kompleksitas waktunya adalah $O(NY)$, yang masih memenuhi soal karena $N\cdot Y\leq10^3\cdot10^4=10^7 < 10^8$ yang berarti algoritma brute force ini dapat dieksekusi kurang dari $1$ detik. Tetapi, bagaimana kalau ada _syntax_ `rev`? Dengan cara membalikkan Queue secara manual, kompleksitas waktunya adalah $O(K)$ per pemanggilan, dimana $K$ itu adalah banyak elemen dari Queue tersebut. Pemanggilan `rev` berkali kali akan membuat algoritma kita **TLE** (_Time Limit Exceeded_) jika Queue mempunyai banyak elemen yang sangat besar. Salah satu contohnya adalah pemanggilan `add X 10000` sebanyak 900 kali dan `rev` sebanyak 100 kali. Pada skenario terburuk, banyak operasi yang perlu dilakukan dengan algoritma brute force ini adalah $10000\cdot900\cdot(100+1) > 2\cdot10^8$, yang pasti akan membuat kode **TLE**. Jadi, ada 2 cara untuk optimisasi algoritma ini.

<br />

### Solusi A (_Dynamic Array_ dan Manipulasi `std::pair`)

Solusi pertama yang dapat dilakukan adalah dengan penggunaan salah satu tipe _dynamic array_ yaitu `std::deque`. Tipe array dinamis ini mirip dengan `std::vector`, namun keuntungan dari penggunaan `std::deque` adalah kita dapat _push_ atau _pop_ data ke dalam atau dari deque ini dari depan juga (dengan fungsi `push_front()` dan `pop_front()`), tidak seperti vector yang hanya bisa _push_ dari belakang dan _pop_ elemen paling belakang. Implementasi `std::deque` itu sangatlah mirip dengan `std::vector`, dan bisa dilihat seperti di bawah ini.

```c++
std::deque<int> barisan={3,2,1,5};
barisan.push_front(4);
// barisan={4,3,2,1,5}
barisan.pop_front();
// barisan={3,2,1,5}
barisan.pop_back();
// barisan={3,2,1}
barisan.push_back(4);
// barisan={3,2,1,4}
```

"Bentar, tapi kan ini cuman biar mudah aja melakukan _syntax_ `add` sama `del`, bukannya mengoptimisasi kompleksitas waktu."

Nah, sekarang kita akan melakukan optimisasi _syntax_ `add` dengan menggunakan `std::pair`. Tipe data _pair_ ini merupakan tipe data yang menyimpan dua tipe data lain sekaligus, bahkan dirinya sendiri! Tipe data ini biasanya digunakan untuk menyimpan data yang berupa pasangan. Contohnya adalah bila kita ingin menyimpan pasangan seperti `{6,9}` atau `{"rating",6.9}`, kita dapat mengimplementasikannya seperti kode di bawah ini:

```c++
std::pair<int,int> pasangan1={6,9};
std::pair<std::string,float> pasangan2={"rating",6.9};
std::cout << pasangan1.first << " " << pasangan1.second << std::endl;
// keluaran: 6 9
```

Dari kode di atas, bisa dilihat bahwa kita dapat menggunakan _keyword_ `first` dan `second` untuk akses anggota pertama dan kedua dari pasangan tersebut. ~~Bagaimana dengan pasangan anda?~~

Kembali ke soal. Perhatikan bahwa setiap kali kita melakukan input `add X Y`, kita sebenarnya hanya menambah sebuah grup berisi $Y$ bilangan $X$ ke dalam barisan, sehingga kita hanya perlu memasukkan `{X,Y}` ke dalam barisan. Formalnya, setiap kali `add X Y` dipanggil, kita akan melakukan `push_back({X,Y})` untuk _maintain_ bentuk barisan awal namun dengan waktu dan memori $O(1)$ per masukan. Untuk operasi `del Y`, kita bisa kurangi nilai $Y$ dengan `barisan.front().second` terus lakukan `pop_front()` pada barisan sampai nilai $Y$ kurang dari `barisan.front().second`, lalu kita kurangkan `barisan.front().second` dengan $Y$. Dengan kata lain, hapus grup paling depan jika sisa banyak penghapusan masih tidak kurang dari ukuran grup yang akan dihapus, dan hapus sebagian isi grup tersebut jika sudah kurang dari ukuran grup yang akan dihapus.

"Tapi kan banyak anggota dari barisan itu cuman banyaknya kita melakukan `add X Y`, bukan ukuran dari barisan itu. Mana lagi, setiap kali panggil `add X Y`, harus keluarin banyak anggota barisan" - Anon, baru aja dapet _verdict_ **WA** (_Wrong Answer_) gara-gara itu (makanya jangan submit dulu masbro)

Cara untuk mencegah hal ini adalah dengan menambahkan variabel baru namanya $sz$. Variabel ini dinamakan begini sebagai singkatan dari _size_ atau ukuran. Atur nilai dari $sz$ ke $0$ terlebih dahulu. Setiap kali perintah `add X Y` dipanggil, tambah nilai $sz$ dengan $Y$, kemudian output nilai dari $sz$. Dan setiap kali perintah `del Y` dipanggil, kurangi nilai $sz$ dengan $Y$. Eits, tapi kalau $sz < Y$, kita harus atur nilai $sz$ menjadi $0$. (Bayangkan kalo array ukuran negatif :0).

Untuk perintah `rev`, gunakan `std::reverse()` untuk mempercepat proses pembalikan barisan.

Definisikan $K$ sebagai ukuran dari _deque_ `barisan`

Kompleksitas Waktu:

- $O(1)$ setiap pemanggilan `add X Y`
- $O(\min(Y,sz))$ setiap pemanggilan `del Y`
- $O(K)$ setiap pemanggilan `rev`

Kompleksitas Memori: $O(\min(K,N))$

<details>
  <summary>Kode (C++ iostream Library)</summary>

```c++
#include <iostream>
#include <deque>      // std::deque
#include <algorithm>  // std::reverse
#include <utility>    // std::pair
#include <string>     // std::string

using namespace std;

deque<pair<int, int> > barisan;
int sz = 0;

void add(int x, int y) {
  barisan.push_back({x, y});
  sz += y;
}

void del(int y) {
  sz = max(0, sz - y);
  if (barisan.empty()) {
    return;
  }
  while (y >= barisan.front().second) {
    y -= barisan.front().second;
    barisan.pop_front();
    if (barisan.empty()) {
      return;
    }
  }
  barisan.front().second -= y;
}

void rev() { reverse(barisan.begin(), barisan.end()); }

int main() {
  int N, X, Y;
  string s;
  cin >> N;
  while (N--) {
    cin >> s;
    if (s == "add") {
      cin >> X >> Y;
      add(X, Y);
      cout << sz << endl;
    } else if (s == "del") {
      cin >> Y;
      // akses elemen paling depan
      cout << barisan.front().first << endl;
      if (sz != 0) {
        del(Y);
      }
    } else if (s == "rev") {
      rev();
    }
  }
  return 0;
}
```
</details>

<br />

### Solusi B (_Static Array_, Manipulasi `rev`, dan Pencarian _Two Pointers_) (Ft. _Binary Search_)

"Lah, masih ada ya?"

Sebenernya sih nggak, tapi terkadang dengan batasan yang diberikan, kita bisa melakukan beberapa hal yang lebih kreatif dengan soal tersebut. Solusi ini patut dipelajari kalo misalnya kalian pakai bahasa C, bahasa yang ~~inferior~~ lebih susah, namun lebih cepat dalam hal eksekusi program, karena solusi ini tidak akan menggunakan _resources_ dari _Standard Template Library_ yang hanya tersedia di C++. Dan juga solusi ini dibuat untuk mengoptimisasi solusi A dari setiap perintah yang ada dalam segi waktu (kecuali perintah `add` karena paling rendah memang hanya memerlukan waktu $O(1)$). Tentu saja kompleksitas memorinya akan menjadi jauh lebih besar, namun biasanya _Time Limit_ lah yang harus lebih diperhatikan dibanding _Memory Limit_.

Manipulasi `rev` yang dimaksud di sini adalah daripada kita anggap perintah ini sebagai membalikkan array dengan kompleksitas $O(K)$, kita anggap `rev` sebagai pembalik kondisi `isReversed`. Jika `isReversed = false`, maka `rev` akan mengubahnya menjadi `true` dan jika `isReversed = true`, maka `rev` akan mengubahnya menjadi `false`, yang hanya memerlukan waktu $O(1)$.

Jadi, prinsip dari solusi ini adalah dengan menggunakan array dengan ukuran yang sudah ditentukan serta penggunaan dua titik (_two pointers_) untuk menentukan range di dalam array yang merupakan queue yang kita buat. Jadi, pertama kita akan buat tipe data baru dengan nama `kelompok` yang isinya adalah `nilai, indeks paling kiri, indeks paling kanan`. Cara pembuatannya adalah dengan menggunakan `typedef struct` seperti di bawah ini:

```c++
typedef struct kelompok {
  int nilai;
  int indexl;
  int indexr;
} kelompok;
```

"Kok keliatan kompleks yah? :("

Tenang, semua hal ini akan dijelaskan kok, ~~Yang sabar ya bos~~. Sekarang, kita akan inisialisasi array dengan ukuran $2N$ dan _two pointers_, yaitu $L$ dan $R$. Atur $L=N$ dan $R=N-1$. Sekarang, setiap kali kita memanggil `add X Y`, lakukan hal berikut ini:

- Jika $L > R$ dan `isReversed = false`, tambahkan nilai $R$ dengan $1$, kemudian ubah nilai $barisan[R]$ menjadi $\{X,10000N+1,10000N+Y+1\}$ (dengan kata lain, $nilai=X,indexl=10000N+1,indexr=10000N+Y+1$) karena $Y\leq10000$.
- Jika $L > R$ dan `isReversed = true`, kurangkan nilai $L$ dengan $1$, kemudian ubah nilai $barisan[L]$ menjadi $\{X,10000N+1,10000N+Y+1\}$ (dengan kata lain, $nilai=X,indexl=10000N+1,indexr=10000N+Y+1$) karena $Y\leq10000$.
- Jika $L\leq R$ dan `isReversed = false`, tambahkan nilai $R$ dengan $1$, kemudian ubah nilai $barisan[R]$ menjadi $\{X,barisan[R-1].indexr+1,barisan[R-1].indexr+Y\}$.
- Jika $L\leq R$ dan `isReversed = true`, kurangkan nilai $L$ dengan $1$, kemudian ubah nilai $barisan[L]$ menjadi $\{X, barisan[L+1].indexl-Y,barisan[L+1].indexl-1\}$.

"di luar nalar coy!!11!!!1!!11!" - Anon, lagi pusing baca apapun lah yang ada di atas ini

Kayak gini maksudnya. Anggap kita punya sebuah array dengan ukuran $2N\cdot Y_{MAX}$, cukup untuk $N$ operasi `add X Y`. Perhatikan bahwa untuk masukan `add X Y` pertama, kita bisa saja langsung taruh kelompok tersebut di tengah-tengah array dengan informasi tentang letak paling kiri dan paling kanan kelompok atau segmen itu. Kemudian setiap kali `add X Y` dipanggil, kita bisa tambahkan kelompok atau segmen tersebut di sebelah kanan elemen paling kanan atau di sebelah kiri elemen paling kiri jika `isReversed`. Karena kelompok ini pasti punya anggota yang sama (ya kan `add X Y` itu sama aja kayak tambahin kelompok isi bilangan $X$ doang), maka kita bisa hanya mencatat pojok kiri dan kanan kelompok tersebut, kemudian data ini disimpan di dalam array yang lebih pendek.

"Ok menarik, tapi kalo `del Y` itu gimana? Bukannya nanti sama aja ya kayak solusi A prosesnya ;-;"

Untuk mempercepat solusi, kita bisa pakai konsep _binary search_. Kita anggap `isReversed` itu `false` terlebih dahulu. Perhatikan bahwa arti dari `del Y` itu sendiri adalah menghapus bilangan dari indeks paling kiri ke indeks paling kiri $+Y-1$. Berarti, secara formalnya, bilangan dari $barisan[L].indexl$ sampai $barisan[L].indexl+Y-1$ akan dihapus. Dari sini, kita hanya perlu mencari letak indeks di array utama yang dimana di dalam intervalnya berisi letak $barisan[L].indexl+Y$ dengan _binary search_. Untuk implementasi _binary search_ yang dimaksud, bisa dilihat di kode di bawah ini:

```c++
int l = L;
int r = R;
int mid;
while (l < r) {
  mid = (l + r) / 2;
  if (barisan[L].indexl + Y < barisan[mid].indexl) {
    r = mid;
  } else if (barisan[L].indexl + Y >= barisan[mid + 1].indexl) {
    l = mid + 1;
  } else {
    break;
  }
}
mid = (l + r) / 2;
// atur titik paling kiri dari array
barisan[mid].indexl = barisan[L].indexl + Y;
L = mid;
// reset array utama jika queue kosong
if (barisan[mid].indexl > barisan[mid].indexr) {
  L++;
}
```

Jika `isReversed` adalah `true`, maka kita akan pakai _binary search_ untuk mencari letak $barisan[R].indexr-Y$ dari semua $indexr$ yang ada, kemudian nilai $R$ dan $barisan[mid].indexr$ akan diatur berdasarkan hasil dari binary search itu.

Kompleksitas Waktu:

- $O(1)$ setiap pemanggilan `add X Y`
- $O(\log(R-L))$ setiap pemanggilan `del Y`
- $O(1)$ setiap pemanggilan `rev`

Kompleksitas Memori: $O(N)$

<details>
  <summary>Kode (C++ stdio.h Library or Standard C Library)</summary>

```c++
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

int L = 1001, R = 1000, sz = 0;
bool isReversed = false;

typedef struct kelompok {
  int nilai;
  int indexl;
  int indexr;
} kelompok;

kelompok barisan[2002];

void add(int x, int y) {
  sz += y;
  if (!isReversed) {
    if (L > R) {
      R++;
      barisan[R].nilai = x;
      barisan[R].indexl = 10000001;
      barisan[R].indexr = 10000000 + y;
    } else {
      R++;
      barisan[R].nilai = x;
      barisan[R].indexl = barisan[R - 1].indexr + 1;
      barisan[R].indexr = barisan[R - 1].indexr + y;
    }
  } else {
    if (L > R) {
      L--;
      barisan[L].nilai = x;
      barisan[L].indexl = 10000000 - y;
      barisan[L].indexr = 9999999;
    } else {
      L--;
      barisan[L].nilai = x;
      barisan[L].indexl = barisan[L + 1].indexl - y;
      barisan[L].indexr = barisan[L + 1].indexl - 1;
    }
  }
}

void del(int y) {
  int l = L;
  int r = R;
  int mid;
  sz -= y;
  if (!isReversed) {
    while (l < r) {
      mid = (l + r) / 2;
      if (barisan[L].indexl + y < barisan[mid].indexl) {
        r = mid;
      } else if (barisan[L].indexl + y >= barisan[mid + 1].indexl) {
        l = mid + 1;
      } else {
        break;
      }
    }
    mid = (l + r) / 2;
    barisan[mid].indexl = barisan[L].indexl + y;
    L = mid;
    if (barisan[mid].indexl > barisan[mid].indexr) {
      L++;
    }
  } else {
    while (l < r) {
      mid = (l + r + 1) / 2;
      if (barisan[R].indexr - y <= barisan[mid - 1].indexr) {
        r = mid - 1;
      } else if (barisan[R].indexr - y > barisan[mid].indexr) {
        l = mid;
      } else {
        break;
      }
    }
    mid = (l + r + 1) / 2;
    barisan[mid].indexr = barisan[R].indexr - y;
    R = mid;
    if (barisan[mid].indexl > barisan[mid].indexr) {
      R--;
    }
  }
}

int main() {
  int N, X, Y;
  char syn[4];
  scanf("%d", &N);
  while (N--) {
    scanf("%s", syn);
    if (!strcmp(syn, "add")) {
      scanf("%d %d", &X, &Y);
      add(X, Y);
      printf("%d\n", sz);
    } else if (!strcmp(syn, "del")) {
      scanf("%d", &Y);
      if (!isReversed) {
        printf("%d\n", barisan[L].nilai);
      } else {
        printf("%d\n", barisan[R].nilai);
      }
      del(Y);
    } else if (!strcmp(syn, "rev")) {
      if (!isReversed) {
        isReversed = true;
      } else {
        isReversed = false;
      }
    }
  }
  return 0;
}
```
</details>

<br />

## Komentar
    
- Untuk solusi A, sebenarnya optimisasi dengan `std::pair` tidak terlalu diperlukan, hanya perlu optimisasi dengan `std::reverse` karena _Time Limit_ yang diberikan. Namun, hal ini agak beresiko dalam menjawab tipe soal seperti ini namun dengan batasan $N$ dan $Y$ yang lebih tinggi.
- Kompleksitas waktu perintah `rev` di solusi A dapat dioptimisasi lagi menjadi $O(1)$ (hint: coba analisis manipulasi `rev` di solusi B)
- Untuk solusi B, optimisasi yang datang dari solusi ini sebenarnya tidak diperlukan karena batasan $N$ yang kecil (yahaha gak sengaja tak overkill help ._.). Akan tetapi, ada baiknya untuk mengembangkan intuisi optimisasi yang kreatif, karena banyak sekali soal pemmrograman kompetitif yang mempunyai batasan yang hampir membuat soal itu tidak mungkin diselesaikan, kecuali dengan trik trik yang unik dan kreatid yang bisa diterapkan. (pastinya di luar nalar coy)

<br />

## Materi Yang Berhubungan
    
- [Pencarian: _Two Pointers_ (English)](https://www.geeksforgeeks.org/two-pointers-technique/)

<br />

## Soal Yang Berhubungan
    
- [TROC #21: B. Ada Beruang (_Two Pointers_)](https://tlx.toki.id/problems/troc-21/B)
