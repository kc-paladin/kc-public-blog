# [E. Quadtree I: Pengkodean](https://tlx.toki.id/courses/basic/chapters/13/problems/E)

Author: Joceline Araki

Pada soal ini, kita diberikan sebuah matriks berukuran $R \times C$ yang harus diberi "nama" atau "kode". _Note that_ hanya matriks/submatriks yang bersifat homogen (semua elemennya sama) yang boleh diberi nama. Jika suatu matriks tidak homogen, maka matriks tersebut harus dibagi menjadi $4$ submatriks yang sama besar. Garis besar  solusi untuk problem ini dapat digambarkan seperti ini: 

[![Quadtree-I.jpg](https://i.postimg.cc/Xq3BybX9/Quadtree-I.jpg)](https://postimg.cc/cg9LVPRJ)

Dalam solusi ini, kita akan membuat 2 fungsi, yaitu:
- `quadtree(x1, y1, x2, y2, s)` yang akan memproses pembagian matriks ke $4$ kuadran dan menyimpan kode berupa string `s` jika submatriks $(x_1, y_1)$ $(x_2, y_2)$ homogen yang bernilai $1$
- `homogen(x1, y1, x2, y2)` yang akan mengembalikan nilai `true` jika semua elemen yang terletak diantara titik koordinat tersebut homogen dan `false` jika sebaliknya.

> Catatan: $(x_1, y_1)$ adalah koordinat titik kiri atas dan $(x_2, y_2)$ adalah koordinat titik kanan bawah dari suatu submatriks

Sekarang, bagaimana cara membagi suatu matriks menjadi $4$ submatriks yang sama besar? Tentu saja kita harus membagi $2$ matriks tersebut secara horizontal dan vertikal di titik tengahnya.

[![Quadtree-I-Pembagian.jpg](https://i.postimg.cc/YqZ3K8zK/Quadtree-I-Pembagian.jpg)](https://postimg.cc/HV05bwNB)

Sebelum cara untuk membagi matriksnya di*spill*, kita _define_ beberapa variabel dulu:
- $mid_x =  \frac{x_1 + x_2}{2}$ (titik tengah dari $x_1$ dan $x_2$)
- $mid_y =  \frac{y_1 + y_2}{2}$ (titik tengah dari $y_1$ dan $y_2$)

Maka, cara untuk membagi suatu matriks yang memiliki titik kiri atas $(x_1, y_1)$ dan titik kanan bawah $(x_2, y_2)$ menjadi $4$ submatriks yang koordinat titik kiri atasnya $(x_3, y_3)$ dan titik kanan bawahnya $(x_4, y_4)$ adalah:
- Kuadran 0 (Kiri - Atas)  
$x_3 = x_1$ &emsp;&emsp;&emsp;&emsp;&ensp;$x_4 = mid_x$  
$y_3 = y_1$ &emsp;&emsp;&emsp;&emsp;&ensp; $y_4 = mid_y$

- Kuadran $1$ (Kanan - Atas)  
$x_3 = mid_x + 1$ &emsp;$x_4 = x_2$  
$y_3 = y_1$ &emsp;&emsp;&emsp;&emsp;&ensp; $y_4 = mid_y$

- Kuadran 2 (Kiri - Bawah)  
$x_3 = x_1$ &emsp;&emsp;&emsp;&emsp;&ensp; $x_4 = mid_x$  
$y_3 = mid_y + 1$ &emsp; $y_4 = y_2$

- Kuadran 3 (Kanan - Bawah)  
$x_3 = mid_x + 1$ &emsp;$x_4 = x_2$  
$y_3 = mid_y + 1$ &emsp; $y_4 = y_2$

Terakhir, jangan lupa untuk mengubah ukuran $R$ dan $C$ jika ukuran matriks tidak tepat bernilai $2^p \times 2^p$. Nilai ini bisa langsung kita cari menggunakan `while` loop.

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

const int N = 130;
int a[N][N];    
vector<string>ans;

bool homogen(int x1, int y1, int x2, int y2){
    int tmp = a[y1][x1];
    for(int i = y1; i <= y2; i++){
        for(int j = x1; j <= x2; j++){
            if(a[i][j] != tmp) return false;
        }
    }

    return true;
}

void quadtree(int x1, int y1, int x2, int y2, string s){
    if(homogen(x1, y1, x2, y2)){
        if(a[y1][x1] == 1) ans.push_back(s);        //tambahkan string 's' ke dalam daftar jawaban
        return;
    }

    int xmid = (x1 + x2)/2;
    int ymid = (y1 + y2)/2;

    quadtree(x1, y1, xmid, ymid, s + "0");          //Kuadran 0
    quadtree(xmid + 1, y1, x2, ymid, s + "1");      //Kuadran 1
    quadtree(x1, ymid + 1, xmid, y2, s + "2");      //Kuadran 2
    quadtree(xmid + 1, ymid + 1, x2, y2, s + "3");  //Kuadran 3
}

int main(){
    ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);  //optimize input output
    int r, c; cin >> r >> c;
    for(int i = 1; i <= r; i++){
        for(int j = 1; j <= c; j++)
            cin >> a[i][j];
    }

    int p = 1;

    while(p < max(r, c)){
        p *= 2; 
    }

    quadtree(1, 1, p, p, "1");

    cout << ans.size() << '\n';
    for(int i = 0; i < ans.size(); i++){
        cout << ans[i] << '\n';
    }

    return 0;
}
```
</details>

## Komentar
- Buat temen-temen yang belum tau `vector` itu apa, _basically_ vector itu array yang fleksibel dan sizenya gak perlu dideclare duluan. Kita bisa menambahkan elemen ke belakang vector dengan menggunakan fungsi `.push_back()`.
- Fun fact: Kenapa ya ukuran matriksnya harus $2^p \times 2^p$ 🤔? _Notice that_ setiap submatriks yang bukan homogen harus dibagi menjadi $4$ kuadran sama besar. Artinya, kita harus membagi $2$ sumbu-$x$ dan sumbu-$y$ di titik tengahnya. Jika ukuran matriksnya tidak tepat $2^p$, maka suatu saat matriks tersebut tidak bisa dibagi $2$ lagi! Hal ini bisa dilihat dari faktorisasi primanya. Sebagai contoh, coba bandingkan $12$ dengan $8$:  
$12 = 2^2 \times 3$  
$8 = 2^3$  
Jika $12$ dibagi $2$ sampai tidak bisa lagi dibagi dengan $2$, maka sisanya adalah $3$. Sedangkan, jika $8$ dibagi $2$ sampai tidak bisa lagi dibagi dengan $2$, maka sisanya adalah $1$. Jika ukuran sekarang adalah $3$ dan matriksnya belum homogen, maka matriks tersebut tidak bisa dibagi $2$ lagi (karena ganjil). Nah, jika ukuran matriks sekarang adalah $1$, maka matriks tersebut *pasti* homogen (kan elementnya cuma 1 :D).

## Materi Yang Berhubungan
- [Vector C++](https://www.geeksforgeeks.org/vector-in-cpp-stl/)

## Soal Yang Berhubungan
- [Quadtree II: Penerjemahan](https://tlx.toki.id/courses/basic/chapters/13/problems/F)