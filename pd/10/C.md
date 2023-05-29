# [Membalik yang Terbalik](https://tlx.toki.id/courses/basic/chapters/10/problems/C)

Author: Hamiz Ghani

Pada soal ini kita akan menerima dua buah input $A$ dan $B$, kemudian kita akan mendefinisikan $C$ sebagai nilai dari $reverse(A)+reverse(B)$ setelah itu kita akan output nilai dari $reverse(C)$. Dimana fungsi `reverse()` merupakan fungsi yang mengeluarkan nilai kebalikan dari suatu bilangan. Pada soal sudah disediakan pseudocode yang menjelaskan algoritma dari fungsi `reverse()` sebagai berikut :
```c++
reverse(x) {
    temp = x
    ret  = 0

    while (temp > 0) {
        ret  = (ret * 10) + (temp mod 10)
        temp = temp div 10
    }

    return ret
}
```

Kompleksitas Waktu: $O(\log A + \log B)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
int a, b, c;
int reverse(int x) {
  int temp = x;
  int ret = 0;
  while (temp > 0) {
    ret = (ret * 10) + (temp % 10);
    temp /= 10;
  }
  return ret;
}
int main() {
  cin >> a >> b;
  c = reverse(a) + reverse(b);
  cout << reverse(c) << endl;
}

```
</details>



<!-- Tambahkan komentar apabila perlu

## Komentar
    
- Komentar I
- Komentar II

-->

<!-- Tambahkan referensi link materi yang berhubungan apabila perlu

## Materi Yang Berhubungan
    
-  [swap() in C++](https://www.geeksforgeeks.org/swap-in-cpp/)
-->

<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal 1](link-soal)
- [Nama Soal II](link-soal)

-->