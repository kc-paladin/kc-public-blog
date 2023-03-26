# [B. Menggambar Pegunungan](https://tlx.toki.id/courses/basic/chapters/13/problems/B)

Author: Ackhava Adam Malonda

Soal ini menunjukan cara mengaplikasikan rekursi.

Pada C++, sebuah fungsi dapat memanggil dirinya sendiri seperti saat memanggil fungsi lain. Dalam soal ini kita akan membuat fungsi `mountain(N)` yang akan mencetak pegunungan tingkat `N`. Sebagai fungsi bantu kita juga akan membuat fungsi `drawLine(length)` yang akan membuat garis datar sepanjang `length` karakter dengan karakter `"*"`. Cara kerja `drawLine` cukup mudah dengan hanya menggunakan loop. Di sisi lain, `mountain` bekerja seperti berikut:
- Jika `N` adalah 1, cetak `"*"` dan *return* tanpa menjalankan perintah selanjutnya
- Jalankan `mountain` untuk nilai `N-1`
- Buat sebuah garis dengan panjang `N`
- Jalankan `mountain` kembali untuk nilai `N-1`

Kompleksitas Waktu: $O(N\times 2^{N})$

Kompleksitas Memori: $O(N)$ (dikarenakan *call stack*)

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

void drawLine(int length) {
  for (int i = 0; i < length; i++) {
    cout << '*';
  }
  cout << '\n';
}

void mountain(int N) {
  if (N == 1) {
    cout << "*\n";
    return;
  }
  mountain(N - 1);
  drawLine(N);
  mountain(N - 1);
}

int main() {
  int N;
  cin >> N;
  mountain(N);
}
```
</details>

## Komentar
- Meskipun kompleksitas waktu mungkin lebih baik daripada yang tertera, fungsi tersebut tetap memiliki kompleksitas eksponensial. Penulis tidak dapat membuktikan kompleksitas yang lebih baik, namun solusi ini tetap bisa digunakan.
- Meskipun terlihat memiliki ruang tambahan yang konstan, C++ menyimpan *call stack* yang melacak semua pemanggilan fungsi. Maka, penggunaan memori juga dipengaruhi kedalaman rekursi terdalam. Untuk kasus ini, rekursi akan mecapai kedalam yang berbanding lurus dengan `N`.

## Materi Yang Berhubungan
- [Function Call Stack in C](https://www.geeksforgeeks.org/function-call-stack-in-c/) dapat digunakan sebagai referensi sebab C and C++ memiliki desain yang cukup mirip.