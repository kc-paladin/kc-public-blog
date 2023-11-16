# [I. Tebak Angka](https://tlx.toki.id/courses/competitive/chapters/13/problems/I)

Author: Joceline Araki

Soal ini merupakan soal _interaktif_. Berbeda dengan soal biasa (input lalu output), soal tipe ini mengharuskan kita untuk berinteraksi dengan program juri. Di soal ini, program juri memiliki sebuah angka $X$ yang harus berhasil ditebak tanpa melakukan lebih dari $10$ tebakan. Kita akan menebak suatu angka $Y$, dan juri akan menjawab sesuai dengan kondisi yang berlaku, yaitu:
- `terlalu kecil` apabila $X > Y$
- `terlalu besar` apabila $X < Y$
- `selamat` apabila $X = Y$

Kita bisa menyelesaikan problem ini dengan menggunakan _binary search_. Batas kiri (`L`) nya adalah $A$, dan batas kanan (`R`) nya adalah $B$. Angka yang kita tebak adalah nilai tengah (`mid`) dari $L$ dan $R$. Kita akan menggeser nilai $L$ dan $R$ sesuai dengan output juri, yaitu:
- Geser ke kiri apabila angka tebakan kita sekarang `terlalu besar`
- Geser ke kanan apabila angka tebakan kita sekarang `terlalu kecil`
- Hentikan proses binary searchnya apabila tebakan kita sudah benar (`selamat`)

Solusi binary search ini dijamin memenuhi syarat tidak boleh menebak lebih dari $10$ kali karena _worst case_ pada soal ini adalah $A = 1$ dan $B = 30$, yang berarti kita akan melakukan binary search di $30$ angka. Ingat bahwa _time complexity_ dari binary search adalah $O(log N)$. Berarti untuk worst casenya, diperlukan paling banyak $log(30) \approx 5$ kali tebakan.

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int ask(int x) {
  cout << x << endl;  // tebak angka x
  string s;
  getline(cin, s);
  if (s == "terlalu kecil") return 1;
  if (s == "terlalu besar") return 2;
  return 3;
}

int main() {
  int l, r;
  cin >> l >> r;
  cin.ignore();  // abaikan baris kosong yang ada setelah input A dan B (l dan r)
  while (l <= r) {
    int mid = (l + r) / 2;
    int tmp = ask(mid);
    if (tmp == 1) {  // jika jawaban juri "terlalu kecil"
      l = mid + 1;
    } else if (tmp == 2) {  // jika jawaban juri "terlalu besar"
      r = mid - 1;
    } else {  // jika jawaban juri "selamat"
      break;
    }
  }

  return 0;
}
```
</details>


## Komentar
    
- Di soal interaktif, output kita bisa saja tidak langsung diberikan ke "interactor" (dapat memberikan verdict TLE atau WA). Untuk menghindari hal ini, kita harus menggunakan operasi `flush` setiap kali kita mengoutput suatu data. Di C++, kita bisa menggunakan `cout << endl;` karena `endl` akan mem-flush output tiap kali dipanggil. Menggunakan `cout << '\n'` untuk mencetak baris baru tidak direkomendasikan karena operasinya tidak akan mem-flush outputnya. Flush ini adalah alasan mengapa operasi `cout << '\n'` lebih cepat daripada `cout << endl;`.


## Materi Yang Berhubungan
    
- [Guide for Interactive Problems](https://codeforces.com/blog/entry/45307)
- [Binary Search - GFG](https://www.geeksforgeeks.org/binary-search/)
- [Perbedaan endl dan \n di C++](https://codeforces.com/blog/entry/43780#:~:text=Endl%20is%20actually%20slower%20because,%5Cn%20'%20instead%20of%20endl.)