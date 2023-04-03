# [C. Modus Terbesar](https://tlx.toki.id/courses/basic/chapters/09/problems/C)

Author: Muhammad Kamal Shafi

<!-- Masukkan penjelasan disini -->
Pada soal ini Anda diminta untuk mencari **modus terbesar** dari $N$ $(1 \leq N \leq 10^5)$ buah bilangan bulat $A_1, A_2, \dots, A_N$ $(1 \leq A_i \leq 1000)$.

> **Modus** dalam matematika adalah nilai yang paling sering muncul dalam sebuah data.

Untuk mengetahui modus, banyak kemunculan setiap nilai pada suatu data perlu diketahui. Karena pada soal ini nilai elemen $A_i$ pada data terbatas dari $1$ hingga $1000$, banyak kemunculan nilai bisa disimpan pada sebuah **Array** dengan indeks $1$ sampai $1000$.

Banyak kemunculan nilai bisa didapat dengan melakukan iterasi terhadap nilai di dalam data, seperti contoh berikut:

```c++
for (int i = 0; i < n; i++) {
  counter[a[i]]++;
}
```

Kemudian modus terbesar bisa dicari dengan memanfaatkan informasi banyak kemunculan nilai dalam data tersebut.

---
Kompleksitas Waktu: $O(N)$

Kompleksitas Memori: $O(E)$, dengan $E = 1000$ adalah nilai $A_i$ maksimum yang mungkin.

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

constexpr int MAX_ELEMENT = 1000;

int counter[MAX_ELEMENT + 1];

int main() {
  ios_base::sync_with_stdio(false);
  cin.tie(0);
  cout.tie(0);

  int n;
  cin >> n;
  for (int i = 0; i < n; i++) {
    int a;
    cin >> a;
    counter[a]++;
  }
  int modus = 0;
  for (int i = 1; i <= MAX_ELEMENT; i++) {
    if (counter[i] >= counter[modus]) {
      modus = i;
    }
  }
  cout << modus << '\n';

  return 0;
}
```
</details>

---
## Tambahan

Pada soal ini, nilai dalam data yang terbatas dari $1$ hingga $1000$ memberikan kemudahan untuk menyelesaikan permasalahan dengan cara menghitung kemunculan di dalam array. 

Namun, bagaimanakah cara menyelesaikan permasalahan serupa apabila diberikan batasan yang berbeda, misalnya dengan $(1 \leq A_i \leq 10^9)$?

Selain dengan mengganti pendekatan, masalah ini juga tetap bisa diselesaikan dengan pendekatan yang sama. Yaitu dengan mengubah tempat menyimpan banyak kemunculan dengan menggunakan struktur data **Map** untuk menggantikan peran **Array**.

Baca lebih lanjut mengenai **Map** [disini](https://en.cppreference.com/w/cpp/container/map).


<!-- Tambahkan referensi link materi yang berhubungan apabila perlu

## Materi Yang Berhubungan
    
- [Materi I](link-materi)
- [Materi II](link-materi)

-->

<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal I](link-soal)
- [Nama Soal II](link-soal)

-->
