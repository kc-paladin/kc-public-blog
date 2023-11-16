# [G. Jarak Manhattan](https://tlx.toki.id/courses/basic/chapters/05/problems/G)

Author: Muhammad Hasan

Inti dari permasalahan ini adalah kita perlu menghitung nilai dari suatu mutlak $|A - B|$ dengan $A,B$ bilangan bulat.

Sesuai dengan definisi nilai mutlak, kita akan dapatkan bahwa $|X| = X$ apabila $X \geq 0$ dan $|X| = -X$ apabila $X < 0$. 

Oleh karena itu, nilai dari $|A - B| = A - B$ apabila $A \geq B$ dan $|A - B| = B - A$ apabila $A < B$.

Dengan informasi tersebut, kita bisa gunakan *if* statement untuk komparasi $A, B$ agar bisa mendapatkan nilai mutlak yang kita inginkan.

Kompleksitas Waktu: $O(1)$

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

  int x1, y1, x2, y2;
  cin >> x1 >> y1 >> x2 >> y2;
  cout << (x1 >= x2 ? x1 - x2 : x2 - x1) + (y1 >= y2 ? y1 - y2 : y2 - y1) << '\n';

  return 0;
}
```
</details>

## Komentar
    
- Cara yang lebih mudah dalam menyelesaikan soal ini adalah dengan langsung menggunakan fungsi `abs` pada C++, yang merupakan fungsi **absolute value** atau fungsi nilai mutlak. Kenapa tidak pake solusi ini? soalnya biar ngikutin tema materi aja sih pakai percabangan.
- Pada solution code, digunakan *Ternary Operator* (`<kondisi> ? <benar> : <salah>`) atau bisa dibilang versi cool-nya *if* / *else* di pemrograman.

## Materi Yang Berhubungan
    
- [Ternary Operator](https://www.w3schools.com/cpp/cpp_conditions_shorthand.asp)
- [Abs in C++](https://www.scaler.com/topics/abs-in-cpp/)
