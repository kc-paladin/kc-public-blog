# [E. If Then / Case](https://tlx.toki.id/courses/basic/chapters/05/problems/E)

Author: Evelyn

Pada soal ini, kita akan diberikan sebuah bilangan $N$, dan kita diminta untuk menentukan apakah $N$ termasuk `satuan`, `puluhan`, `ratusan`, `ribuan`, atau `puluhribuan`.

Untuk menyelesaikan soal ini, kita bisa menggunakan metode percabangan.

Pada C++, kita bisa menggunakan *keyword* berupa `if`, `else if`, dan juga `else`.

Kita akan melakukan pengecekan dengan percabangan seperti berikut ini, dengan urutan dari atas ke bawah:
- Jika $N < 10$, maka $N$ adalah `satuan`.
- Jika $N < 100$, maka $N$ adalah `puluhan`. Kita bisa tahu bahwa $N$ bukan `satuan` karena kita sudah melakukan pengecekan pada poin pertama. Karena $N$ tidak kurang dari 10, maka pengecekan dilanjutkan ke poin berikutnya, dan begitu seterusnya.
- Jika $N < 1000$, maka $N$ adalah `ratusan`.
- Jika $N < 10000$, maka $N$ adalah `ribuan`.
- Selain itu, maka $N$ adalah `puluhribuan`. Kita tidak perlu mengecek apakah $N < 100000$ karena pada soal, nilai $N$ paling besar dijamin kurang dari seratus ribu.

Kompleksitas Waktu: $O(1)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
int main() {
  int N;
  cin >> N;
  if (N < 10) {
    cout << "satuan";
  } else if (N < 100) {
    cout << "puluhan";
  } else if (N < 1000) {
    cout << "ratusan";
  } else if (N < 10000) {
    cout << "ribuan";
  } else {
    cout << "puluhribuan";
  }
  return 0;
}
```
</details>

## Materi Yang Berhubungan
    
- [C++ If ... Else](https://www.w3schools.com/cpp/cpp_conditions.asp)