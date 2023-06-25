# [A. Rak Buku](https://tlx.toki.id/courses/competitive/chapters/06/problems/A)

Author: Evelyn

Pada soal ini, kita diminta untuk menentukan jumlah bebek minimal yang diperlukan dari $N$ ekor bebek untuk mencapai bagian atas rak buku dengan tinggi $B$. Kita juga diberitahu masing-masing tinggi bebek, yaitu bebek ke-$i$ memiliki tinggi $H_i$.

Untuk mencapai bagian atas rak buku, maka total tinggi bebek-bebek yang kita tumpuk tidak boleh kurang dari tinggi rak buku.

Misalkan tinggi rak buku yang baru dibeli Pak Dengklek adalah 40, dan Pak Dengklek mempunyai 6 ekor bebek yang masing-masing tingginya adalah 6, 18, 11, 13, 19, 11. (Dapat dilihat di bagian **Contoh Masukan** pada soal)

Kita bisa mencoba menumpuk bebek-bebek yang ada satu per satu, dimulai dari bebek pertama hingga bebek ke-$i$ $(1 \leq i \leq N)$ sehingga total tinggi badan bebek-bebek tersebut tidak lebih rendah dari tinggi rak buku. Dengan kata lain, $H_1 + H_2 + ... H_i \geq B$.

Dengan cara ini, kita memerlukan 4 ekor bebek karena total tinggi badan bebek pertama hingga bebek keempat adalah 6 + 18 + 11 + 13 = 48, sedangkan tinggi rak buku adalah 40.

Apakah cara ini sudah cukup untuk menentukan jumlah bebek minimal yang diperlukan?

Jawabannya adalah tidak! Ternyata kita bisa menggunakan hanya 3 ekor bebek, yaitu bebek kedua, bebek keempat, dan bebek kelima. Total tinggi bebek-bebek tersebut adalah 18 + 13 + 19 = 50, cukup untuk melewati tinggi rak buku yang hanya bernilai 40. Artinya cara yang kita gunakan tadi belum tepat.

Sebenarnya, solusi dari soal ini sederhana saja. Kita hanya perlu berpikir secara *greedy*.

Dengan mengutamakan bebek-bebek yang lebih tinggi, kita bisa mencapai bagian atas rak buku dengan jumlah bebek yang lebih sedikit.

Kita urutkan bebek-bebek menurut tingginya, mulai dari yang tertinggi hingga yang terendah. Lalu, kita akan memilih $X$ bebek tertinggi sehingga total tinggi $X$ ekor bebek tersebut tidak lebih rendah dari tinggi rak buku.

Dengan cara ini, kita bisa meminimalkan jumlah bebek yang kita perlukan.

Kompleksitas Waktu: $O(N + N log N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

#define int long long

signed main() {
  int N, B;  cin >> N >> B;
  int H[N + 1];
  for(int i = 1; i <= N; i++) cin >> H[i];

  sort(H + 1, H + N + 1, greater<int>()); // O(N log N)

  int height = 0;

  for(int i = 1; i <= N; i++) {
    height += H[i];
    if(height >= B) {
      cout << i;
      return 0;
    }
  }
  
  return 0;
}
```
</details>

## Materi yang Berhubungan

- [C++ Sorting](https://www.geeksforgeeks.org/sort-c-stl/)