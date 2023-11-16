# [J. Permainan Mejik](https://tlx.toki.id/courses/competitive/chapters/13/problems/JB)

Author: Muhammad Hasan

Pada soal ini kita dipaksa untuk $\text{Menguli Berat}$ karena ini adalah soal OO (Output-Only).

Untuk setiap input file kita bisa coba cari solusi dari input tersebut.

Beberapa ide dasar yang bisa kita lakukan untuk setiap persoalan adalah sebagai berikut:

- Coba untuk selesaikan beberapa row / column satu-satu terlebih dahulu
- Liat elemen terbesar / terkecil pada input, dan coba kira-kira apakah menaruh elemen-elemen besar / kecil bisa mencukupinya
- Apabila kelebihan / kekecilan bisa di *adjust*
- Pada kasus uji juga ada yang berupa [Magic Square](https://en.wikipedia.org/wiki/Magic_square) (Semua rows / column nya sama jumlahnya)
  - Bisa coba liat pola-nya untuk $N$ yang lebih kecil
- Misal $N=5$ pada awalnya bisa coba membuat draft file:
```
X X X X X
X X X X X
X X X X X
X X X X X
X X X X X
```
- Kemudian coba fill-in `X` nya perlahan-lahan untuk mendapatkan hasil sesuai yang diinginkan
- Bisa coba untuk fill-in semua rows dulu baru columns (ataupun sebaliknya), nanti bisa melakukan pertukaran cell sehingga jumlah rows-nya masih aman.
- Pada dasarnya soal ini hanya menebak-nebak dengan strategi coba-coba

Berikut merupakan input dan output dari setiap kasus uji (hasil output tentu saja tidak perlu persis sama dengan yang diinginkan):

---

### Kasus Uji $0$

<details>
<summary>Input</summary>

```
5
- 38 64 - 92
15 - 67 - -
```

</details>

<details>
<summary>Output</summary>

```
1 20 8 9 14
2 6 7 10 13
3 22 16 11 12
4 17 21 19 18
5 25 15 23 24
```

</details>

---

### Kasus Uji $1$

<details>
<summary>Input</summary>

```
4
19 29 39 49
10 38 46 42
```

</details>

<details>
<summary>Output</summary>

```
1 5 7 6
2 8 10 9
3 11 13 12
4 14 16 15
```

</details>

---

### Kasus Uji $2$

<details>
<summary>Input</summary>

```
5
26 - - - 115
32 - - - 56
```

</details>

<details>
<summary>Output</summary>

```
1 8 6 7 4
2 12 13 14 9
3 15 16 17 10
5 18 19 20 11
21 25 24 23 22
```

</details>

---

### Kasus Uji $3$

<details>
<summary>Input</summary>

```
6
111 111 111 111 111 111
111 111 111 111 111 111
```

</details>

<details>
<summary>Output</summary>

```
1 35 4 33 32 6
25 11 9 28 8 30
24 14 18 16 17 22
13 23 19 21 20 15
12 26 27 10 29 7
36 2 34 3 5 31
```

</details>

---


### Kasus Uji $4$

<details>
<summary>Input</summary>

```
7
143 135 140 170 211 259 167
- - - - - - -
```

</details>

<details>
<summary>Output</summary>

```
30 29 28 26 11 10 9
14 15 16 18 19 20 33
27 25 24 22 17 13 12
40 39 38 37 7 5 4
44 43 42 41 36 3 2
49 48 47 46 45 23 1
35 34 32 31 21 8 6
```

</details>

---

### Kasus Uji $5$

<details>
<summary>Input</summary>

```
8
- - 219 281 275 223 201 311
- 280 335 209 - - 257 209
```

</details>

<details>
<summary>Output</summary>

```
27 57 62 16 33 35 53 48
31 56 2 15 34 36 54 11
42 3 63 14 41 40 6 10
32 4 60 45 39 37 52 12
25 58 61 43 24 20 21 23
26 38 1 46 28 30 7 47
51 5 22 13 49 44 9 8
18 59 64 17 29 19 55 50
```

</details>

---

Untuk soal ini kita perlu membuat semua file output tersebut sesuai panduan soal dan mengumpulkannya kedalam bentuk zip, gambarannya sebagai berikut:

```
osn-2018-mejik-output.zip
├───osn-2018-mejik_0.out
├───osn-2018-mejik_1.out
├───osn-2018-mejik_2.out
├───osn-2018-mejik_3.out
├───osn-2018-mejik_4.out
└───osn-2018-mejik_5.out
```

Diakhir, kita juga bisa membuat program checker sederhana, yang mana dia akan mengecheck apakah angka dari $1$ sampai $N^2$ ada semua, kemudian output nilai jumlah kolom / baris.

Berikut merupakan contoh program checker tersebut:

<details>
  <summary>Program Checker</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);

  int n;
  cin >> n;
  vector<vector<int>> a(n, vector<int>(n));
  vector<bool> vis(n * n + 1);
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
      cin >> a[i][j];
      vis[a[i][j]] = 1;
    }
  }
  for (int x = 1; x <= n * n; x++) {
    assert(vis[x]);
  }
  for (int i = 0; i < n; i++) {
    int res = 0;
    for (int j = 0; j < n; j++) {
      res += a[i][j];
    }
    cout << res << " \n"[i == n - 1];
  }
  for (int i = 0; i < n; i++) {
    int res = 0;
    for (int j = 0; j < n; j++) {
      res += a[j][i];
    }
    cout << res << " \n"[i == n - 1];
  }

  return 0;
}
```
</details>

## Komentar

- Apabila ada masalah submisi pada page course TLX, bisa coba submit pada original soalnya pada page OSN TLX [disini](https://tlx.toki.id/problems/osn-2018/0C).