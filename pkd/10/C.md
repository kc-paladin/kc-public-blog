# [C. Pertahanan Pekanbaru](https://tlx.toki.id/courses/competitive/chapters/10/problems/C)

Author: Muhammad Hasan

Soal ini dapat diselesaikan dengan **greedy** sebagai berikut:

- Kita akan coba selalu ambil waktu yang lebih kecil.
- Namun ketika ternyata stamina kita kurang untuk melawan musuh, maka kita coba "koreksi" pemilihan kita sebelumnya.

Untuk lebih detailnya sebagai berikut:

- Kita lakukan iterasi $i$ dari $1$ sampai $N - 1$.
- Kita maintain $ans$ sebagai waktu total untuk mengalahkan musuh.
- Kita maintain *priority queue* $PQ$ yang nantinya akan menyimpan $(L_i - K_i)$ terkecil.
  - Ini akan membantu kita dalam melakukan "koreksi" pemilihan, yakni ketika kita coba ambil $K_i$ dulu, nantinya bisa kita ubah menjadi $L_i$ dengan menambahkan $L_i - K_i$
- Apabila $S_d \geq P_i$ artinya stamina kita cukup:
  - Apabila $K_i \geq L_i$ artinya akan selalu lebih optimal untuk melawan penjaga, dengan ini $ans$ bertambah $L_i$ dan $S_d$ bertambah $1$
  - Apabila $K_i < L_i$
    - Kita ambil dulu saja $K_i$ sehingga $ans$ bertambah sebesar $K_i$
    - Kemudian kita masukkan $(L_i - K_i)$ kedalam $PQ$.
- Apabila $S_d < P_i$ artinya stamina kita kurang:
  - Oleh karena itu, kita bisa "mengkoreksi" pemilihan kita dengan mengambil nilai-nilai dari $PQ$
  - Apabila $PQ$ belum kosong dan $S_d < P_i$ maka:
    - Kita ambil elemen terkecil dari $PQ$, sebut saja $X$, dan hapus elemen tersebut
    - Maka $ans$ kita tambahkan dengan $X$
    - $S_d$ kita tambahkan dengan $1$
    - Dengan ini, kita seolah-olah mengkoreksi pemilihan kita sebelumnya dengan **optimal** (karena selalu mengambil elemen terkecil dari $L_i - K_i$ yang mungkin)
  - Apabila $PQ$ sudah kosong dan $S_d < P_i$ artinya kita tidak bisa lanjut, cukup output $-1$ disini


<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  string useless;
  cin >> useless;
  int n, sd, sm;
  cin >> n >> sd >> sm;
  priority_queue<int, vector<int>, greater<int>> pq;
  vector<tuple<int, int, int>> guards(n - 1);
  for (auto & [ p, k, l ] : guards) {
    cin >> p >> k >> l;
  }
  long long ans = 0;
  for (auto[p, k, l] : guards) {
    while (p > sd && !pq.empty()) {
      int cur = pq.top();
      pq.pop();
      ans += cur;
      sd++;
    }
    if (p > sd) {
      cout << -1 << '\n';
      return 0;
    }
    if (l <= k) {
      ans += l;
      sd++;
    } else {
      ans += k;
      pq.emplace(l - k);
    }
  }
  while (sm > sd && !pq.empty()) {
    int cur = pq.top();
    pq.pop();
    ans += cur;
    sd++;
  }
  if (sm > sd) {
    cout << -1 << '\n';
    return 0;
  }
  cout << ans << '\n';

  return 0;
}
```
</details>

## Komentar

- Disini bisa digunakan `priority_queue<int, vector<int>, greater<int>> pq` untuk menyimpan elemen terkecil pada priority queue.