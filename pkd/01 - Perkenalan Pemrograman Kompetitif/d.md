# [D. Hapus Satu Saja!](https://tlx.toki.id/courses/competitive/chapters/01/problems/D)

Author: Andreas Timothy

Pada problem ini kita diberikan string $A$ dan $B$, lalu kita diminta untuk menentukan apakah kita bisa mengubah string $A$ menjadi $B$ dengan menghapus tepat sebuah karakter dari $A$.

Solusi untuk problem ini cukup sederhana, kita tinggal mencoba untuk menghapus setiap karakter dari $A$ lalu mengecek apakah hasilnya sama dengan $B$.

Kompleksitas Waktu: $O(|A|^2)$

Kompleksitas Memori: $O(|A| + |B|)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

string a, b;
bool bisa = false;

int main() {
  cin >> a >> b;
  for (int i = 0; i < a.length(); i++) {
    // Cek apakah a == b apabila karakter ke-i dihapus
    if (a.substr(0, i) + a.substr(i + 1) == b) bisa = true;
  }
  if (bisa)
    cout << "Tentu saja bisa!";
  else
    cout << "Wah, tidak bisa :(";
  cout << '\n';
}
```

</details>

## Materi Yang Berhubungan

- [C++ Substring](https://www.geeksforgeeks.org/substring-in-cpp/)
