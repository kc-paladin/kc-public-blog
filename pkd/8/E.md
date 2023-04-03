# [E. Penghancuran Batu](https://tlx.toki.id/courses/competitive/chapters/08/problems/E)

Author: Muhammad Hasan

Pada soal ini, kita diberikan nilai berat $N$ buah batu, $W_1, W_2, \dots, W_N$.

Kita dapat menghancurkan batu berberat $W_i$ dengan mengangkat batu berberat $W_j$ apabila pada saat itu kedua batu tersebut bersebalahan dan $W_i \leq W_j$. Tujuan kita adalah menghancurkan sebanyak-banyaknya batu dengan meminimalkan total berat batu yang kita angkat.

Perhatikan bahwa akan selalu tersisa satu buah batu dengan nilai berat maksimal diakhir (hal ini karena batu dengan berat maksimal tidak bisa dihancurkan dengan batu lain, kecuali dengan berat yang sama).

Dalam mendapatkan nilai total berat minimal yang diangkat, pada intinya kita harus mengangkat batu berat terkecil yang memungkinkan.

Kita definisikan $W_X$ sebagai batu dengan berat terkecil yang mana batu sebelahnya bisa kita hancurkan.

Kita bisa selesaikan soal ini dengan mencari $W_X$ dan lakukan hal tersebut berulang-ulang. Sehingga kita bisa lakukan $N$ iterasi untuk mencari $W_X$ tersebut, namun sayangnya ini terlalu lambat karena kita melakukan iterasi $N$ kali, kemudian setiap mencari $W_X$ kita juga melakukan iterasi kembali, sehingga hal ini memakan kompleksitas waktu $O(N^2)$.

Disinilah manfaatnya kita belajar dan menggunakan struktur data, untuk menanggulangi permasalahan lambatnya kompleksitas waktu, kita bisa gunakan `std::set` untuk menyelesaikan soal ini. Gunanya `std::set` disini agar kita bisa mencari nilai $W_X$ dengan cepat, yakni setiap kita cari hanya membutuhkan kompleksitas waktu $O(\log N)$. Namun, bagaimana cara melakukan hal tersebut?

Untuk lebih jelasnya, simak dan pahami algoritma berikut dalam menyelesaikan soal ini:

- Terima input nilai berat batu, dan masukkan ke dalam array `pair<int, int>`, pada array ini kita akan tampung nilai pair `(berat, posisi)`
  - Kita gunakan `pair<int, int>` berupa `(berat, posisi)` karena kita akan membutuhkan nilai `posisi` tersebut
- Ketika sedang menerima input, kita masukkan nilai berupa `(posisi, berat)` ke dalam `set<pair<int, int>>`
  - Kita tampung nilai `(posisi, berat)` dan bukan `(berat, posisi)` karena kita ingin terurut berdasaarkan `posisi` pada `set` yang kita gunakan. 
- Sort array `pair<int, int>` tersebut
  - Dengan cara ini, kita bisa dapatkan berat yang terurut dari kecil ke besar
- Maintain nilai `ans = 0` dan lakukan iterasi array `pair<int, int>` katakan saja kita sedang berada pada `(berat_i, pos_i)`
  - Cari dengan nilai `(pos_i, berat_i)` dari `set` yang kita punya, dengan menggunakan `set::find`
  - Hasil dari `set::find` tersebut akan mengembalikan iterator dari `(pos_i, berat_i)`, kita namakan iterator ini sebagai `it`
  - Apabila `it` merupakan `set::end()` artinya kita tidak menemukan nilai `(pos_i, berat_i)` kita bisa `continue` saja
  - Apabila `it` bukan `set::end()` lakukan hal tersebut.
    - Cek apakah depan dari `it` ini ada, dan apakah bisa kita hapus dengan batu pada `it` (untuk mendapatkan depan dari `it` kita bisa gunakan `next(it, 1)` pada C++)
    - Cek apakah belakang dari `it` ini ada, dan apakah bisa kita hapus dengan batu pada `it` (untuk mendapatkan belakang dari `it` kita bisa gunakan `prev(it, 1)` pada C++)
  - Untuk setiap penghapusan batu yang terjadi, tambahkan nilai `ans` dengan `berat_i`

Pada algoritma diatas, singkatnya kita mencari batu terkecil yang bisa kita angkat dan menghapus batu disebelahnya berulang-ulang.

Kompleksitas Waktu: $O(N \log N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  int n;
  cin >> n;
  vector<pair<int, int>> a(n);
  set<pair<int, int>> st;
  for (int i = 0; i < n; i++) {
    int x;
    cin >> x;
    a[i] = make_pair(x, i);
    st.emplace(i, x);
  }
  sort(a.begin(), a.end());
  long long ans = 0;
  for (auto [val, pos] : a) {
    auto it = st.find(make_pair(pos, val));
    if (it == st.end()) {
      continue;
    }
    while (next(it, 1) != st.end() && next(it, 1)->second <= it->second) {
      ans += it->second;
      st.erase(next(it, 1));
    }
    while (it != st.begin() && prev(it, 1)->second <= it->second) {
      ans += it->second;
      st.erase(prev(it, 1));
    }
  }
  cout << ans << '\n';

  return 0;
}
```
</details>

## Komentar
    
- Soal ini juga bisa diselesaikan dengan data struktur lain seperti DSU (Disjoint Set Union) yang digunakan untuk "menggabungkan" batu yang sudah dihancurkan. Namun, cara diatas sudah lebih baik dan lebih sederhana.
