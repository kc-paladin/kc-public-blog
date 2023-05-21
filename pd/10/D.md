# [D. Faktorisasi Prima](https://tlx.toki.id/courses/basic/chapters/10/problems/D)

Author: I Nyoman Narayan Kitas Utama

Ini adalah soal pengkodean ketiga di bab ke 10 pemrograman dasar yaitu [10. Subprogram](https://tlx.toki.id/courses/basic/chapters/10/lessons/A). Sangat disarankan untuk menguasai materi tentang faktorisasi prima (ya kan nama soalnya aja itu :p) untuk memahami editorial yang akan diberikan.

Kalo masih belum ngerti tentang subprogram, _in a nutshell_ subprogram itu cara nyingkat suatu proses kalo proses ini mau dipanggil berulang kali (ato kalo misalnya lagi males ngetik awokwkwkwk). Nah, di editorial ini, akan diberikan 2 solusi yang akan menggunakan subprogram dalam implementasinya.

**Solusi A**. Perhatikan bahwa kita bisa ambil setiap prima dibawah $N$ kemudian cek satu per satu apakah prima tersebut habis membagi $N$. Kemudian, setelah kita bagi $N$ dengan prima tersebut, masukkan ke dalam faktorisasi prima, kemudian cek kembali apakah hasil baginya masih habis dibagi sama bilangan prima tersebut. Jika tidak, kita ganti primanya. Jika masih, ulangi langkah di atas sampai tidak habis dibagi. Formalnya, kita bisa mencari faktorisasi prima $N$ dengan cara mengecek setiap prima $p\leq N$ kemudian menentukan nilai $a$ maksimum agar $p^a$ habis membagi $N$.

"Berarti kita cuman perlu pake for loop dari 2 sampe N, cek prima per bilangan, terus cari $a$ untuk setiap bilangan prima $p$ aja yah?" - Kata terakhir dari Anon sebelum kirim kode terus kena **TLE** (yahaha langsung kena mental)

Disini, untuk mengecek apakah suatu bilangan $i$ itu prima memerlukan kompleksitas waktu paling rendah $O(\sqrt{i})$ untuk batasan $i\leq N\leq10^6$. Sehingga, jika kita melakukan cek prima satu per satu dari $2$ sampai $N$, maka kompleksitas waktunya adalah $O(N\sqrt{N})$, yang akan memberikan _verdict_ **TLE** (_Time Limit Exceeded_) untuk $N>3\times 10^5$.

Trik yang dapat dilakukan adalah dengan cara mengecek apakah $i$ membagi $N$ untuk setiap $i\leq N$, kemudian cek prima jika ternyata $i$ habis membagi $N$. Jika ternyata prima, maka kita bisa mulai mencari nilai dari $a$ untuk nilai $p=i$ tersebut.

Untuk mempermudah penulisan kode, kita akan menulis subprogram bernama `pangkatTerbesar(i,N)` dengan metode _pass by value_ setiap kali $i$ muncul sebagai prima yang habis membagi $N$ dan `cekPrima(i)` untuk mengecek apakah $i$ itu prima.

<details>
    <summary>Kode Untuk Solusi A (C++ iostream library)</summary>

```c++
#include <iostream>
#include <cmath>

using namespace std;

bool cekPrima(int k) {
  for (int i = 2; i <= sqrt(k + 1); i++) {
    if (k % i == 0) {
      return false;
    }
  }
  return true;
}

int pangkatTerbesar(long long k, long long n) {
  int a = 0;
  long long p = k;
  while (n % p == 0) {
    a++;
    p *= k;
  }
  return a;
}

int main() {
  int N, a;
  cin >> N;
  bool pertama = true;
  for (int i = 2; i <= N; i++) {
    if (N % i == 0) {
      if (cekPrima(i)) {
        a = pangkatTerbesar(i, N);
        // mengkondisikan output
        if (pertama) {
          pertama = false;
        } else {
          cout << " x ";
        }
        cout << i;
        if (a > 1) {
          cout << "^" << a;
        }
      }
    }
  }
  cout << endl;
}
```
</details>
    
Kompleksitas Waktu Solusi A: $O(N)$

Kompleksitas Memori Solusi A: $O(\sigma_0(N)\sqrt{N}+K)$ dimana $\sigma_0(N)$ adalah banyak faktor berbeda dari $N$ dan $K$ sebagai banyaknya faktor prima dari $N$

**Solusi B (Optimisasi lebih jauh)**. Solusi yang satu ini akan menggunakan konsep pembuatan pohon faktor. Masih inget kan pohon faktor itu bagaimana? Bagi yang belum pernah belajar tentang ini (atau lupa :p), silahkan klik [di sini](https://www.zenius.net/blog/kpk-fpb-dengan-pohon-faktor) (ya emang sih itu link untuk cari KPK dan FPB tapi cara pembuatan pohonnya ada di sana kok). Singkatnya, kita cari faktor prima terkecil $N$, simpan prima tersebut, bagi $N$ dengan prima tersebut, dan terus lakukan ini sampai ketemu semua prima pembentuk $N$.

"Kalo dalam pengkodean itu kayak gimana nulisnya?"

Untuk optimisasi pengkodean solusi A, kita akan menggunakan lemma di bawah ini.

**Lemma**. Untuk setiap bilangan asli $N>1$, pembagi bulat terkecil $N$ yang lebih dari $1$ pasti merupakan suatu bilangan prima.

**Bukti**. Andaikan pembagi bulat terkecil tersebut bukanlah suatu bilangan prima. Misalkan pembagi ini adalah $B$. Maka, $B$ pasti habis dibagi suatu $P$ dimana $P$ merupakan bilangan prima. Ini berarti $P$ juga habis membagi $N$, padahal $P < B$. Jadi, pembagi bulat terkecil $N$ adalah suatu bilangan prima.

"Kok malah belajar pembuktian matematika? :/"

Terkadang kita harus mengetahui dan menggunakan beberapa trik matematika dan logika untuk optimisasi kode lebih jauh dan lebih mudah. Kita akan menggunakan lemma tersebut untuk mengoptimalisasi solusi A. Atur $a=0$ terlebih dahulu. Kita mulai iterasikan $i$ dari $2$ dan selama $i\leq \sqrt{N}$, setiap kali $i$ habis membagi $N$, lakukan prosedur ini secara berulang hingga $i$ tidak habis membagi $N$:

- Tambahkan nilai $a$ dengan $1$
- Perbarui nilai $N$ menjadi $N/i$

Setelah mendapat nilai $a$, keluarkan $p^a$ kemudian atur ulang nilai $a$ menjadi $0$. Karena nilai pertama $i$ yang membagi $N$ sudah pasti berupa bilangan prima, maka dijamin setelah tiap iterasi $i$, tidak ada bilangan asli $\leq i$ yang lebih dari $1$ yang habis membagi $N$. Untuk mempermudah penulisan kode, kita hanya perlu menulis subprogram bernama `pangkatTerbesar(i,N)` dengan metode _pass by reference_.

<details>
    <summary>Kode Untuk Solusi B (C++ stdio.h library)</summary>

```c++
#include <stdio.h>
#include <cmath>

int pangkatTerbesar(long long& k, long long& n) {
  int a = 0;
  long long p = k;
  while (n % p == 0) {
    a++;
    p *= k;
  }
  p /= k;
  n /= p;
  return a;
}

int main() {
  long long N;
  int a;
  scanf("%lld", &N);
  bool pertama = true;
  for (long long i = 2; i <= sqrt(N); i++) {
    if (N % i == 0) {
      a = pangkatTerbesar(i, N);
      // mengkondisikan output
      if (pertama) {
        pertama = false;
      } else {
        printf(" x ");
      }
      printf("%lld", i);
      if (a > 1) {
        printf("^%lld", a);
      }
    }
  }
  // jika nilai N akhir bukan 1, berarti N akhir itu faktor prima N awal
  if (N > 1) {
    if (!pertama) {
      printf(" x ");
    }
    printf("%lld", N);
  }
  printf("\n");
}
```
</details>

Kompleksitas Waktu Solusi B: $O(\sqrt{N})$

Kompleksitas Memori Solusi B: $O(1)$

## Komentar
    
- Untuk cara nulis keluarannya, bisa dilihat pengkondisiannya di kode untuk setiap solusi. 
- Soal ini sangat menarik, karena ada banyak perspektif dan cara pintar secara matematis untuk menyelesaikan soal ini dengan batasan yang diberikan. Bahkan, kode di solusi A dapat dioptimisasi lagi dengan menggunakan _pass by reference_ dan manipulasi variabel $N$ seperti yang ada di solusi B. Akan tetapi, kompleksitas waktu yang didapatkan tetap lebih lambat daripada solusi B.
- Sangat disarankan untuk menggunakan solusi B apabila batasan dari nilai $N$ jauh lebih tinggi, seperti $N\leq 10^{12}$. (Bahkan sebenernya memang harus karena nanti kena ~~mental~~ **TLE** hebat kalo pake solusi A) 

## Materi Yang Berhubungan
    
- [Faktorisasi Prima, KPK, dan FPB](https://www.kompas.com/skola/read/2023/03/14/153000569/cara-mencari-faktorisasi-prima-kpk-dan-fpb?page=all)
- [_Passing Parameter_ di C dan C++](https://socs.binus.ac.id/2018/12/05/passing-parameter/)
- [Perbedaan _Pass by Value_ dan _Pass by Reference_ (English)](https://www.geeksforgeeks.org/difference-between-call-by-value-and-call-by-reference/)
