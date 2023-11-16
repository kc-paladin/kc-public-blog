# [F. Waterfall](https://tlx.toki.id/courses/competitive/chapters/07/problems/F)

Author : Arnold Ardianto

Hai teman-teman! 👋

Di blog kali ini ayo kita sama sama belajar cara menge-solve soal _waterfall_. Aku saranin kamu baca soalnya dulu ya di link yang ada diatas 👆

Kalau sudah ayo kita lihat cara penyelesaiannya

**Observasi 1**

> Apabila ada suatu titik air yang mulai jatuh dari petak $(r, c)$, maka titik air itu akan bergerak ke arah ke bawah sampai menabrak suatu batu. Atau secara formal bergerak dengan arah : $(r+1, c), (r+2, c), ..., (r', c)$ dimana $(r'+1, c)$ adalah petak terdekat yang berisi sebuah batu

**Observasi 2**

> Setelah air tersebut menabrak batu, pecahan air akan tersebar ke kiri dan ke kanan selama titik pecahan air tersebut berada di atas batu. Kemudian setelah titik sudah tidak ada lagi berada di atas batu, maka air akan mulai jatuh dari petak baru. Atau secara formal : <br>
<br>
$(r', c-1), (r', c-2), ..., (r', c')$ dan <br>
$(r', c+1), (r', c+2), ..., (r', c'')$ <br>
<br>
dimana $(r'+1, c')$ dan $(r'+1, c'')$ adalah petak terdekat dari titik tabrak yang di bawahnya bukan batu

Perhatikan ilustrasi berikut : 
<details>
<summary>Ilustrasi Waterfall</summary>
<img src="https://im.ezgif.com/tmp/ezgif-1-3191112a9b.gif"/>
</details>

Kita bisa melihat kalau air tersebut berpindah dari titik $(r, c)$ ke titik : 
- $(r', c')$
- $(r', c'')$

Lalu jumlah tabrakan / gemerciknya bertambah $1$

Kita bisa melihat bahwa disini ada "sub-problem" baru dimana airnya sama sama jatuh tapi kali ini jatuhnya dimulai dari titik jatuh yang berbeda. Approach apa yang bisa kita _pake_ kalau kita ingin menyelesaikan sub-problem yang mirip? Yak betul! DP!

Karena itu mari kita definisikan fungsi DP kita : 

> $dp(r, c)$ : Banyak tabrakan yang terjadi jika air mulai dijatuhkan dari titik $(r, c)$

Dari dua observasi diatas, kita bisa memperoleh : 

- **Base Case** <br>
  - Jika $r > V$ maka $dp(r, c) = 0$ (titik air sudah berada di luar grid)
  - Jika $c < 1$ atau $c > H$ maka $dp(r, c) = 0$ juga

- **Transisi** <br>
  Untuk suatu titik $(r, c)$, cari dua titik pemecahan air (sesuai observasi 1 dan 2 diatas) maka : 
  - $dp(r, c) = dp(r', c') + dp(r', c'') + 1$

🙋 : _Terus gimana kak supaya tau tabrakan maksimal yang mungkin?_

Nah disini kita bisa memilih mau menjatuhkan airnya dari titik mana. Artinya kita akan memilih suatu titik jatuh yang menghasilkan banyak tabrakan termaksimal yang bisa dibentuk. Atau secara formal, jawaban dari persoalan ini adalah : 

> $\max(dp(0, 1), dp(0, 2), ..., dp(0, H))$


**Kompleksitas Waktu:**

Untuk menghitung kompleksitas waktu dalam DP, kita bisa menghitung banyak state dikali dengan banyak transisi. Karena banyak state yang mungkin adalah $VH$ (seukuran dengan grid) dan untuk setiap titik kita akan menggerakan titik air sebanyak $V$ ke bawah atau sebanyak $H$ ke kiri dan kanan, maka pergerakan titik adalah $V+H$. Sehingga kompleksitas keseluruhannya adalah : 

$O(VH + (V+H))$

**Kompleksitas Memori:**

Banyak memori yang digunakan sama dengan ukuran array yang digunakan untuk DP sehingga kompleksitasnya adalah :

$O(VH)$

**Gotcha:**

Diketahui banyak tabrakan yang terjadi paling banyak adalah $10^{15}$, jadi jangan lupa _pake_ tipe data `long long` ya untuk menyimpan jawabannya 😏

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

long long C, R, n;
bool batu[505][505];
long long memo[505][505];

long long dp(long long r, long long c) {
  if (r > R || c < 1 || c > C) return 0;
  if (memo[r][c] != -1) {
    return memo[r][c];
  }

  int nxtr = r;
  while (nxtr <= R && !batu[nxtr + 1][c]) nxtr++;

  long long res = 0;
  res += batu[nxtr + 1][c];

  long long cnext = c;
  while (cnext > 0 && batu[nxtr + 1][cnext]) cnext--;
  res += dp(nxtr, cnext);

  cnext = c;
  while (cnext <= C && batu[nxtr + 1][cnext]) cnext++;
  res += dp(nxtr, cnext);

  return memo[r][c] = res;
}

int main() {
  cin >> R >> C >> n;

  memset(batu, false, sizeof(batu));
  memset(memo, -1, sizeof(memo));

  for (long long i = 1; i <= n; i++) {
    long long top, left, bot, right;
    cin >> top >> left >> bot >> right;
    for (long long r = top; r <= bot; r++) {
      for (long long c = left; c <= right; c++) {
        batu[r][c] = true;
      }
    }
  }

  long long ans = 0;
  for (long long c = 1; c <= C; c++) {
    ans = max(ans, dp(0, c));
  }
  cout << ans;
}
```

</details>