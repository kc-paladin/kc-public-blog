# [E. Quadtree II: Penerjemahan](https://tlx.toki.id/courses/basic/chapters/13/problems/F)

Author: Joceline Araki

Soal ini merupakan kebalikan dari soal sebelumnya ([Quadtree I: Pengkodean](https://tlx.toki.id/courses/basic/chapters/13/problems/E)). Di soal ini, kita diberi $N$ buah kode yang menunjukkan kuadran homogen bernilai $1$ dan kita harus mencari matriks yang penamaannya sesuai dengan kode yang diberikan. Karena kita sudah mengetahui kode dari matriks tersebut, kita cukup "membagi" matriks tersebut sesuai dengan namanya. Garis besar solusi untuk problem ini adalah:  
1. Lakukan pembagian matriks sesuai kode
2. Isi submatriks tersebut dengan angka $1$  

Untuk lebih jelasnya, gambar berikut menunjukkan matriks yang memiliki kode "112" 

[![Screenshot-2023-06-01-at-16-32-32.png](https://i.postimg.cc/8zFYzWTX/Screenshot-2023-06-01-at-16-32-32.png)](https://postimg.cc/xX25sXJL)
>Perhatikan bahwa angka 1 yang paling pertama hanyalah kode untuk menunjukkan bahwa isi submatriksnya berisi angka-angka 1. Jadi yang harus diproses untuk pembagiannya hanyalah "12" (Kuadran 1 -> Kuadran 2) bukan "112" (Kuadran 1 -> Kuadran 1 -> Kuadran 2)

Pada solusi ini, kita akan membuat sebuah fungsi `quadtree(x1, y1, x2, y2, s)` yang akan memproses pembagian matriks sesuai dengan kode `s`. Cara pembagiannya sama persis dengan soal sebelumnya, yaitu:
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
int arr[N][N];
vector<string>s;

void quadtree(int x1, int y1, int x2, int y2, string t){
    if(t.empty()){
        for(int i = y1; i <= y2; i++){
            for(int j = x1; j <= x2; j++)
                arr[i][j] = 1;
        }
    }  else{
        int xmid = (x1 + x2)/2;
        int ymid = (y1 + y2)/2;

        char nxt = t.back();
        t.pop_back();

        if(nxt == '0') quadtree(x1, y1, xmid, ymid, t);         //Kuadran 0
        else if(nxt == '1') quadtree(xmid + 1, y1, x2, ymid, t);//Kuadran 1
        else if(nxt == '2') quadtree(x1, ymid + 1, xmid, y2, t);//Kuadran 2
        else quadtree(xmid + 1, ymid + 1, x2, y2, t);           //Kuadran 3
    }
}

int main(){
    ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);      //Optimize input output
    memset(arr, 0, sizeof(arr));        //Set semua nilai array menjadi 0
    int n; cin >> n;

    for(int i = 0; i < n; i++){
        string t; cin >> t;
        reverse(t.begin(), t.end());    //reverse string
        t.pop_back();                   //hapus angka 1 yang paling depan
        s.push_back(t);
    }

    int r, c; cin >> r >> c;
    int p = 1;

    while(p < max(r, c)){
        p *= 2;
    }

    for(int i = 0; i < n; i++){
        quadtree(1, 1, p, p, s[i]);
    }

    for(int i = 1; i <= r; i++){
        for(int j = 1; j <= c; j++)
            cout << arr[i][j] << " ";
        cout << '\n';
    }

    return 0;
}
```
</details>

## Komentar
- String `s` harus diproses dari depan ke belakang untuk pembagian matriksnya, namun untuk memudahkan implementasi, kita bisa memanfaatkan _built-in functions_ C++ untuk string, yaitu `.reverse()` dan `.pop_back()`. Tentu saja hal ini tidak harus diikuti dan kita bisa menyimpan index _character_ yang sedang kita proses di stringnya.

## Materi Yang Berhubungan
- [Vector C++](https://www.geeksforgeeks.org/vector-in-cpp-stl/)
- [String reverse()](https://www.geeksforgeeks.org/stdreverse-in-c/)
- [String pop_back()](https://www.tutorialspoint.com/cpp_standard_library/cpp_string_pop_back.htm)