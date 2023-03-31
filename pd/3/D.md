# [D. Bebek Untuk Teman](https://tlx.toki.id/courses/basic/chapters/03/problems/D)

Author: Eileen Camelia Limneus

Untuk menyelesaikan persoalan ini, kita harus berkenalan sama **modulo** dulu. Nah, apa itu **modulo**?

**Modulo** adalah sebuah fungsi untuk menentukan sisa bagi integer. Operator **modulo** dilambangkan dengan `%` di C/C++. Untuk contohnya, telah disediakan di website ***tlx.toki.id*** ya!

>Catatan: Perlu diketahui bahwa operasi pembagian akan membagi kedua operand lalu dibulatkan (ke bawah untuk hasil positif, ke atas untuk hasil negatif).

Kompleksitas Waktu: $O(1)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  int n, m, sisa;
  cin >> n >> m;

  sisa = n % m;
  cout << "masing-masing " << n / m << "\n";
  if (sisa == 0) {
    cout << "bersisa 0";
  } else {
    cout << "bersisa " << sisa;
  }
}
```
</details>

## Komentar
    
- Operasi modulo sering digunakan dalam berbagai persoalan seperti membagi bilangan ke dalam kelompok, melakukan perulangan, menentukan urutan dan lainnya. 

## Materi Yang Berhubungan
    
- [Modulo Operator (%) in C/C++ with Examples](https://www.geeksforgeeks.org/modulo-operator-in-c-cpp-with-examples/)
