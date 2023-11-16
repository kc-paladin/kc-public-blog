# [Brankas Terkunci](https://tlx.toki.id/courses/basic/chapters/13/problems/D)

Author: Hamiz Ghani

Pada soal ini kita akan menerima dua buah bilangan $N$ dan $K$. Kita akan mengeluarkan $K$ buah bilangan bulat yang berada di antara $1 \dots N$ mulai dari yang paling kecil sampai dengan yang paling besar. Dengan kata lain, kita akan mencetak kombinasi $K$ buah bilangan dari $1$ sampai $N$ secara terurut.

Definisikan fungsi $f(x,y)$ dimana $x$ merupakan index urutan dari $K$ buah bilangan dan $y$ menandakan bilangan terkecil yang dapat kita ambil.

```c++
void f(int x, int y) {
    if (x > k || y > n + 1) //batasan fungsi
        return;
    if (x == k) { //apabila x=k, output
        for (int i = 1; i <= k; i++) {
            cout << arr[i] << " ";
        }
        cout << endl;
    }
    else { //apabila x<k, lakukan transisi fungsi
        for (int i = y; i <= n; i++) {
            arr[x + 1] = i;
            f(x + 1, i + 1);
        }
    }
}
```
Kita akan memanggil $f(0,1)$ untuk setiap kasus. Apabila $x<K$ kita akan melakukan for loop dari bilangan terkecil yang dapat kita ambil yaitu $y$ sampai dengan $N$, apabila kita mengambil bilangan $i$ untuk $y \leq i \leq N$, maka bilangan terkecil yang dapat kita ambil selanjutnya adalah $i+1$ dan tentu saja index untuk fungsi selanjutnya akan bertambah yaitu menjadi $x+1$ sehingga kita akan memanggil $f(x+1,i+1)$ 

Perhatikan batasan fungsi yaitu apabila $f(x,y)$ dimana $x>K$ atau $y>N+1$ maka kita harus menghentikan fungsi tersebut. Kenapa batasannya $y>N+1$ dan bukan $y>N$, karena apabila kita mengambil bilangan terakhir untuk suatu $f(k-1,N)$ transisi selanjutnya adalah $f(k,N+1)$ dengan bilangan yang terakhir diambil adalah $N$ sehingga masih terhitung valid.


Kompleksitas Waktu: $O(N!)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
int n, k;
int arr[15];
void f(int x, int y)
{
    if (x > k || y > n + 1)
        return;
    if (x == k) {
        for (int i = 1; i <= k; i++) {
            cout << arr[i] << " ";
        }
        cout << endl;
    }
    else {
        for (int i = y; i <= n; i++) {
            arr[x + 1] = i;
            f(x + 1, i + 1);
        }
    }
}
main()
{
    cin >> n >> k;
    f(0, 1);
}

```
</details>

## Materi Yang Berhubungan
    
-  [cpp program combination list numbers](https://www.sanfoundry.com/cpp-program-possible-combinations-list-numbers/)