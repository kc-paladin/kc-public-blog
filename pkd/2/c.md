# [C. Pasar Rakyat](https://tlx.toki.id/courses/competitive/chapters/02/problems/C)

Author: Andreas Timothy

Pada problem ini, terdapat $N$ orang pedagang dimana pedagang ke-$i$ akan mengunjungi desa setiap $D_i$ hari sekali. Kita diminta untuk mencari kapan waktu tercepat semua pedagang akan berkunjung bersamaan.

### **Observasi 1**

Pedagang $i$ dan pedagang $j$ pasti bertemu di hari yang merupakan kelipatan dari $D_i$ dan $D_j$. Karena kita mau mencari waktu bertemu yang tercepat, maka kita hanya tertarik dengan kelipatan terkecil atau $\text{KPK}$ dari $D_i$ dan $D_j$. Tugas kita sekarang adalah mencari nilai $\text{KPK}$ dari keseluruhan array $D$.

### **Observasi 2**

Perhatikan bahwa nilai $\text{KPK}$ dari seluruh bilangan dalam array $D$ dapat diformulasikan sebagai berikut:

$KPK(...KPK(KPK(D_1, D_2), D_3), ...D_n)$

Kita akan melakukan iterasi dari index $1$ hingga $N$. Misalkan sekarang kita berada di index ke-$i$ dan kita sudah mempunyai nilai $KPK(D_1, ..., D_{i-1})$, sebut saja nilai ini $val$. Maka $KPK(D_1, ..., D_i) = KPK(val, D_i)$.

Kita akan menggunakan sifat berikut untuk mencari nilai $\text{KPK}$:

$KPK(a, b) = \frac{a \times b}{FPB(a, b)}$

Atau jika diganti dengan variabel yang kita miliki maka akan menjadi:

$KPK(val, D_i) = \frac{val \times D_i}{FPB(val, D_i)}$

Kompleksitas Waktu: $O(N \times log(D_{\max}))$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int n, d, fpb, val;

int main() {
  cin >> n;
  for (int i = 1; i <= n; i++) {
    cin >> d;
    if (i == 1) {
      // Inisialisasi nilai val
      val = d;
    } else {
      // Fungsi __gcd bawaan C++ untuk mencari nilai FPB
      fpb = __gcd(val, d);
      val = val * d / fpb;
    }
  }
  cout << val << '\n';
}
```

</details>

## Komentar

- Selain menggunakan fungsi `__gcd` bisa juga mengimplementasikan fungsi $\text{FPB}$ sendiri jika ingin berlatih
- Jangan panik liat rumusnya, sebenernya simple kok😊, liat aja kodenya😋

## Materi Yang Berhubungan

- [C++ \_\_gcd](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/)
