# [B. Hobi Batu Akik](https://tlx.toki.id/courses/competitive/chapters/10/problems/B)

Author: Muhammad Hasan

Pada soal ini, kita perlu suatu data struktur yang dapat menerima bilangan bulat $X$, mendapatkan bilangan bulat $X_{\max}$ yang sudah diterima, dan mengeluarkan / *remove* 
bilangan bulat $X_{\max}$ yang diterima.

## Solusi 1 (Priority Queue)

Operasi-operasi tersebut mudah dilakukan dengan [**Max Heap**](https://www.codecademy.com/article/max-heaps-conceptual), ada banyak jenis Max Heap yang bisa dipakai, namun yang paling umum dan cocok digunakan disini adalah `std::priority_queue`.

Apabila kita gunakan `std::priority_queue` maka beberapa operasi berat diatas bisa dilakukan dengan $O(\log N)$.

Untuk melihat lebih jelas cara penggunaan-nya, dapat dilihat pada *Solution Code* dibawah.

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
  priority_queue<int> pq;
  for (int i = 0; i < n; i++) {
    int tp;
    cin >> tp;
    if (tp == 1) {
      int x;
      cin >> x;
      pq.emplace(x);
    } else if (tp == 2) {
      cout << pq.top() << '\n';
    } else if (tp == 3) {
      pq.pop();
    }
  }

  return 0;
}
```
</details>


## Solusi 2 (Multiset)

Kita juga bisa menggunakan tipe lain dari **Max Heap** seperti `std::multiset` (Kita gunakan `std::multiset` dan bukan `std::set` karena bisa saja terdapat elemen $X$ yang muncul $>1$ kali).

Untuk melihat lebih jelas cara penggunaan-nya, dapat dilihat pada *Solution Code* dibawah.

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
  multiset<int, greater<int>> ms;
  for (int i = 0; i < n; i++) {
    int tp;
    cin >> tp;
    if (tp == 1) {
      int x;
      cin >> x;
      ms.emplace(x);
    } else if (tp == 2) {
      cout << *ms.begin() << '\n';
    } else if (tp == 3) {
      ms.erase(ms.begin());
    }
  }

  return 0;
}
```
</details>

## Komentar
- Secara *default* `std::priority_queue` menyimpan elemen terbesar pada hasil `top()`-nya, namun kita bisa juga menyimpan elemen terkecil dengan melakukan *declaration* sebagai berikut `std::priority_queue<T, vector<T>, greater<T>>` dengan `T` suatu tipe bilangan seperti `int`.
- Pada kode tersebut digunakan `emplace()` untuk melakukan *insertion*, ini sama saja seperti `insert()`, namun *keyword* `emplace()` tersebut bisa digunakan dibanyak `std` lain seperti `std::set`, `std::multiset`, `std::queue`, `std::stack`, dll.
- Untuk `std::multiset` sendiri secara *default* dia akan menyimpan elemen terkecil pada `begin()`-nya, namun kita bisa modif untuk menyimpan elemen terbesar dengan `std::multiset<T, greater<T>>` seperti pada kode solusi.
- Dalam kasus ini, `std::priority_queue` lebih *simple* dibandingkan `std::multiset` sehingga waktu eksekusi `std::priority_queue` seharusnya menjadi lebih cepat (kalau dari submisi sih kayak gitu juga).
- Tentunya banyak data struktur lain yang bisa digunakan untuk soal klasik seperti ini, masing-masing dengan *pros* dan *cons*-nya.

## Materi Yang Berhubungan
- [Min-Max Heap](https://en.wikipedia.org/wiki/Min-max_heap)
- [Priority Queue C++](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)
- [Multiset C++](https://www.geeksforgeeks.org/multiset-in-cpp-stl/)

## Soal Yang Berhubungan
- [Take Gifts From The Richest Pile - LeetCode](https://leetcode.com/problems/take-gifts-from-the-richest-pile/)
- [Special Array Operation](https://www.hackerearth.com/practice/data-structures/trees/heapspriority-queues/practice-problems/algorithm/pk-and-special-array-operation-1-7bd52ad1/)
