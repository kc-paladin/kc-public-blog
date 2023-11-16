# [B. 5 Segmen Garis](https://tlx.toki.id/courses/competitive/chapters/12/problems/B)

Author: Muhammad Hasan

Pada soal ini kita diberikan sebuah segiempat dan garis lurus, kita perlu check apakah garis lurus tersebut berpotongan dengan segiempat.

Soal ini tentunya cukup sederhana, kita hanya perlu mengecek apakah garis lurus tersebut berpotongan dengan minimal salah satu dari $4$ segmen garis yang membentuk segiempat.

Untuk mengecek apakah dua garis berpotongan, dapat melihat lebih detail pada materi [Check If Two Segments Intersect - CP Algorithms](https://cp-algorithms.com/geometry/check-segments-intersection.html).

Kode untuk mengecek dua garis lurus berpotongan adalah sebagai berikut:

```cpp
struct pt {
    long long x, y;
    pt() {}
    pt(long long _x, long long _y) : x(_x), y(_y) {}
    pt operator-(const pt& p) const { return pt(x - p.x, y - p.y); }
    long long cross(const pt& p) const { return x * p.y - y * p.x; }
    long long cross(const pt& a, const pt& b) const { return (a - *this).cross(b - *this); }
};

int sgn(const long long& x) { return x >= 0 ? x ? 1 : 0 : -1; }

bool inter1(long long a, long long b, long long c, long long d) {
    if (a > b)
        swap(a, b);
    if (c > d)
        swap(c, d);
    return max(a, c) <= min(b, d);
}

bool check_inter(const pt& a, const pt& b, const pt& c, const pt& d) {
    if (c.cross(a, d) == 0 && c.cross(b, d) == 0)
        return inter1(a.x, b.x, c.x, d.x) && inter1(a.y, b.y, c.y, d.y);
    return sgn(a.cross(b, c)) != sgn(a.cross(b, d)) &&
           sgn(c.cross(d, a)) != sgn(c.cross(d, b));
}
```

Berikut merupakan *breakdown* dari kode tersebut:

```cpp
struct pt {
    long long x, y;
    pt() {}  // Konstruktor default
    pt(long long _x, long long _y) : x(_x), y(_y) {}  // Konstruktor dengan parameter
    pt operator-(const pt& p) const { return pt(x - p.x, y - p.y); }  // Operator pengurangan vektor
    long long cross(const pt& p) const { return x * p.y - y * p.x; }  // Perkalian silang vektor
    long long cross(const pt& a, const pt& b) const { return (a - *this).cross(b - *this); }  // Perkalian silang 3 titik
};
```

- `struct pt` adalah struktur yang merepresentasikan sebuah titik dalam $\text{2D}$ dengan koordinat $X$ dan $Y$.
- Fungsi-fungsi di dalamnya memungkinkan pengurangan vektor dan perhitungan perkalian silang yang akan berguna untuk menentukan hubungan posisi garis-garis.

```cpp
int sgn(const long long& x) { return x >= 0 ? x ? 1 : 0 : -1; }
```

- Fungsi `sgn` digunakan untuk menentukan tanda dari suatu bilangan.
- Nilai yang dikembalikan adalah $1$ jika bilangan positif, $0$ jika nol, dan $-1$ jika bilangan negatif.

```cpp
bool inter1(long long a, long long b, long long c, long long d) {
    if (a > b)
        swap(a, b);
    if (c > d)
        swap(c, d);
    return max(a, c) <= min(b, d);
}
```
- Fungsi `inter1` digunakan untuk mengecek apakah dua interval $[a, b]$ dan $[c, d]$ berpotongan.
- Jika salah satu interval tidak terurut, fungsi ini akan mengurutkannya terlebih dahulu.
- Kemudian, fungsi ini memeriksa apakah nilai terkecil dari interval pertama masih lebih kecil dari atau sama dengan nilai terbesar dari interval kedua.

```cpp
bool check_inter(const pt& a, const pt& b, const pt& c, const pt& d) {
    if (c.cross(a, d) == 0 && c.cross(b, d) == 0)
        return inter1(a.x, b.x, c.x, d.x) && inter1(a.y, b.y, c.y, d.y);
    return sgn(a.cross(b, c)) != sgn(a.cross(b, d)) &&
           sgn(c.cross(d, a)) != sgn(c.cross(d, b));
}
```

- Fungsi `check_inter` digunakan untuk mengecek apakah dua garis yang ditentukan oleh titik-titik $a$ dan $b$, serta titik-titik $c$ dan $d$, berpotongan.
- Pertama, fungsi ini memeriksa apakah titik $c$ dan $d$ berada pada garis yang sama dengan garis yang diwakili oleh titik-titik $a$ dan $b$. Ini dilakukan dengan menggunakan perkalian silang.
- Jika titik-titik tersebut berada pada garis yang sama, maka fungsi akan memeriksa apakah interval proyeksi $X$ dan $Y$ dari titik-titik berpotongan.
- Jika titik-titik tidak berada pada garis yang sama, fungsi ini memeriksa apakah hasil perkalian silang dari titik-titik membentuk tanda yang berbeda saat dibandingkan dengan kedua pasangan titik.
- Jika salah satu kondisi terpenuhi, berarti garis-garis berpotongan.

Dengan kata lain, fungsi `check_inter` menggunakan perkalian silang dan konsep interval untuk menentukan apakah dua garis berpotongan atau tidak.

Kompleksitas Waktu: $O(N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

struct point {
  long long x, y;
  point() {}
  point(long long _x, long long _y) : x(_x), y(_y) {}
  point operator-(const point& p) const { return point(x - p.x, y - p.y); }
  long long cross(const point& p) const { return x * p.y - y * p.x; }
  long long cross(const point& a, const point& b) const {
    return (a - *this).cross(b - *this);
  }
};

int sgn(const long long& x) { return x >= 0 ? x ? 1 : 0 : -1; }

bool inter1(long long a, long long b, long long c, long long d) {
  if (a > b) swap(a, b);
  if (c > d) swap(c, d);
  return max(a, c) <= min(b, d);
}

bool check_inter(const point& a, const point& b, const point& c,
                 const point& d) {
  if (c.cross(a, d) == 0 && c.cross(b, d) == 0)
    return inter1(a.x, b.x, c.x, d.x) && inter1(a.y, b.y, c.y, d.y);
  return sgn(a.cross(b, c)) != sgn(a.cross(b, d)) &&
         sgn(c.cross(d, a)) != sgn(c.cross(d, b));
}

const int K = 4;

void solve() {
  vector<long long> x(K), y(K);
  for (int i = 0; i < K; i++) {
    cin >> x[i] >> y[i];
  }
  point A(x[0], y[0]);
  point B(x[0], y[1]);
  point C(x[1], y[1]);
  point D(x[1], y[0]);
  point E(x[2], y[2]);
  point F(x[3], y[3]);
  if (check_inter(A, B, E, F) || check_inter(B, C, E, F) ||
      check_inter(C, D, E, F) || check_inter(D, A, E, F)) {
    cout << "YA" << '\n';
  } else {
    cout << "TIDAK" << '\n';
  }
}

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  int tc = 1;
  cin >> tc;
  for (int t = 1; t <= tc; t++) {
    solve();
  }

  return 0;
}
```
</details>

## Materi yang Berhubungan

- [Basic Geometry - CP Algorithms](https://cp-algorithms.com/geometry/basic-geometry.html)
- [Check If Two Segments Intersect - CP Algorithms](https://cp-algorithms.com/geometry/check-segments-intersection.html)