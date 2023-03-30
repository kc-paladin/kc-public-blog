# [F. Floor and Ceiling](https://tlx.toki.id/courses/basic/chapters/05/problems/F)

Author: Faishal Falih

Pada soal ini kita diminta untuk mengeluarkan nilai dari pembulatan ke bawah dan pembulatan ke atas
dari sebuah bilangan $N$ secara berurutan.

Dalam C++, kita bisa menggunakan *keyword* berupa `floor` untuk pembulatan ke bawah dan `ceil`
untuk pembulatan ke atas.

Kompleksitas Waktu: $O(1)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() 
{
  double N;

  scanf("%lf", &N);

  printf("%.0lf %0.lf", floor(N), ceil(N));
}
```
</details>

## Materi Yang Berhubungan
    
- [Ceil and Floor functions in C++](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)