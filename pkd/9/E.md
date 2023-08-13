# [E. Tantangan Dengklek](https://tlx.toki.id/courses/competitive/chapters/09/problems/E)

Author: Arnold Ardianto

_"Loh ini soal graphnya dimana?"_ - semua pengguna TLX yang baru belajar materi bab 9 PKD (graph)

Oke guys. Sekilas setelah membaca soal ini, kita akan heran karena gak ada graph nya tapi masuk di dalam topik graph. Oleh karena itu lewat blog kali ini, ayo kita belajar buat bisa nge-AC in soal ini.

**Observasi 1**

> $N$ nya kecil

Kalo kita perhatikan dari soal ini, nilai $N$ yang mungkin cuma $1 ≤ N ≤ 8$. Itu artinya, dalam _worst case_ nya hanya akan ada maksimal $8! = 40320$ susunan permutasi berbeda

**Observasi 2**

> Anggap aja susunan permutasi kita saat ini $P$. Maka saat kita melakukan operasi _reverse_ dari suatu sub array di $P$, kita akan menghasilkan suatu permutasi baru. Sebut aja permutasi ini $P'$ <br>
<br>
Dengan kata lain dibutuhkan $1$ kali operasi untuk mengubah permutasi $P$ menjadi $P'$

Dari observasi 2 ini kita bisa menyimpulkan : 

**Observasi 3**

> Kita bisa menganggap suatu permutasi sebagai **node** dan suatu operasi sebagai **edge**

![](https://media.tenor.com/tpmaM5Jf7M0AAAAC/mind-blown.gif)

Lebih jelasnya kamu bisa melihat gambar berikut ini : 

Anggap kita memiliki permutasi $P = [4, 2, 3, 1]$ dan $K = 2$ maka bentuk graphnya adalah sebagai berikut : 

![](https://i.ibb.co/hM0yYHQ/Screenshot-2023-08-09-at-16-44-11.png)

**Problem**

Sekarang karena kita sudah mendapatkan bentuk graph nya, kita tinggal mencari suatu _shortest path_ dari permutasi awalan kita $P$ menuju ke suatu permutasi $[1, 2, .., N]$

Untuk menyelesaikan ini kita bisa menggunakan algoritma mencari shortest path yaitu BFS (Breadth First Search) yang sebelumnya sudah dipelajari di problem problem chapter 9 lainnya

**Trik Implementasi**

🙋 _Kak biasanya kan kalo graph itu nomor node nya bilangan bulat (1, 2, ...). Tapi ini kok nomor node nya permutasi? Gimana dong kak?_

😎 Nah untuk mengatasi solusi tersebut, kamu bisa menggunakan `vector<int>` pada C++ sebagai nomor dari node nya. Sedangkan untuk menandai apakah suatu node sudah dikunjungi, kamu bisa menggunakan `map<vector<int>, int>`. Untuk memahami implementasi kedua tipe data tersebut, kamu bisa membaca dahulu teori mengenai map dan vector pada C++ ya untuk mempermudah hidup

**Kompleksitas Waktu:**

Untuk suatu graph yang terdiri dari $V$ buah vertex dan $E$ buah edge, kompleksitas dari algoritma BFS adalah $O(V+E)$

Pada graph diatas, banyak vertex adalah $N!$ dan banyak edge adalah $(N-K+1) * N!$ (setiap node memiliki $(N-K+1)$ buah edge)

Maka dari itu perkiraan kompleksitas menjalankan algoritma BFS adlaah $O(N! + N * N!)$

Untuk mencatat data ke dalam map, kira kira terdapat $\log N!$ buah pengecekan (karena map disusun menggunakan struktur data _binary search tree_ maka untuk mengecek akses suatu map, banyak perbandingan yang dilakukan paling banyak adalah $\log N$)

Sedangkan untuk setiap membandingkan index pada map tersebut, dibutuhkan $O(N)$ pengecekan (terdapat $N$ elemen pada vector yang menjadi index pada map)

Karena kita melakukan pengecekan dan perbandingan setiap kali melakukan BFS, maka kompleksitasnya menjadi $O(N * N! * \log (N!) * N)$

**Kompleksitas Memori:**

Dikarenakan setiap susunan permutasi disimpan pada sebuah map sebagai index, maka kompleksitas memori yang dibutuhkan adalah $O(N!)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
int main() {
  int n, k;
  cin >> n;
  vector<int> start;
  for(int i=0; i<n; i++){
    int x; cin >> x;
    start.push_back(x);
  }
  cin >> k;

  queue<vector<int>> q;
  map<vector<int>, int> dis;
  vector<int> goal;
  for(int i=1; i<=n; i++) goal.push_back(i);

  dis[start] = 0;
  q.push(start);

  while(!q.empty()){
    vector<int> u = q.front(); q.pop();

    if(u == goal){
      cout << dis[u] << endl;
      return 0;
    }

    for(int i=0; i+k <= n; i++){
      vector<int> v = u;
      reverse(v.begin()+i, v.begin()+i+k);
      if(!dis.count(v)){
        dis[v] = dis[u] + 1;
        q.push(v);
      }
    }
  }

  cout << -1 << endl;
}
```
</details>

## Komentar

Sebenarnya untuk soal ini kita tidak harus memakai map untuk menyimpan datanya. Kita bisa menggunakan penomoran _factoradic (factorial number system)_ (menomori semua kemungkinan permutasi dari $0, 1, 2, ..., N!-1)$ sehingga nantinya untuk setiap _state_ pada permutasi yang disimpan sebagai node bisa diberi nomor dengan menggunakan sistem tersebut

Untuk lebih jelasnya kamu bisa membacanya di https://en.wikipedia.org/wiki/Factorial_number_system

## Materi Yang Berhubungan
- https://cplusplus.com/reference/vector/vector/
- https://cplusplus.com/reference/map/map/
- https://en.wikipedia.org/wiki/Factorial_number_system