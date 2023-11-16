# [H. Radar Pesawat](https://tlx.toki.id/courses/competitive/chapters/13/problems/H)

Author: Muhammad Hasan

Pada soal ini diberikan $N$ pesawat $P_1, P_2, \dots, P_N$ dengan pesawat $P_i=(T_i, V_i)$ dimana 
$T_i=$ detik keberangkatan pesawat ke-$i$ dan $V_i$ kecepatan satuan / detik pesawat ke-$i$. 
Selain itu, setiap $P_i$ ditaruh pada koordinat $(i, 0)$.

Kita bisa menaruh radar pada $(A, B)$ dan setiap pesawat yang melalui garis 
$y=B$ akan menerima sinyal dari radar tersebut. Namun, hal tersebut hanya dapat dilakukan jika tidak ada halangan, misalnya pesawat lainnya, di antara pesawat dan radar tersebut.

Tujuan kita adalah **menaruh radar seminimal mungkin** agar semua pesawat mendapatkan sinyal.

Disini kita bisa melakukan beberapa observasi.

Perhatikan bahwa, apabila kita menaruh radar $R$ pada suatu koordinat $(A, B)$ maka:

- Semua pesawat $P_i$ dengan koordinat $(i, 0)$ dapat menerima sinyal radar 
$R$ jika $i < A$ dan tidak ada $P_j$ sedimikian sehingga nilai $P_i =$ nilai $P_j$ dan $i < j$.
- Semua pesawat $P_i$ dengan koordinat $(i, 0)$ dapat menerima sinyal radar 
$R$ jika $i > A$ dan tidak ada $P_j$ sedimikian sehingga nilai $P_i=$ nilai $P_j$ dan $j < i$.

Hal ini didapat dengan memilih $B$ yang tepat (memilih $B$ agar banyaknya pesawat yang terkena semaksimal mungkin).

Karena kita tidak perlu memberikan hasil $B$ disoal, kita bisa asumsikan saja bahwa kita akan selalu memilih $B$ yang tepat, sehingga yang terpenting adalah memilih nilai $A$ pada suatu radar.

Kita dapat menyelesaikan persoalan ini dengan **Algoritma Greedy** sebagai berikut:

- Didefinisikan $pos$ sebagai tempat terakhir kita menaruh radar pada suatu pesawat $i$
    - Apabila kita menaruh pada pesawat $i$ atau $pos=i \rightarrow$ kita anggap saja bahwa kita taruh radar pada koordinat $(i - 0.5, B)$.
    - Pada awalnya kita *set* $pos=-1$ 
- Didefinisikan $S$ sebagai suatu himpunan nilai pesawat $P$ yang masih belum terkena suatu sinyal
    - Pada awalnya kita *set* $S$ sebagai himpunan kosong.
    - Kita bisa gunakan `std::set<pair<int, int>>` untuk implementasi $S$ ini.
- Kita akan lakukan iterasi $i$ dari $1$ sampai $N$, dan *set* variabel jawaban $ans=0$.
- Didefinisikan $prev$ sebagai indeks terakhir adanya nilai $P_i$
    - Dengan kata lain $P_{prev} = P_i$ dan $prev  < i$
    - Apabila tidak ada kita *set* $prev=-1$.
    - $prev$ ini bisa kita dapatkan dengan `std::map<pair<int, int>, int>` (saat iterasi bisa kita *store* indeks terakhir dari $P_i$).
- Apabila $prev < pos$
    - Kita bisa pastikan bahwa $P_{prev}$ ini sudah mendapatkan sinyal dari radar yang pernah kita taruh.
- Apabila $prev \geq pos$ dapat terjadi beberapa hal:
    - Apabila nilai $P_i$ ini belum ada pada $S$:
        - Ketika $prev=-1$ artinya $P_i$ belum terkena sinyal dari radar manapun, maka bisa kita tambahkan nilai $P_i$ ke dalam $S$
        - Ketika $prev\neq -1$ artinya $P_{prev}$ belum terkena sinyal dari radar manapun, artinya perlu kita tambahkan nilai $P_{prev}$ ke dalam $S$.
        - Karena $P_i=P_{prev}$ artinya dikasus ini kita akan selalu menambahkan nilai $P_i$ ke dalam $S$.
    - Apabila nilai $P_i$ ini sudah ada dalam $S$:
        - Kita sudah harus taruh radar baru dipesawat ini, yakni kita *set* $pos=i$.
            - Dengan cara ini, maka $P_i$ dan $P_{prev}$ (apabila $prev \neq -1$) dapat dikenakan oleh radar baru ini.
        - Karena kita menambah radar baru, kita tambahkan jawaban atau *set* $ans = ans + 1$
        - Disini dapat dipastikan bahwa semua nilai pesawat $P$ dalam $S$ sudah terkena oleh radar baru ini, oleh karena itu kita perlu kosongkan $S$.
- Terakhir kita perlu cek apakah $S$ kosong atau tidak, **apabila tidak kosong** maka kita perlu tambah satu radar baru, sehingga kita tambahkan jawaban atau *set* $ans = ans + 1$

Dengan cara tersebut, dipastikan bahwa kita akan mendapatkan nilai minimal dalam menaruh radar.

Untuk lebih mudah dalam memahami algoritma tersebut, Anda dapat melihat *solution code* dibawah.

Kompleksitas Waktu: $O(N \log N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  cout.tie(0);

  int n;
  cin >> n;
  map<pair<int, int>, int> mp;
  set<pair<int, int>> st;
  int ans = 0;
  int pos = -1;
  for (int i = 0; i < n; i++) {
    int t, v;
    cin >> t >> v;
    pair<int, int> cur = make_pair(t, v);
    int prev = mp.count(cur) > 0 ? mp[cur] : -1;
    if (prev >= pos) {
      if (st.count(cur) > 0) {
        ++ans;
        pos = i;
        st.clear();
      } else {
        st.insert(cur);
      }
    }
    mp[cur] = i;
  }
  if (!st.empty()) {
    ++ans;
  }
  cout << ans << '\n';

  return 0;
}
```
</details>

## Komentar
- Soal-soal seperti ini memang membutuhkan banyak observasi dan percobaan dalam mengerjakan-nya
- Setelah mendapatkan beberapa observasi penting, kita bisa mendefinisikan beberapa hal yang kira-kira akan membantu kita dalam menyelesaikan soal (Dalam kasus penjelasan soal yang didefinisikan adalah $pos$, $S$, dan $prev$)