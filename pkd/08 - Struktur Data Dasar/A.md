# [A. Stack dan Queue](https://tlx.toki.id/courses/competitive/chapters/08/problems/A)

Author: Evelyn

Sebelum kita membahas solusi dari soal ini, kita berkenalan dulu dengan *stack* dan *queue*.

Apa itu *stack*?

*Stack* dapat dimisalkan sebagai tumpukan, misalnya tumpukan piring. Jika kita ingin menambahkan piring baru, maka kita letakkan di atas tumpukan tersebut. Jika kita ingin mengambil sebuah piring dari tumpukan tersebut, maka kita akan mengambil yang paling atas.

Oleh karena itu, struktur data *stack* bersifat LIFO (*Last In First Out*). Artinya informasi yang terakhir dimasukkan ke dalam *stack* akan menjadi informasi pertama yang bisa dikeluarkan. Informasi yang kita masukkan akan diletakkan di bagian paling atas dari tumpukan. Kita hanya bisa mengakses atau menghapus informasi paling atas.

Lalu, apa itu *queue*?

*Queue* dapat dimisalkan sebagai antrean. Jika kita mengantre di tempat umum, kita pasti berdiri di bagian paling belakang dari barisan kan? Lalu, orang yang dilayani terlebih dahulu adalah orang yang berada di bagian paling depan dari barisan. 

Begitu juga dengan *queue*. Informasi yang kita masukkan ke dalam *queue* akan diletakkan di belakang barisan. Informasi yang bisa diakses adalah informasi yang terletak di bagian paling depan.

Sekarang kita bahas soalnya ya.

Soal ini meminta kita untuk bisa memasukkan elemen ke bagian depan ataupun belakang struktur data, serta menghapus elemen ke bagian depan ataupun belakang struktur data.

Jika kita menggunakan *stack*, kita hanya bisa memasukkan elemen ke bagian belakang *stack* dan menghapus elemen paling belakang pada *stack*.

Jika kita menggunakan *queue*, kita hanya bisa memasukkan elemen ke bagian belakang *queue* dan menghapus elemen paling depan pada *queue*.

Karena itu, kita akan menggunakan struktur data *deque* (*double ended queue*) yang memungkinkan untuk memasukkan elemen ke bagian depan ataupun belakang struktur data, serta menghapus elemen ke bagian depan ataupun belakang struktur data.

Pada struktur data *deque*, kita menggunakan fungsi `push_front()` untuk memasukkan elemen ke bagian depan *deque*, `push_back()` untuk memasukkan elemen ke bagian belakang *deque*, `pop_front()` untuk menghapus elemen paling depan pada *deque*, `pop_back()` untuk menghapus elemen paling belakang pada *deque*.

Kompleksitas Waktu: $O(N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

#define int long long

signed main() {
  int N;
  cin >> N;

  string s;
  int x;

  deque<int> dq;

  while (N--) {
    cin >> s;
    if (s == "push_front") {
      cin >> x;
      dq.push_front(x);
    } else if (s == "push_back") {
      cin >> x;
      dq.push_back(x);
    } else if (s == "pop_front") {
      dq.pop_front();
    } else if (s == "pop_back") {
      dq.pop_back();
    }
  }

  for (auto ans : dq) cout << ans << " ";

  return 0;
}
```
</details>

## Materi yang Berhubungan

- [C++ Stack](https://www.programiz.com/cpp-programming/stack)

- [C++ Queue](https://www.programiz.com/cpp-programming/queue)

- [C++ Deque](https://www.programiz.com/cpp-programming/deque)