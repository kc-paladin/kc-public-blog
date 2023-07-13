# [E. Sepatu](https://tlx.toki.id/courses/competitive/chapters/06/problems/E)

Author: Yose Yehezkiel Maranata

Bebek Pak Dengklek... make **sepatu**?! **sepatu** paan tuh?!!

[![image.png](https://i.postimg.cc/jd0hTSbB/image.png)](https://postimg.cc/c6h3MZ6c)

bukann bukann...

nih POV pak dangklek : 

[![image.png](https://i.postimg.cc/cHGJH2L1/image.png)](https://postimg.cc/67zKbHZF)

anyway, di soal ini kita diminta untuk mencari banyaknya bebek maksimum yang menggunakan sepatu baru. Seekor bebek bisa make sebuah sepatu kalau ukuran sepatunya pas atau lebih 1. 

[![image.png](https://i.postimg.cc/N047t3tT/image.png)](https://postimg.cc/B8j1cwXQ)

Gambar diatas menunjukan untuk suatu ukuran kaki(warna merah) dapat memilih ukuran sepatu yang diwarna hijaukan. Kita dapat melihat bahwa ukuran kaki tidak dapat lebih besar dari ukuran sepatu. Contoh ukuran kaki 2 tidak dapat memilih sepatu ukuran 1. 

Kita dapat mencocokan dulu kaki dengan sepatu yang pas. Lalu, kita cocokan ukuran kaki dengan sepatu yang lebih 1. 

Implementasi diserahkan kepada kalian untuk belajar :D. Apabila stuck, silahkan lihat solution code.

Kompleksitas Waktu: $O(N \log N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  int n, m;
  cin >> n >> m;
  int freq[100005];
  vector<int> bebek(n);

  for (int i = 0; i < n; i++) cin >> bebek[i];
  sort(bebek.begin(), bebek.end());

  memset(freq, 0, sizeof freq);
  for (int i = 0; i < m; i++) {
    int a;
    cin >> a;
    freq[a]++;
  }

  int cnt = 0;
  for (int a : bebek) {
    if (freq[a] > 0)
      cnt++, freq[a]--;
    else if (freq[a + 1] > 0)
      cnt++, freq[a + 1]--;
  }
  cout << cnt << endl;
}
```
</details>


## Komentar
    
- Kompleksitas waktu $O(N \log N)$ karena kita perlu melakukan sort dengan quicksort. Namun, bisa dipercepat dengan counting sort menjadi $O(N)$ 
- Kompleksitas waktu greedynya tetap $O(N)$




## Soal Yang Berhubungan
    
- [Studying Algorithms](https://codeforces.com/gym/102951/problem/B)


