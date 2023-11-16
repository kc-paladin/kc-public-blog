# [F. Transpos Matriks](https://tlx.toki.id/courses/basic/chapters/03/problems/F)

Author: I Nyoman Narayan Kitas Utama

Perhatikan bahwa dapat dipastikan matriks yang diberikan hanya berisi 9 angka. Sehingga, kita dapat mendefinisikan 9 variabel berdasarkan format masukan soal, yaitu:

```c++
a b c
d e f
g h i
```

Karena keluarannya adalah transpos dari matriks tersebut, maka kita hanya perlu melakukan prosedur ini:
- Menukar posisi `b` dengan `d`
- Menukar posisi `c` dengan `g`
- Menukar posisi `f` dengan `h`

Setelah melakukan prosedur ini, kita dapat mengeluarkan transpos dari matriks tersebut.

Kompleksitas Waktu: $O(1)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Kode (C++)</summary>
C++ (stdio.h library):

```c++
#include <stdio.h>
int main()
{
    int a, b, c, d, e, f, g, h, i;
    scanf("%d %d %d", &a, &b, &c);
    scanf("%d %d %d", &d, &e, &f);
    scanf("%d %d %d", &g, &h, &i);
    printf("%d %d %d\n", a, d, g);
    printf("%d %d %d\n", b, e, h);
    printf("%d %d %d\n", c, f, i);
    return 0;
}
```

C++ (iostream library):

```c++
#include <iostream>

using namespace std;

int main()
{
    int a, b, c, d, e, f, g, h, i;
    cin >> a >> b >> c;
    cin >> d >> e >> f;
    cin >> g >> h >> i;
    cout << a << " " << d << " " << g << endl;
    cout << b << " " << e << " " << h << endl;
    cout << c << " " << f << " " << i << endl;
    return 0;
}
```
</details>

## Komentar
    
- Cara alternatif untuk menyelesaikan soal ini adalah dengan menggunakan 2D array (Baca tentang array [di sini](https://tlx.toki.id/courses/basic/chapters/09/lessons/A)), membaca 3 masukan per baris dan memasukkannya ke dalam array menurut posisi baris dan kolom, kemudian masukan ke$-j$ di baris ke$-i$ akan menjadi bilangan ke- $i$ di baris ke- $j$ di dalam keluaran. Strategi ini lebih efektif jika ukuran matriks sangat besar atau berdasarkan masukan dengan melakukan [perulangan](https://tlx.toki.id/courses/basic/chapters/06/lessons/A) untuk masukan dan keluaran.
