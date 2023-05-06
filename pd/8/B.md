# [B. Cek Bilangan Prima](https://tlx.toki.id/courses/basic/chapters/08/problems/B)

Author: Yazid Aqila Haikal

Haloo.. !! 👋

Sekarang kita telah memasuki materi *kompleksitas* ✨. Kira-kira bakal sekompleks itu kah materi ini??

Jadi, di [soal ini](https://tlx.toki.id/courses/basic/chapters/08/problems/B) kita akan menganalisis *kompleksitas* suatu program 🙌.

<details>
  <summary>Apa sih "kompleksitas"?</summary>

*Kompleksitas* adalah tingkat kerumitan suatu program, yang dimana semakin rumit programnya, maka kompleksitas program tersebut semakin besar.
</details>

<details>
  <summary>Notasi O Besar [Big-O Notation]</summary>

*Notasi O Besar* atau *Big-O Notation* adalah sebuah cara atau metode untuk melakukan analisa terhadap waktu serta memori sebuah algoritma pemrograman.

Untuk penjelasan lebih lengkap:
- [Big-O Notation: A Simple Explanation with Examples](https://betterprogramming.pub/big-o-notation-a-simple-explanation-with-examples-a56347d1daca) 
</details>

## Penjelasan Soal

Soal ini meminta kita untuk membantu Pak Dengklek menentukan dari $N$ bilangan yang dimilikinya, yang mana saja yang merupakan bilangan prima dan yang bukan bilangan prima.

<details>
  <summary>Solusi Soal</summary>

<details>
  <summary>💡 <b>Ide Solusi yang Kurang Tepat</b> ❎</summary>

1. Buat perulangan sebanyak $N$ kali, karena kita diminta untuk mengecek $N$ bilangan.
2. Tambahkan variabel baru untuk setiap bilangan yang akan dimasukkan dan satu boolean untuk menjadi penentu apakah bilangan tersebut prima atau bukan.
3. Periksa, apakah bilangan tersebut merupakan angka *1* atau bukan, karena angka *1* bukanlah bilangan prima.
4. Karena bilangan prima hanya dapat habis dibagi 1 dan bilangan itu sendiri. Buat perulangan, yang dimana akan di cek apakah bilangan tersebut habis dibagi 2 hingga angka sebelum bilangan tersebut.
5. Kalau ternyata ada yang membagi habis, booleannya jadi false, lalu di *break* agar tidak lanjut lagi.
6. Periksa, apakah booleannya *true* atau *false*. Kalau true, keluarkan "YA" dan kalau false, keluarkan "BUKAN"
7. Nah, habis itu udaaah 😇✨.

```c++
#include <iostream>
using namespace std;

int main(){
	int N;
	cin >> N;
	
	for(int i = 0; i < N; i++){
		int A;
		bool B = true;
		cin >> A;
		
		if(A == 1){
			cout << "BUKAN" << endl;
		}else{
			for(int j = 2; j < A; j++){
				if(A % j == 0){
					B = false;
					break;
				}
			}
			if(B){
    			cout << "YA" << endl;
    		}else{
    			cout << "BUKAN" << endl;
    		}
		}
	}
}
```
Kompleksitas Waktu: $O(N×A)$

Kompleksitas Memori: $O(1)$

Verdict: TLE (Time Limit Exceeded)

Verdictnya menjadi "TLE" dikarenakan proses untuk menjalankan program tersebut melebihi batas waktu yang telat ditentukan.
</details>

<details>
  <summary>💡 <b>Ide Solusi yang Tepat</b> ✅</summary>

*Note: Perbedaan terdapat pada poin ke 5*

1. Buat perulangan sebanyak $N$ kali, karena kita diminta untuk mengecek $N$ bilangan.
2. Tambahkan variabel baru untuk setiap bilangan yang akan dimasukkan dan satu boolean untuk menjadi penentu apakah bilangan tersebut prima atau bukan.
3. Periksa, apakah bilangan tersebut merupakan angka *1* atau bukan, karena angka *1* bukanlah bilangan prima.
4. Karena bilangan prima pasti tidak habis dibagi 2 hingga akar dari bilangan tersebut. Buat perulangan, yang dimana akan di cek apakah bilangan tersebut habis dibagi 2 hingga akar dari bilangan tersebut.
5. Kalau ternyata ada yang membagi habis, booleannya jadi false, lalu di *break* agar tidak lanjut lagi.
6. Periksa, apakah booleannya *true* atau *false*. Kalau true, keluarkan "YA" dan kalau false, keluarkan "BUKAN"
7. Nah, habis itu udaaah 😇✨.

```c++
#include <iostream>
#include <cmath>
using namespace std;

int main(){
	int N;
	cin >> N;
	
	for(int i = 0; i < N; i++){
		int A;
		bool B = true;
		cin >> A;
		
		if(A == 1){
			cout << "BUKAN" << endl;
		}else{
			for(int j = 2; j < sqrt(A); j++){
				if(A % j == 0){
					B = false;
					break;
				}
			}
			if(B){
    			cout << "YA" << endl;
    		}else{
    			cout << "BUKAN" << endl;
    		}
		}
	}
}
```
Kompleksitas Waktu: $O(N×\sqrt{A})$

Kompleksitas Memori: $O(1)$

Verdict: AC (Accepted)

Verdictnya menjadi "AC" sehingga kita bisa lanjut mengerjakan soal berikutnya! 🥳
</details>
</details>

## Komentar
    
- Dari kedua solusi diatas, kita bisa lihat bahwa sebenarnya kedua ide solusi tersebut benar. Namun, ide kedua lebih efisien daripada ide pertama 😊. Sehingga, dapat disimpulkan bahwa dalam programming, kompleksitas dari program yang kita buat sangatlah perlu untuk kita perhatikan ✨.

## Materi Yang Berhubungan

- [Analisis Kompleksitas](https://docs.google.com/viewerng/viewer?url=https://github.com/ia-toki/training-gate-id-pdf/raw/master/pemrograman-dasar-cpp_08-analisis-kompleksitas.pdf)    
- [Big-O Notation: A Simple Explanation with Examples](https://betterprogramming.pub/big-o-notation-a-simple-explanation-with-examples-a56347d1daca) 
- [Notasi O Besar atau Big-O Notation](https://rizafahmi.com/2020/03/21/notasi-o-besar-big-o-notation/)