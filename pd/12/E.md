# [Konversi Biner](https://tlx.toki.id/courses/basic/chapters/12/problems/E)

Author: Hamiz Ghani

Pada soal ini kita akan menerima suatu bilangan bulat $N$. Kemudian kita akan mengeluarkan output berupa bilangan $N$ yang direpresentasikan dalam bentuk biner.
Batasan nilai $N$ pada kasus ini adalah $10^9$. 

Kita dapat menggunakan sebuah pointer yang kita beri nama $idx$.
```c++
int idx = 30;
while (n != 0) {
    if (pow(2, idx) <= n) {
      markn = max(markn, idx);
      a[idx] = 1;
      n -= pow(2, idx);
    }
    idx--;
}
```
$idx$ memiliki nilai awal 30, karena nilai dari `pow(2,30)` lebih dari $10^9$. Apabila ditemukan suatu nilai $idx$ dimana $pow(2,idx)≤N$ maka $a[idx]=1$, kemudian kurangi nilai $N$ dengan $pow(2,idx)$. Setelah itu lanjutkan proses rekursi.

Kompleksitas Waktu: $O(30)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
int n, idx = 30;
int a[31];
int markn;
main() {
  cin >> n;
  while (n != 0) {
    if (pow(2, idx) <= n) {
      markn = max(markn, idx);
      a[idx] = 1;
      n -= pow(2, idx);
    }
    idx--;
  }
  for (int i = markn; i >= 0; i--) {
    cout << a[i];
  }
  cout << endl;
}

```
</details>



<!-- Tambahkan komentar apabila perlu
-->
## Komentar

- fungsi `pow(x,y)` merupakan suatu fungsi bawaan dari C++ yang akan mengembalikan dari $x^y$.


<!-- Tambahkan referensi link materi yang berhubungan apabila perlu

## Materi Yang Berhubungan
    
-  [swap() in C++](https://www.geeksforgeeks.org/swap-in-cpp/)
-->

<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal 1](link-soal)
- [Nama Soal II](link-soal)

-->