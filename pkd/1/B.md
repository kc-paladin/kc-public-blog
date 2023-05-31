# [B. Runtuh](https://tlx.toki.id/courses/competitive/chapters/01/problems/B)

Author: Yose Yehezkiel Maranata

Halo semua :wave: 

Di blog ini kita akan belajar membuat algorithm untuk permainan Jawbreaker! :hushed:

Pertama-tama, pastikan kalian sudah membaca soalnya dengan benar ya! Kebanyakan gagal nyelesaiin soal ini karena salah baca soal. :wink:

Selama ada suatu baris yang penuh terisi, kita akan terus-menerus meruntuhkan. Kita akan gunakan `while` sambil memeriksa apakah ada suatu baris yang penuh terisi.

Perhatikan visualisasi dari peruntuhan berikut:
[![image.png](https://i.postimg.cc/C55wwmWG/image.png)](https://postimg.cc/ygMMPX6x)

Kita akan runtuhkan masing-masing per kolomnya. Cari lokasi dimana akan bertumpuk, kemudian satu-persatu balok yang terisi diturunkan untuk ditumpuk.

Kompleksitas Waktu: $O(N \times M \times totalPeruntuhan)$

Kompleksitas Memori: $O(N \times M)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  int n, m;
  cin >> n >> m;
  vector<vector<int>> grid(n, vector<int>(m));
  for (int i = 0; i < n; i++) {
    string s;
    cin >> s;
    for (int j = 0; j < m; j++) {
      grid[i][j] = s[j] - '0';
    }
  }
  // hilangin
  while (true) {
    int most_bottom_clear = -1;
    for (int i = 0; i < n; i++) {  // hapus apabila satu baris berisi penuh
      bool cek_all_one = true;
      for (int j = 0; j < m; j++) {
        if (grid[i][j] == 0) cek_all_one = false;
      }
      if (cek_all_one) {
        for (int j = 0; j < m; j++) grid[i][j] = 0;
        most_bottom_clear = i;  // simpen baris yang paling bawah
      }
    }
    if (most_bottom_clear == -1)
      break;  // tidak ada line yang dihilangkan, tidak ada proses peruntuhan
      
    for (int j = 0; j < m; j++) {
      int bottom = most_bottom_clear;
      for (int i = bottom; i < n; i++) {  // cari tempat dimana bakal numpuk
        if (i == n - 1) {
          bottom = i;
          break;
        }
        if (grid[i + 1][j] == 1) {
          bottom = i;
          break;
        }
      }
      for (int i = most_bottom_clear; i >= 0; i--) {  // tumpukin
        if (grid[i][j] != 0) {
          grid[bottom][j] = grid[i][j];
          grid[i][j] = 0;
          bottom--;
        }
      }
    }
  }

  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) cout << grid[i][j];
    cout << endl;
  }
}
```
</details>



## Komentar
    
- kebanyakan solusi menggunakan solusi yang memiliki Kompleksitas Waktu: $O(N^2 \times M \times totalPeruntuhan)$, solusi ini akan mendapatkan `AC`, namun solusi yang di deskripsikan di atas lebih bagus untuk latihan dan implementasi.

<!-- Tambahkan referensi link materi yang berhubungan apabila perlu

## Materi Yang Berhubungan
    
- Komentar I
- Komentar II

-->



## Soal Yang Berhubungan
    
- [Jawbreaker III: Cari Terbesar dan Runtuhkan](https://tlx.toki.id/courses/competitive/chapters/04/problems/F)


