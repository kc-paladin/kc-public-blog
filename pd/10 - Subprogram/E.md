# [E. Komposisi Fungsi](https://tlx.toki.id/courses/basic/chapters/10/problems/E)

Author: Muhammad Hasan

Kita bisa melakukan *for loop* sebanyak $K$ kali dengan melakukan assignment sebagai berikut:

- $x = |Ax + B|$

Hasil $x$ terakhir merupakan jawaban yang kita inginkan.

Kompleksitas Waktu: $O(K)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  int A, B, K, X;
  cin >> A >> B >> K >> X;
  for (int i = 0; i < K; i++) {
    X = abs(A * X + B);
  }
  cout << X << '\n';

  return 0;
}
```
</details>