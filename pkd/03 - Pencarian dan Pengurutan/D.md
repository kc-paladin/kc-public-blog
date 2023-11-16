# [D. Pendataan Berat Bebek](https://tlx.toki.id/courses/competitive/chapters/03/problems/D)

Author: Muhammad Hasan

Dalam persoalan ini, kita diberikan $N$ berat bebek $B_1, B_2, \dots, B_N$ terurut secara tidak menurun $(B_1 \leq B_2 \leq \cdots \leq B_N)$.

Kemudian, untuk setiap query, diberikan $X$ dan $Y$, kita perlu mencari banyaknya $B_i$ sedemikian sehingga $X < B_i \leq Y$ dengan $1 \leq i \leq N$.

Soal ini dapat kita selesaikan menggunakan **Binary Search**, lebih khususnya lagi, dalam C++ kita dapat memanfaatkan utilitas bawaan bernama `lower_bound` ataupun `upper_bound`.

<details>
  <summary>Penjelasan <code>lower_bound</code> dan <code>upper_bound</code> Dalam C++ </summary>

## Lower Bound dan Upper Bound Dalam C++

`lower_bound` dan `upper_bound` adalah dua fungsi dalam C++ yang digunakan untuk mencari posisi elemen tertentu di dalam suatu array yang sudah terurut secara tidak menurun. Hasil pencarian ini didasari dengan **Binary Search** sehingga jika menggunakan-nya pada array dengan $N$ elemen, maka kompleksitas waktu yang didapat adalah $O(\log N)$.

`lower_bound` digunakan untuk mencari indeks elemen pertama dalam array yang nilainya **lebih dari sama dengan** ($\geq$) dari nilai yang dicari, sementara `upper_bound` digunakan untuk mencari indeks elemen pertama dalam array yang nilainya **lebih besar** ($>$) dari nilai yang dicari.

Misalnya, jika kita memiliki sebuah array yang diurutkan dari kecil ke besar seperti $[1, 2, 3, 4, 5]$.

Apabila kita mencari `lower_bound` dari nilai $3$, maka hasilnya adalah indeks $2$ (karena nilai pada indeks $2$ adalah $3$ atau lebih besar dari sama dengan $3$). Sementara itu, jika kita mencari `upper_bound` dari nilai $3$, maka hasilnya adalah indeks $3$ (karena nilai pada indeks $3$ adalah $4$, yang merupakan nilai pertama yang lebih besar dari $3$).

Berikut adalah contoh kode sederhana untuk menggunakan `lower_bound` dan `upper_bound` dalam C++:

```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
  int arr[] = {1, 3, 3, 5, 7};
  int n = 5;

  // mencari lower_bound dan upper_bound dari nilai 3
  int lower = lower_bound(arr, arr + n, 3) - arr;
  int upper = upper_bound(arr, arr + n, 3) - arr;

  // mencetak hasil
  cout << "Lower bound dari 3 adalah " << lower << endl;
  cout << "Upper bound dari 3 adalah " << upper << endl;

  return 0;
}
```

Hasil eksekusi:

```
Lower bound dari 3 adalah 1
Upper bound dari 3 adalah 3
```

Ini artinya, nilai $\geq 3$ dapat ditemukan pertama kali pada indeks $1$ (`lower_bound`), dan nilai $> 3$ pertama kali ditemukan pada indeks $3$ (`upper_bound`).

> **Catatan**: Hasil dari `lower_bound` dan `upper_bound` sendiri tidak menghasilkan indeks secara langsung, namun mengembalikan **iterator** dari elemen yang didapatkan. Lalu, hasil dari `lower_bound` dan `upper_bound` juga mungkin dapat menghasilkan nilai diluar indeks, contohnya pada kode diatas, apabila kita mencari dengan nilai $10$, maka akan dihasilkan nilai indeks `n`.

</details>

Pada soal ini, salah satu cara menyelesaikannya adalah mencari **indeks terkecil** $L$ sedemikian sehingga $X < B_L$ dan mencari **indeks terbesar** $R$ sedemikian sehingga $B_R \leq Y$.

Setelah mencari $L$ dan $R$, maka nilai yang kita inginkan adalah $R - L + 1$.

Oleh karena itu, sebetulnya kita cukup menggunakan `upper_bound` untuk persoalan ini:

- Untuk mendapatkan indeks $L$ kita gunakan `upper_bound` dengan nilai yang dicari $=X$ (Ini penggunaan `upper_bound` seperti biasa).
- Untuk mendapatkan indeks $R$ kita gunakan `upper_bound` dengan nilai yang dicari $=Y$ kemudian hasil indeks yang didapat kita kurangi $1$ (Hal ini menjamin $R$ adalah indeks terbesar yang memenuhi $B_R \leq Y$).

Kompleksitas Waktu: $O(Q \log N)$

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
  vector<int> a(n);
  for (int i = 0; i < n; i++) {
    cin >> a[i];
  }
  int q;
  cin >> q;
  while (q--) {
    int x, y;
    cin >> x >> y;
    int l = upper_bound(a.begin(), a.end(), x) - a.begin();
    int r = upper_bound(a.begin(), a.end(), y) - a.begin() - 1;
    cout << r - l + 1 << '\n';
  }

  return 0;
}
```

</details>

## Komentar

- Soal ini juga bisa diselesaikan dengan implementasi *Binary Search* yang dilakukan sendiri, dan disarankan untuk lebih membiasakan implementasi sendiri agar lebih fleksibel dengan apa yang kita mau.
- Tentunya akan ada cara untuk memanfaatkan `lower_bound` juga untuk soal ini apabila kita mau.
- Jangan lupa untuk memastikan bahwa array sudah terurut secara tidak menurun saat menggunakan `lower_bound` / `upper_bound`.

## Materi Yang Berhubungan

- [Lower Bound - CPP Reference](https://en.cppreference.com/w/cpp/algorithm/lower_bound)
- [Upper Bound - CPP Reference](https://en.cppreference.com/w/cpp/algorithm/upper_bound)
- [Binary Search](https://en.wikipedia.org/wiki/Binary_search_algorithm)
- [The Most Comprehensive Binary Search Lecture - Codeforces](https://codeforces.com/blog/entry/67509)
