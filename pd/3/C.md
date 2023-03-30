# [C. Burung Beo](https://tlx.toki.id/courses/basic/chapters/03/problems/C)

Author: Eileen Camelia Limneus

Sebelum menyelesaikan persoalan ini, apakah teman - teman sudah mengetahui apa itu fungsi `getline` di C++? Kalau belum, boleh cek link yang ada di bawah ya!

Secara singkat, fungsi `getline` ini digunakan untuk membaca input dari pengguna dalam satu baris atau lebih hingga muncul karakter khusus (delimiter).

Jadi, kita bisa mengaplikasikan fungsi ini ke persoalan tersebut untuk menyelesaikannya.

Kompleksitas Waktu: $O(N)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  string s;
  getline(cin, s);
  cout << s;
}
```
</details>

## Komentar
    
- `cin` hanya membaca input sampai menemukan karakter whitespace (spasi, tab, newline), sedangkan `getline` membaca input hingga menemukan karakter newline (enter).

## Materi Yang Berhubungan
    
- https://www.geeksforgeeks.org/getline-string-c/
- https://www.geeksforgeeks.org/cin-in-c/
- https://www.geeksforgeeks.org/problem-with-getline-after-cin/

