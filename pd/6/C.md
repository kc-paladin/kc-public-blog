# [C. While](https://tlx.toki.id/courses/basic/chapters/06/problems/C)

Author: Yose Yehezkiel Maranata

While loop adalah salah satu metode perulangan yang sering digunakan di dalam pemrograman. 

```
while(<condition>){
    //action
}
```
while loop akan berulang-ulang melakukan aksi yang terdapat pada kurung kurawal {...}, apabila ```<condition>``` bernilai ```true```, dan berhenti apabila ```<condition>``` bernilai ```false```.

```getline(cin,s)``` akan mengembalikan nilai ```true``` apabila berhasil membaca sebuah baris. Dengan memanfaatkan properti ini kita bisa membuat while loop dengan ```getline(cin,s)``` pada ```<condition>```nya.

Kompleksitas Waktu: $O(N)$ 

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  string s;
  while (getline(cin, s)) {
    cout << s << endl;
  }
}
```
</details>



## Komentar
    
- Apabila anda menggunakan interactive console untuk menjalankan code tersebut, code tersebut tidak akan berhenti karena sifatnya interaktif dan program akan menunggu interaksi anda yang memasukan string.   
- ```getline(cin,s)``` bernilai false apabila mencapai end of file atau ```EOF```. Tidak ```EOF``` pada interactive console, sedangkan ```while(getline(cin,s))``` akan terus menerus membaca string hingga ```EOF```.



## Materi Yang Berhubungan
    
- [C++ While loop](https://www.w3schools.com/cpp/cpp_while_loop.asp)

