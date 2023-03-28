# [C. Wartel](https://tlx.toki.id/courses/competitive/chapters/03/problems/C)

Author: Andreas Timothy

Pada problem ini kita diminta untuk mencari nomor telepon dari setiap orang. Tapi kali ini kita ga bisa lakuin linear search kaya soal-soal sebelumnya😞. Kira-kira gimana ya cara nyarinya biar cepet?🤔

💡Ahaa, kita bisa pakai `map`. `Map` memungkinkan kita untuk nyimpen data dalam format _key:value_ dimana kita bisa _assign_ value untuk suatu key **unik**. Cocok banget buat soal ini dimana kita mau _assign_ nomor ke orang yang bersangkutan, dan nama-nama orangnya dijamin unik.

Kompleksitas Waktu: $O((N+Q)\ log\ N)$

Kompleksitas Memori: $O(Total\ panjang\ string\ input)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int n, q;
string s, x;
map<string, string> nomor;

int main() {
  cin >> n >> q;
  for (int i = 1; i <= n; i++) {
    cin >> s >> x;
    nomor[s] = x;
  }
  while (q--) {
    cin >> s;
    if (nomor.count(s)) {
      cout << nomor[s];
    } else {
      cout << "NIHIL";
    }
    cout << '\n';
  }
}
```

</details>

## Komentar

- Soal ini juga bisa diselesaikan dengan cara lain, seperti menggunakan `std::set` atau _binary search_

## Materi Yang Berhubungan

- [C++ Map](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)
