# [B. Balik Daftar](https://tlx.toki.id/courses/basic/chapters/09/problems/B)

Author: Evelyn

Pada soal ini, kita akan menerima sejumlah baris dengan masing-masing baris berisi sebuah bilangan bulat. Lalu, kita diminta untuk mencetak kembali bilangan-bilangan tersebut dengan urutan terbalik.

Untuk menerima sejumlah baris *input* yang tidak kita ketahui jumlahnya, kita bisa memanfaatkan perulangan `while`.

Jadi, selama kita masih diberikan suatu baris berisi bilangan bulat, maka kita akan menyimpan bilangannya terlebih dahulu. Setelah tidak ada lagi *input* yang diberikan, kita akan mencetak bilangan-bilangan yang telah kita simpan dengan urutan terbalik.

Lalu, bagaimana cara menyimpan begitu banyak bilangan? Tentunya kita tidak bisa pakai `int` seperti biasa ya. Kita akan pakai yang namanya array.

Langkah-langkah solusi:
- Deklarasikan suatu variabel dengan nama $i$ (nama variabel bebas) yang bernilai 0.
- Deklarasikan suatu array dengan tipe data `int`. Karena kita tidak tahu banyaknya baris yang akan kita terima, kita akan memberikan ukuran yang maksimal pada array kita, yaitu 100. Kenapa 100? Karena jumlah baris *input* maksimum adalah 100 (lihat bagian **Batasan** pada soal). Kita akan menamakan array ini dengan nama `arr` (nama array bebas).
- Selama kita menerima *input*, simpan bilangan tersebut pada array sebagai data ke- $i$, yaitu `arr[i]`. Setiap kali kita menerima suatu bilangan, tambah nilai $i$ sebesar 1. Kenapa begitu? Misalnya kita menerima bilangan yang pertama. Karena $i$ awalnya bernilai 0, maka bilangan tersebut akan tersimpan pada `arr[0]` (indeks terkecil pada array dimulai dari 0). Selanjutnya, kita mungkin akan menerima bilangan berikutnya. Karena itu, setelah menerima bilangan pertama tadi, kita tambah nilai $i$ sebesar 1. Jadi, nlai $i$ sekarang adalah 1. Maka, kalau kita menerima *input* berikutnya, bilangan tersebut akan disimpan di `arr[1]` karena $i$ kini bernilai 1, dan seterusnya seperti itu.
- Setelah selesai menerima semua input, kita akan mencetak bilangan-bilangan tersebut dalam urutan terbalik. Jadi, kita akan mencetak mulai dari data terakhir yang kita terima, yaitu data ke- $(i - 1)$. Kenapa? Karena setiap kali kita menerima *input*, nilai $i$ akan bertambah 1. Jadi, saat menerima *input* yang terakhir, nilai $i$ tetap ditambah 1 walaupun tidak ada *input* berikutnya lagi. Karena itu, nilai $i$ menjadi lebih 1 dari jumlah data yang kita terima. Jadi, jangan lupa dikurang 1 dulu ya.

Kompleksitas Waktu: $O(N)$

Kompleksitas Memori: $O(N)$

$N$ adalah banyak baris *input* berisi bilangan bulat yang kita terima.

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
int main() {
  int i = 0, arr[100];
  while(cin >> arr[i]) {
    i++;
  }
  for(int j = i - 1; j >= 0; j--) {
    cout << arr[j] << "\n";
  }
  return 0;
}
```
</details>

## Materi yang Berhubungan

- [C++ Arrays](https://www.w3schools.com/cpp/cpp_arrays.asp)