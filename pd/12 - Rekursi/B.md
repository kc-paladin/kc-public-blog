# [B. Faktorial Ganjil-Genap](https://tlx.toki.id/courses/basic/chapters/12/problems/B)

Author: Hamiz Ghani

Pada soal ini kita akan menerima suatu bilangan bulat $N$. Kemudian kita akan output hasil dari $N!!$ yang dapat didefinisikan oleh pseudocode berikut :
```c++
function f(n)
    if (n = 1) 
        return 1
    else if (n mod 2 = 0) 
        return (n / 2) * f(n - 1)
    else
        return (n) * f(n - 1) 
    endif
endfunction
```
Dalam fungsi tersebut $f(n)$ akan mengembalikan $3$ nilai. Apabila $n=1$, menandakan bahwa kita sudah mengalikan bilangan terakhir, maka `return 1`.  Apabila $n$ bilangan ganjil `return f(n - 1) * n`. Apabila $n$ bilangan genap `return f(n - 1) * (n / 2)`.

Kompleksitas Waktu: $O(N)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
int n;
int f(int x) {
  if (x == 1)
    return 1;
  else if (x % 2 == 0) {
    return f(x - 1) * (x / 2);
  } else {
    return f(x - 1) * x;
  }
}
main() {
  cin >> n;
  cout << f(n) << endl;
}

```
</details>



<!-- Tambahkan komentar apabila perlu
-->
## Komentar
    
- Batasan untuk nilai $N$-nya kecil banget :v


<!-- Tambahkan referensi link materi yang berhubungan apabila perlu

## Materi Yang Berhubungan
    
-  [swap() in C++](https://www.geeksforgeeks.org/swap-in-cpp/)
-->

<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal 1](link-soal)
- [Nama Soal II](link-soal)

-->