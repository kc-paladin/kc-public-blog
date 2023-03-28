# [B. For](https://tlx.toki.id/courses/basic/chapters/06/problems/B)

Author: Yazid Aqila Haikal

Haloo.. !! 👋

Di soal ini, kita diminta untuk mengoperasikan sebuah *perulangan* ✨🙌.

Yang dimana, di dalam bahasa pemrograman C++, terdapat fungsi **`for`** sebagai salah satu cara mengoperasikan *perulangan*.

<details>
  <summary>Apa itu "for"?</summary>

`for` adalah salah satu fungsi yang dapat melakukan *perulangan* ✨. 
```c++
for(Pernyataan 1; Pernyataan 2; Pernyataan 3){
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
#include<iostream>
using namespace std;

int main(){
  int hasil = 0;
  for(int i = 1; i <= 5; i++){
    hasil = hasil + i;
  }
  cout << hasil;
  return 0;
}
```
</details>

## Penjelasan Soal

Soal ini meminta kita untuk membantu Pak Dengklek *menghitung total* bebek dari $N$ kandang yang dimilikinya dengan cara menjumlahkan nilai $B_1, B_2, ..., B_N$  menggunakan sebuah fungsi *perulangan* `for`.

<details>
  <summary>Solusi Soal</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  int N;
  cin >> N;
  int Bi;
  int hasil = 0;
  for (int i = 0; i < N; i++) {
    cin >> Bi;
    hasil = hasil + Bi;
  }
  cout << hasil << endl;
  return 0;
}
```

</details>

## Komentar
    
- Fungsi `for` adalah salah satu fungsi dasar yang perlu kita ketahui. Karena fungsi `for` kedepannya bakal sangat berguna 🙌.

## Materi Yang Berhubungan

- [Perulangan](https://docs.google.com/viewerng/viewer?url=https://github.com/ia-toki/training-gate-id-pdf/raw/master/pemrograman-dasar-cpp_06-perulangan.pdf)    
- [C++ For Loop](https://www.w3schools.com/cpp/cpp_for_loop.asp)

