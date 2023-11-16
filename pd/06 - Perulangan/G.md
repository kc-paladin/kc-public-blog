# [G. Statistika Sederhana](https://tlx.toki.id/courses/basic/chapters/06/problems/G)

Author: Yazid Aqila Haikal

Haloo.. !! 👋

Sebelumnya kan kita sudah mempelajari tentang *perulangan*. Nah, [soal ini](https://tlx.toki.id/courses/basic/chapters/06/problems/G) merupakan salah satu permasalahan yang dapat dijawab menggunakan *perulangan* ✨.

Seperti yang kita tau, di dalam bahasa pemrograman C++, terdapat fungsi **`for`** dan fungsi **`while`** untuk mengoperasikan *perulangan*.

<details>
  <summary>Belum paham "for"?</summary>

`for` adalah salah satu fungsi yang dapat melakukan *perulangan* ✨. 
```c++
for (Pernyataan 1; Pernyataan 2; Pernyataan 3) {
    // blok kode yang akan dijalankan
}
```
Nah, dari contoh di atas, dapat kita lihat bahwa dalam fungsi `for` terdapat 3 pernyataan yang berada di dalam `"()"` dan dibatasi oleh tanda `";"`.

- **Pernyataan 1** dieksekusi (satu kali) sebelum menjalankan blok kode.
- **Pernyataan 2** mendefinisikan kondisi untuk mengeksekusi blok kode.
- **Pernyataan 3** dijalankan (setiap kali) setelah blok kode dieksekusi.

### Contoh:

```
Hitunglah jumlah, mulai dari angka 1 hingga 5.
```

😎: "Ya.., tinggal ditambah manual aja kan? 1+2+3+4+5?"

Sebenernya.., ga salah sih. Tapi, kalau misalkan kita disuruh hitung dari angka 1 sampai 1000 kan bakal pegel juga ngetiknya 🗿.

Nah, disinilah fungsi `for` bakal berguna banget.

Caranya adalah:
1. Misalkan $i = 1$.
2. Buat kondisi yang selama $i ≤ 5$, blok kode di dalam `"{}"` akan dikerjakan.
3. Ubah nilai $i$ menjadi tambah 1 setiap blok kode di dalam `"{}"` selesai dikerjakan.
4. Tunggu sampe $i > 5$.
5. Uuudahh.. 🤌

Dalam bentuk program C++ nya dapat diketikkan sebagai:
```c++
#include <iostream>

using namespace std;

int main() {
  int hasil = 0;
  for (int i = 1; i <= 5; i++) {
    hasil = hasil + i;
  }
  cout << hasil;
  return 0;
}
```
</details>

<details>
  <summary>Belum paham "while"?</summary>

`while` adalah salah satu fungsi yang dapat melakukan *perulangan* ✨. 
```c++
while (Pernyataan) {
    // blok kode yang akan dijalankan
}
```
Nah, dari contoh di atas, dapat kita lihat bahwa dalam fungsi `while` terdapat pernyataan yang berada di dalam `"()"`. Pernyataan tersebut memiliki fungsi yang sama seperti fungsi `if`, yang dimana bertujuan untuk memeriksa kebenaran.

### Contoh:

```
Keluarkan angka dari 1 hingga 5 yang habis dibagi 3,
```

😎: "Ooo... tinggal `cout << "3"` aja kan?"

Boleeeeh.., tapi kalau misalkan yang diminta dari angka 1 sampai 1000 kan ga mungkin kita periksa satu per satu sampai 1000 terus diketik semuanya 🗿.

Nah, dengan adanya fungsi `while` dapat mempermudah hidup kita 🙌.

Caranya adalah:
1. Misalkan $i = 1$.
2. Buat kondisi yang selama $i ≤ 5$, blok kode di dalam `"{}"` akan dikerjakan.
3. Cek apakah $i$ habis dibagi 3. Dan keluarkan jika benar.
4. Buat perintah untuk mengubah nilai $i$ menjadi tambah 1 setiap blok kode di dalam `"{}"` selesai dikerjakan.
5. Tunggu sampe $i > 5$.
6. Uuudahh.. 🤌

Dalam bentuk program C++ nya dapat diketikkan sebagai:
```c++
#include <iostream>

using namespace std;

int main() {
  int i = 1;
  while (i <= 5) {
    if (i % 3 == 0) {
        cout << i;
    }
    i++;
  }
  return 0;
}
```
</details>

## Penjelasan Soal

Soal ini meminta kita untuk membantu Pak Dengklek *mencari* bilangan terbesar dan terkecil diantara $N$ bilangan yang dimilikinya.

<details>
  <summary>Solusi Soal</summary>

<details>
  <summary>💡 <b>Ide Solusi</b> 💡</summary>

1. Permisalkan masukan pertama sebagai nilai yang paling besar dan paling kecil.
2. Buat perulangan sebanyak $N-1$ kali untuk memasukkan bilangan yang lain.
3. Setiap perulangan langsung periksa, jika masukan baru lebih besar daripada bilangan sebelumnya, maka bilangan tersebut menjadi bilangan paling besar.
4. Periksa juga, jika masukan baru lebih kecil daripada bilangan sebelumnya, maka bilangan tersebut menjadi bilangan paling kecil.
5. Nah, habis itu udaaah 😇✨.
</details>

1. Menggunakan For
```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  int N, Ni;
  cin >> N >> Ni; //Ni sebagai patokan bilangan pertama
  int A = Ni, B = Ni; //A = terbesar, B = terkecil
  for (int i = 1; i < N; i++) {
    cin >> Ni;
    if (Ni > A) { //Periksa jika Ni lebih besar dari A
        A = Ni; //Nilai A akan menjadi Ni
    } else if (Ni < B) { //Periksa jika Ni lebih kecil dari B
        B = Ni; //Nilai B akan menjadi Ni
    }
  }
  cout << A << " " << B << endl;
  return 0;
}
```

2. Menggunakan While
```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  int N, Ni, i = 1;
  cin >> N >> Ni; //Ni sebagai patokan bilangan pertama
  int A = Ni, B = Ni; //A = terbesar, B = terkecil
  while (i < N) {
    cin >> Ni;
    if (Ni > A) { //Periksa jika Ni lebih besar dari A
        A = Ni; //Nilai A akan menjadi Ni
    } else if (Ni < B) { //Periksa jika Ni lebih kecil dari B
        B = Ni; //Nilai B akan menjadi Ni
    }
  }
  cout << A << " " << B << endl;
  return 0;
}
```

</details>

## Komentar
    
- Fungsi `for` dan fungsi `while` adalah fungsi dasar yang perlu kita ketahui. Karena kedua fungsi tersebut akan sangat berguna kedepannya 🙌.

## Materi Yang Berhubungan

- [Perulangan](https://docs.google.com/viewerng/viewer?url=https://github.com/ia-toki/training-gate-id-pdf/raw/master/pemrograman-dasar-cpp_06-perulangan.pdf)    
- [C++ For Loop](https://www.w3schools.com/cpp/cpp_for_loop.asp)
- [C++ While Loop](https://www.w3schools.com/cpp/cpp_while_loop.asp)

