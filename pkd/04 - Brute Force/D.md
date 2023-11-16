# [D. Kontes Menari](https://tlx.toki.id/courses/competitive/chapters/04/problems/D)

Author: Joceline Araki

Sebelum kita bahas solusi soal ini, yuk pastikan dulu kalian udah paham sama inti soalnya :D Singkatnya, Kwek akan memilih $R$ gerakan berbeda dari $N$ gerakan yang dikuasainya. Sistem _scoring_ gerakannya adalah:
1. Nilai awal suatu gerakan adalah nilai dasar keindahannya.
2. Jika gerakan ke-$i$ adalah gerakan memukau, maka nilai gerakan ke-$(i + 1)$ akan dikalikan $2$.
3. Jika gerakan ke-$i$ adalah gerakan melelahkan, maka nilai gerakan ke-$(i + 1)$ akan dibagi $2$ (dibulatkan ke bawah).
4. Jika gerakan ke-$i$ adalah gerakan meyakinkan, maka nilai *semua* gerakan selanjutnya $(i + 1, i + 2, ..., R)$ akan ditambahkan $Y$.

Setelah itu, ada $J$ orang juri yang diundang, dan masing-masing juri memiliki nilai batas keindahan. Juri ke-$i$ akan terkesima jika total skor/nilai keindahan Kwek melebihi nilai batas juri tersebut. Berapa banyak rangkaian gerakan yang bisa dipilih Kwak untuk membuat setiap juri terkesima?

Kita bisa membagi _problem_ ini menjadi $2$ _subproblem_, yaitu:
1. Mencari nilai dari semua rangkaian gerakan yang bisa dilakukan Kwak.
2. Mencari berapa banyak rangkaian gerakan yang bisa membuat juri ke-$i$ terkesima.

Untuk subproblem pertama, kita bisa membuat fungsi rekursif `permute(x)` seperti pada materi [Rekursi Lanjut](https://tlx.toki.id/courses/basic/chapters/13/lessons/A) untuk mencari semua permutasi $R$ dari $N$ gerakan yang bisa ditampilkan. Kompleksitas untuk bagian ini adalah $O(P(N, R))$. Untuk _worst case_ nya, kita harus memilih $5$ gerakan untuk ditampilan dari $10$ gerakan yang dikuasai $(N = 10, R = 5)$. Nilai $P(10, 5) = \frac{10!}{5!} = 30,240$ (masih masuk di time limit :D)

Untuk subproblem kedua, jika kita menghitung jumlah rangkaian gerakan yang bisa membuat tiap juri terkesima dengan _Linear Search_, kompleksitasnya akan menjadi $O(P(N, R) \times J)$. Untuk _worst case_ nya $(N = 10, R = 5, J = 1000)$, banyak operasi yang dibutuhkan adalah $P(10, 5) \times 1000 = 30,240,000$ (TLE! 🙁). Kita membutuhkan algoritma _searching_ yang lebih efisien, yaitu _Binary Search_! Kita bisa mencari index nilai terbesar yang tidak dapat membuat juri ke-$i$ terkesima, sehingga bisa dipastikan semua nilai yang lebih besar dari nilai tersebut bisa membuat juri ke-$i$ terkesima `idx`. Jawaban akhirnya adalah $P(N, R) - idx$. Dengan begitu, kompleksitas solusi kita akan menjadi $O(\log{(P(N, R))} \times J)$, dan untuk _worst case_ nya, banyak operasi yang dibutuhkan adalah $\log{(P(10, 5))} \times 1000 = ~15,000$ (gak TLE 🎉)

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int n, r, y, j;
vector<int> score;
pair<int, char> arr[15];
int catat[15];
bool mark[15];

void permute(int x) {
  if (x >= r) {
    bool Y = (arr[catat[0]].second == 'Y');
    int ret = arr[catat[0]].first;

    for (int i = 1; i < r; i++) {
      if (arr[catat[i - 1]].second == 'P') {
        ret += (arr[catat[i]].first * 2);
      } else if (arr[catat[i - 1]].second == 'L') {
        ret += (arr[catat[i]].first / 2);
      } else {
        ret += arr[catat[i]].first;
      }

      if (Y) ret += y;

      if (arr[catat[i]].second == 'Y') Y = true;

      if (ret >= 100000) {  // nilai batas juri maks. adalah 100,000
        score.push_back(100001);
        return;
      }
    }

    score.push_back(ret);
  } else {
    for (int i = 0; i < n; i++) {
      if (!mark[i]) {
        catat[x] = i;
        mark[i] = true;
        permute(x + 1);
        mark[i] = false;
      }
    }
  }
}

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);
  string subtask;
  cin >> subtask;
  int st;
  cin >> st;

  cin >> n >> r >> y >> j;
  for (int i = 0; i < n; i++) {
    int d;
    cin >> d;
    char t;
    cin >> t;
    arr[i] = {d, t};
  }

  permute(0);
  sort(score.begin(), score.end());

  while (j--) {
    int x;
    cin >> x;
    int sz = score.size();
    int tmp = upper_bound(score.begin(), score.end(), x) - score.begin();
    cout << sz - tmp << endl;
  }

  return 0;
}
```
</details>

## Komentar
- Fungsi `upper_bound(x)` mengembalikan index pertama yang memiliki nilai lebih besar dari $x$. Kompleksitas fungsi ini kurang lebih sama dengan binary search.

## Materi Yang Berhubungan
- [upper_bound() and lower_bound() in C++](https://www.geeksforgeeks.org/upper_bound-and-lower_bound-for-vector-in-cpp-stl/) 

