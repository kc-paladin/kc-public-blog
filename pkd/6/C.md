# [C. Perkalian Skalar](https://tlx.toki.id/courses/competitive/chapters/06/problems/C)

Author: Evelyn

Perhatikan bahwa semakin besar nilai bilangan yang akan kita kalikan, semakin besar juga hasil perkalian yang akan kita dapatkan. Begitu juga sebaliknya.

Untuk lebih jelasnya, perhatikan contoh berikut!

Misalkan ada dua buah bilangan $a$ dan $b$. Jika $a$ = 3 dan $b$ = 6, maka $a × b$ = 3 × 6 = 18.

Kita coba menambah nilai $a$ menjadi 5.

Sekarang, $a$ = 5 dan $b$ = 6, maka $a × b$ = 5 × 6 = 30. Hasilnya lebih besar dibandingkan sebelumnya yang hanya bernilai 18.

Kali ini, kita juga mencoba untuk hanya mengubah nilai $b$ menjadi 7.

$a$ = 3 dan $b$ = 7, maka $a × b$ = 3 × 7 = 21. Hasilnya juga menjadi lebih besar dibandingkan sebelumnya yang hanya bernilai 18.

Selanjutnya, kita mencoba untuk menambah nilai $a$ maupun $b$. Kita tambah nilai $a$ menjadi 5 dan $b$ menjadi 7.

$a$ = 5 dan $b$ = 7, maka $a × b$ = 5 × 7 = 35. Hasilnya menjadi lebih besar dibandingkan sebelum kita menambah nilai $a$ dan $b$, hanya menambah nilai $a$, maupun hanya menambah nilai $b$.

Artinya, untuk mendapatkan hasil perkalian yang minimum, kita perlu meminimalkan bilangan-bilangan yang hendak dikali juga.

Sekarang, kita tahu jika bilangan yang besar pada vektor $v1$ bertemu dengan bilangan yang besar pada vektor $v2$, maka hasil perkaliannya akan menjadi lebih besar. Karena itu, kita bisa menghindari hal tersebut dengan mengurutkan $v1$ dengan urutan *ascending* (menaik) dan mengurutkan $v2$ dengan urutan *descending* (menurun), atau sebaliknya.

**Contoh**

$v1$ = (1, 3, -5)

$v2$ = (-2, 4, 1)

Jika kita langsung mengalikan kedua vektor, maka hasil yang akan kita dapatkan adalah 1 × (-2) + 3 × 4 + (-5) × 1 = -2 + 12 - 5 = 5.

Sementara jika kita mengurutkan $v1$ secara menaik dan $v2$ secara menurun:

$v1$ = (-5, 1, 3)

$v2$ = (4, 1, -2)

maka hasil yang akan kita dapatkan adalah (-5) × 4 + 1 × 1 + 3 × (-2) = -20 + 1 - 6 = -25.

Dengan cara itulah, kita bisa mendapatkan hasil perkalian skalar yang minimum.

Kompleksitas Waktu: $O(N + N log N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

#define int long long

signed main() {
  int N;  cin >> N;

  int v1[N + 1];
  for(int i = 1; i <= N; i++) cin >> v1[i];

  int v2[N + 1];
  for(int i = 1; i <= N; i++) cin >> v2[i];

  sort(v1 + 1, v1 + N + 1);
  sort(v2 + 1, v2 + N + 1, greater<int>());

  // Kompleksitas waktu dari sorting adalah O(N log N)

  int ans = 0;
  for(int i = 1; i <= N; i++) {
    ans += v1[i] * v2[i];
  }

  cout << ans;

  return 0;
}
```
</details>

## Materi yang Berhubungan

- [C++ Sorting](https://www.geeksforgeeks.org/sort-c-stl/)