# [C. Modified Stack](https://tlx.toki.id/courses/competitive/chapters/08/problems)

Author: Yose Yehezkiel Maranata

Halooo... :D

Sebelum menyeselasikan soal ini, pastikan kalian memahami konsep stack dulu ya.. 

<details> 
<summary>Stack dan Implementasi Stack menggunakan vector</summary>
credits : 

[Buku PKD by IA TOKI](https://osn.toki.id/data/pemrograman-kompetitif-dasar.pdf)


[![image.png](https://i.postimg.cc/ZYdjS8zT/image.png)](https://postimg.cc/BtJ251vy)
Kita dapat  mengimplementasikan stack menggunakan `vector` agar lebih dinamis, vector memberikan tools yang lebih dapat kita gunakan dibanding stack. Penggantian operasinya sebagai berikut : 
- definisikan sebuah `vector` yang bernama `myvector`
- `myvector.push_back(x)` pengganti operasi `push`, memasukan ekemen `x` ke atas tumpukan.
- `myvector.pop_back()` pengganti operasi `pop`, membuang elemen paling atas.
- `myvector.back()` pengganti operasi `top`, mengakses elemen paling atas.
- `myvector.empty()` pengganti operasi `isEmpty`, memeriksa apakah tumpukan saat ini kosong. 
</details>
<br>


Operasi `add x y` dan `del y` menjadi mudah menggunakan stack. Kita bisa menggunakan forloop untuk operasi push dan pop. 


Namun, `adx` dan `dex` menjadi masalah apabila tidak dihandle dengan baik. Solusi naifnya adalah dengan memforloop isi dari stack lalu menambah atau mengurang masing-masing nilainya dengan x. Solusi tersebut sayangnya terlalu lambat. 


<details>
  <summary>Solusi TLE (75 poin)</summary>

```c++
#include <bits/stdc++.h>

using namespace std;
#define pb push_back

vector<int> st;  // stack

void add() {
  int x, y;
  cin >> x >> y;
  for (int i = 0; i < y; i++) st.pb(x);
  cout << st.size() << endl;
}

void del() {
  int y;
  cin >> y;
  cout << st.back() << endl;
  for (int i = 0; i < y; i++) st.pop_back();
}

void adx() {
  int x;
  cin >> x;
  for (int &i : st) i += x;
}

void dex() {
  int x;
  cin >> x;
  for (int &i : st) i -= x;
}

int main() {
  int q;
  cin >> q;
  while (q--) {
    string s;
    cin >> s;
    if (s == "add") add();
    if (s == "del") del();
    if (s == "adx") adx();
    if (s == "dex") dex();
  }
}
```
</details>

<br>

Oleh karena itu kita memerlukan sebuah optimisasi.
Perhatikan bahwa operasi `adx` dan `dex` memerlukan kita untuk memforloop sebanyak size dari stack, sedangkan Operasi `add` dan `del` hanya forloop sebanyak `y`. Operasi `adx` dan `dex` tentu saja sangat lama apabila kita forloop, pertimbangkanlah cara optimasi supaya bisa lebih cepat.

**Buatlah sebuah variable untuk menyimpan increment dari stack!**

Sebut saja variable ini `inc`. Setiap operasi `adx` dan `dex` kita hanya perlu menambah atau mengurang nilai `inc`. Tentunya dengan adanya `inc`, operasi `add` dan `del` harus kita ubah sedikit. 

Ketika kita mau mengakses elemen yang paling atas, kita hanya perlu menambahkan elemen dengan `inc`. 

Apabila kita perlu memasukan elemen baru, kita mau elemen ini tetap sama dengan nilai orinya, maka elemen ini kita perlu kurangi dahulu dengan `inc`, sehingga saat diakses, nilai yang sudah dikurangi dengan `inc` ditambah dengan `inc` itu sama dengan nilai orinya. 

Kompleksitas Waktu: $O(N \times Y_{max})$ 

Kompleksitas Memori: $O(N \times Y_{max})$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;
#define pb push_back

vector<int> st;  // stack
int inc;         // increment for dex(), adx();

void add() {
  int x, y;
  cin >> x >> y;
  for (int i = 0; i < y; i++) st.pb(x - inc);
  cout << st.size() << endl;
}

void del() {
  int y;
  cin >> y;
  cout << st.back() + inc << endl;
  for (int i = 0; i < y; i++) st.pop_back();
}

void adx() {
  int x;
  cin >> x;
  inc += x;
}

void dex() {
  int x;
  cin >> x;
  inc -= x;
}

int main() {
  int q;
  cin >> q;
  while (q--) {
    string s;
    cin >> s;
    if (s == "add") add();
    if (s == "del") del();
    if (s == "adx") adx();
    if (s == "dex") dex();
  }
}
```
</details>

## Materi Yang Berhubungan
    
- [Stack USACO](https://usaco.guide/gold/stacks?lang=cpp)

## Soal Yang Berhubungan
    
- [Advertisement](https://cses.fi/problemset/task/1142/)

