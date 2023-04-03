# [H. Membeli Beras](https://tlx.toki.id/courses/competitive/chapters/03/problems/H)

Author: Andreas Timothy

Pada problem ini kita diberikan $N$ buah karung beras dimana karung ke-$i$ memiliki berat $W_i$ kilogram serta harga $C_i / W_i$ per kilogram. Kita diminta untuk membeli beras dengan kapasitas maksimum $X$ kilogram dengan harga maksimum.

Untuk menyelesaikan problem ini, kita perlu membeli beras dari harga/kg termahal ke termurah. Untuk setiap beras, kita mau membeli berasnya sebanyak mungkin.

Permasalahan yang muncul selanjutnya adalah bagaimana cara kita mengurutkan beras berdasarkan harga sambil tetap menyimpan beratnya. Solusinya adalah dengan menyimpan berat dan harga beras dalam satu variabel yang sama. Hal ini bisa dicapai dengan menggunakan `std::pair` atau `struct`

Kompleksitas Waktu: $O(N^2)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int n, x, w[1005], c;
pair<double, int> a[1005];

int main() {
  cin >> n >> x;
  for (int i = 1; i <= n; i++) cin >> w[i];
  for (int i = 1; i <= n; i++) {
    cin >> c;
    // {harga/kg, kg}
    a[i] = {1.0 * c / w[i], w[i]};
  }

  // sort
  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) {
      // pair akan membandingkan nilai first,
      // apabila nilai firstnya sama maka nilai second akan dibandingkan
      if (a[j] < a[j + 1]) swap(a[j], a[j + 1]);
    }
  }

  int pos = 1;
  double cost = 0;
  while (x > 0 && pos <= n) {
    int kg = min(a[pos].second, x);  // berat maksimal yang dapat dibeli
    cost += a[pos].first * kg;
    x -= kg;
    pos++;
  }

  cout << fixed << setprecision(5) << cost << '\n';
}
```

</details>

## Komentar

- Gunakan tipe data `double` untuk menyimpan bilangan desimal agar lebih akurat.
- Sorting juga bisa dilakukan menggunakan `std::sort` bawaan atau metode lain agar lebih cepat, namun disini menggunakan sorting $O(N^2)$ sudah cukup untuk menyelesaikan soal

## Materi Yang Berhubungan

- [C++ Pair](https://www.geeksforgeeks.org/pair-in-cpp-stl/)
- [C++ Struct](https://www.w3schools.com/cpp/cpp_structs.asp)
- [std::sort](https://www.geeksforgeeks.org/sort-c-stl/)
