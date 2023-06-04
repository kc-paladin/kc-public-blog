# [Kasur Rusak](https://tlx.toki.id/courses/basic/chapters/12/problems/D)

Author: Hamiz Ghani

Pada soal ini kita akan menerima suatu string $S$. Kita akan menentukan apakah $S$ merupakan string palindrome atau bukan. Kita dapat cek untuk setiap karakter $S[i], 1≤i≤S.length()/2$ dan membandingkannya dengan $S[(S.length()-i)-1]$. Apabila ditemukan $i$ dimana $S[i]≠S[(s.length()-i)-1]$ maka dipastikan string tersebut bukan merupakan string palindrom. 
```c++
bool palindrome = true;
    for (int i = 0; i <= s.length() / 2; i++) {
        if (s[i] != s[(s.length() - i) - 1]) {
            palindrome = false;
        }
    }
```
Dalam pseudocode di atas $palindrome$ merupakan tipe data $bool$ yang akan bernilai $1$ apabila string tersebut merupakan bilangan palindrome dan bernilai $0$ jika sebaliknya.

Kompleksitas Waktu: $O(s.length()/2)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>
using namespace std;
string s;
main()
{
    cin >> s;
    bool palindrome = 1;
    for (int i = 0; i <= s.length() / 2; i++) {
        if (s[i] != s[(s.length() - i) - 1])
            palindrome = 0;
    }
    if (palindrome)
        cout << "YA" << endl;
    else
        cout << "BUKAN" << endl;
}
```
</details>



<!-- Tambahkan komentar apabila perlu
-->
## Komentar
    
- `length()` merupakan fungsi bawaan dari C++ untuk mengetahui panjang string


<!-- Tambahkan referensi link materi yang berhubungan apabila perlu

## Materi Yang Berhubungan
    
-  [swap() in C++](https://www.geeksforgeeks.org/swap-in-cpp/)
-->

<!-- Tambahkan referensi link soal yang berhubungan apabila perlu
-->
## Soal Yang Berhubungan
    
- [Déjà Vu - Codeforces 1504A](https://codeforces.com/problemset/problem/1504/A)
