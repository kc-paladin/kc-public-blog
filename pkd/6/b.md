# [B. Jamuan Makan](https://tlx.toki.id/courses/competitive/chapters/06/problems/B)

Author: Andreas Timothy

Problem ini sebenarnya sama persis dengan problem _activity selection_ yang digunakan sebagai contoh pada bab 6 buku [pemrograman kompetitif dasar](https://osn.toki.id/data/pemrograman-kompetitif-dasar.pdf). Observasi utamanya adalah selalu memilih perjamuan dengan waktu berakhir ($Si + Di$) tercepat akan memberikan kita jawaban yang optimal.

Kompleksitas Waktu: $O(N \log N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
#define ll long long

const int maxn = 1e5 + 5;
int n, d, last = 0, ans = 0;
pair<int, int> a[maxn];

int main() {
  cin >> n;
  for (int i = 1; i <= n; i++) {
    cin >> a[i].first >> d;
    a[i].second = a[i].first + d;
  }
  // sort berdasarkan nilai second terkecil
  sort(a + 1, a + n + 1, [](auto i, auto j) { return i.second < j.second; });
  for (int i = 1; i <= n; i++) {
    if (a[i].first >= last) {
      ans++;
      last = a[i].second;
    }
  }
  cout << ans << '\n';
}
```

</details>

## Komentar

- Di sini saya mengasumsikan teman-teman sudah membaca bab 6 buku [pemrograman kompetitif dasar](https://osn.toki.id/data/pemrograman-kompetitif-dasar.pdf), tetapi apabila belum silahkan baca terlebih dahulu untuk penjelasan dan pembuktian yang lebih detail.

## Materi Yang Berhubungan

- [Pemrograman Kompetitif Dasar](https://osn.toki.id/data/pemrograman-kompetitif-dasar.pdf)
- [Sorting Vector/Array of Pair in C++](https://stackoverflow.com/questions/26844983/sort-a-pair-vector-in-c)
