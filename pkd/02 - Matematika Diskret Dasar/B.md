# [B. Prima Ke-K](https://tlx.toki.id/courses/competitive/chapters/02/problems/B)

Author: Muhammad Hasan

Soal ini cukup sederhana, pada setiap query kita hanya perlu *output* bilangan prima ke$-K$.

Mungkin Anda mempunyai intuisi awal seperti ini. Lakukan iterasi dimulai dari angka $i = 1$ dan apabila ketika berada pada angka $i$ kita cek apakah $i$ prima atau tidak, apabila iya, kita tambahkan *counter*, dan ketika *counter* $=K$ maka kita ouput angka $i$ tersebut:

```c++
int cnt = 0;
int i = 1;
while (cnt < k) {
  if (isPrime(i)) {
    k++;
  }
  i++;
}
cout << i << '\n';
```

Sayangnya, pengecekan tersebut terlalu lambat, karena $K_{\max} = 77777$ menyebabkan kita bisa mencapai nilai $i$ sebesar $> 10^5$, dan karena ada $T = 2 \times 10^4$ *query*, kita bisa mencapai total $> 2 \times 10^9$ operasi (Belum lagi operasi yang ditambahkan untuk mengecek $i$ prima atau tidak), tentunya ini tidak akan *pass time limit* yang diinginkan.

Lantas, bagaimana cara menyelesaikan soal ini?

Apabila Anda telah membaca petunjuk pada soal (*most likely* udah baca juga kan yaa), kita bisa menggunakan algoritma klasik nan terkenal bernama [**Sieve of Eratosthenes**](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes).

Inti dari algoritma ini sebetulnya cukup sederhana, dan mudah dijelaskan dengan *snippet* kode sebagai berikut:
```c++
const int N = 1000000;  // batas maksimal

vector<bool> isPrime(N + 1, true);
isPrime[1] = false;
for (int i = 2; i <= N; i++) {
  if (!isPrime[i]) {
    continue;
  }
  for (int j = i + i; j <= N; j += i) {
    isPrime[j] = false;
  }
}
```

![sieve-gif](https://upload.wikimedia.org/wikipedia/commons/b/b9/Sieve_of_Eratosthenes_animation.gif)

Pada intinya, kita mempunyai dua iterasi *for* loop, pada *for* loop pertama, kita mulai dari $i = 2$ sampai $i = N$ (disini bisa dianggap $N$ sebagai batas atas angka yang ingin kita cek).

Lalu, kita cek terlebih dahulu apabila $i$ prima atau tidak, jika tidak prima, maka kita bisa *continue*.

Apabila $i$ prima, maka kita akan *set* kelipatan $i$ menjadi bilangan yang bukan prima (Dimulai dari kelipatan $2$ lalu $3$ sampai seterusnya).

Dengan cara ini, kita bisa *mark / set* dari $1$ sampai $N$, mana saja yang prima dan mana saja yang tidak hanya dengan kompleksitas $O(N \log^2 N)$.

Sehingga untuk menyelesaikan soal ini, kita bisa melakukan beberapa modifikasi pada algoritma diatas, dan melakukan beberapa tahapan sebagai berikut:

- Pada awalnya, kita jalankan algoritma sieve tersebut sebelum menjawab *query*, ini juga biasa dinamakan *precomputation* / istilah lainnya mah mempersiapkan jawaban sebelum pertanyaan dilontarkan
- Kita set batas atas $N = 10^6$ (karena kalau kita coba-coba, maka $N=10^6$ itu sudah cukup untuk mendapatkan $K \geq 77777$)
- Untuk setiap angka prima, bisa kita tampung / masukkan ke dalam `vector<int> primes` secara terurut.
- Kemudian untuk setiap query, dan ditanyakan prima ke$-K$, kita cukup output yang ada pada urutan ke $K$ pada `vector<int> primes` tersebut.

Kompleksitas Waktu: $O(N \log^2 N + T)$

Kompleksitas Memori: $O(N + K_{\max})$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

const int N = 1000000;

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  vector<int> primes;
  vector<bool> isPrime(N + 1, true);
  isPrime[1] = false;
  for (int i = 2; i <= N; i++) {
    if (!isPrime[i]) {
      continue;
    }
    primes.emplace_back(i);
    for (int j = i + i; j <= N; j += i) {
      isPrime[j] = false;
    }
  }
  int t;
  cin >> t;
  while (t--) {
    int k;
    cin >> k;
    cout << primes[k - 1] << '\n';
  }

  return 0;
}
```
</details>

## Komentar
    
- Implementasi dari *Sieve of Eratosthenes* ini dapat berbeda-beda, ada juga yang mungkin lebih efisien, implementasi yang dijelaskan diatas digunakan agar pembaca bisa lebih mudah memahami algoritmanya.
- Untuk tipe soal yang seperti ini, dimana setiap *query independent* dengan *query* lain (satu *query* tidak mempengaruhi *query* yang lain), biasanya kita bisa melakukan *precomputation*, atau *store* jawaban terlebih dahulu sebelum melakukan *query*.
- Terdapat banyak cara lain juga untuk mengecek bilangan prima dalam suatu *range*, bahkan ada yang dengan kompleksitas waktu $O(N)$, pembaca dapat melihat materi yang berhubungan dibawah terkait ini.
    
## Materi Yang Berhubungan

- [Sieve of Eratostenes](https://cp-algorithms.com/algebra/sieve-of-eratosthenes.html)
- [Prime Sieve Linear](https://cp-algorithms.com/algebra/prime-sieve-linear.html)

## Soal Yang Berhubungan

- [Printing some primes - SPOJ](https://www.spoj.com/problems/TDPRIMES/)
- [A conjecture of Paul Erdos - SPOJ](https://www.spoj.com/problems/HS08PAUL/)
