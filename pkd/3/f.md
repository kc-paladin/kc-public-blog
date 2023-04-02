# [Pesta Bebek](https://tlx.toki.id/courses/competitive/chapters/03/problems/F)

Author: Andreas Timothy

Pada problem ini kita diminta untuk menyisipkan $N$ buah string satu per satu, lalu dalam setiap penyisipan kita diminta untuk mencari pada urutan ke berapa string tersebut setelah diurutkan.

Dari deskripsi diatas, kita udah bisa ngerasain problem ini cocok diselesaikan dengan _insertion sort_.

Kompleksitas Waktu: $O(N^2)$

Kompleksitas Memori: $O(\text{Total panjang string})$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int n;
string s[1005];

int main() {
  cin >> n;
  for (int i = 1; i <= n; i++) {
    cin >> s[i];
    int pos = i;
    // Selama posisinya belum tepat, giring ke depan
    while (pos > 1 && s[pos] < s[pos - 1]) {
      swap(s[pos], s[pos - 1]);
      pos--;
    }
    cout << pos << '\n';
  }
}
```

</details>
