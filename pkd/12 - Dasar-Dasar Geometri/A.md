# [A. Dua Gelang](https://tlx.toki.id/courses/competitive/chapters/12/problems/A)

Author: Joceline Araki

Di soal ini, kita diberi $2$ lingkaran dengan titik pusat masing-masing $(x_1, y_1)$ dan $(x_2, y_2)$, dan jari-jarinya masing-masing $r_1$ dan $r_2$. Kita harus menentukan apakah ada bagian dari kedua lingkaran tersebut yang saling bersentuhan atau tidak.

Contoh lingkaran yang bersentuhan:
[![Screenshot-2023-08-21-at-14-58-02.png](https://i.postimg.cc/JzpCYDR6/Screenshot-2023-08-21-at-14-58-02.png)](https://postimg.cc/G4TfHp8G)

Contoh lingkaran yang tidak bersentuhan:
[![Screenshot-2023-08-21-at-15-41-21.png](https://i.postimg.cc/XYyBWCvJ/Screenshot-2023-08-21-at-15-41-21.png)](https://postimg.cc/pmRLYyzb)

Pertama-tama definisikan $A$ sebagai titik pusat lingkaran pertama dan $B$ sebagai titik pusat lingkaran kedua. `dist(A, B)` sebagai jarak antara titik $A$ dan $B$.

Mari kita bagi menjadi $2$ kasus, yaitu:
- Pusat lingkaran $1$ tidak berada di dalam lingkaran $2$ atau sebaliknya
[![Screenshot-2023-08-21-at-15-48-01.png](https://i.postimg.cc/BbrNg1ZV/Screenshot-2023-08-21-at-15-48-01.png)](https://postimg.cc/vxvW8TVr)
Dari lingkaran $1$ dan $2$, bisa dilihat bahwa dua lingkaran bisa dikatakan bersentuhan jika jarak kedua pusatnya lebih kecil atau sama dengan jumlah jari-jarinya. Secara formal,  $dist(A, B) \leq r_1 + r_2$. 

- Pusat lingkaran $1$ berada di dalam lingkaran $2$ atau sebaliknya
[![Screenshot-2023-08-21-at-16-13-28.png](https://i.postimg.cc/LsgK4jYJ/Screenshot-2023-08-21-at-16-13-28.png)](https://postimg.cc/2qYX2bxY)
Dari lingkaran $2$ dan $3$, bisa dilihat bahwa dua lingkaran bisa dikatakan bersentuhan jika jarak kedua pusatnya ditambahkan dengan jari-jari lingkaran yang lebih kecil lebih besar atau sama dengan jari-jari lingkaran yang lebih besar.  Secara formal, $dist(A, B) + r_1 \geq r_2$ dimana $r_1 < r_2$.

Setelah mendapatkan observasi tersebut, kita bisa langsung mengimplementasikan solusinya :D

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);
  double x1, y1, r1;
  cin >> x1 >> y1 >> r1;
  double x2, y2, r2;
  cin >> x2 >> y2 >> r2;

  double a = abs(x1 - x2);
  double b = abs(y1 - y2);

  if (hypot(a, b) > r1 + r2 || hypot(a, b) + min(r1, r2) < max(r1, r2))
    cout << "tidak bersentuhan" << '\n';
  else
    cout << "bersentuhan" << '\n';

  return 0;
}
```
</details>

## Materi Yang Berhubungan
- [GeeksForGeeks - Check if a circle lies inside another circle or not](https://www.geeksforgeeks.org/check-if-a-circle-lies-inside-another-circle-or-not/)
- [GeeksForGeeks - Check if two given circles touch or intersect](https://www.geeksforgeeks.org/check-two-given-circles-touch-intersect/)
