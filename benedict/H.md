# [H. Paduan Suara](https://tlx.toki.id/courses/competitive/chapters/04/problems/H)

Author: Benedict Presley

Pertama-tama, dapat kita temukan bahwa setiap grup memiliki setidaknya $\left\lfloor \dfrac{M}{N} \right\rfloor$ anggota dan paling banyak $\left\lfloor \dfrac{M}{N} \right\rfloor + 1$ anggota, dengan :$\left\lfloor \dfrac{M}{N} \right\rfloor$ adalah nilai $M$ dibagi $N$ dibulatkan ke bawah (fungsi floor).

Mari kita sebut grup dengan $\left\lfloor \dfrac{M}{N} \right\rfloor + 1$ anggota sebagai "grup berlebih". Perhatikan bahwa jumlah "grup berlebih" ada sebanyak $M \; \text{mod} \; N$ grup atau dengan kata lain, sisa bagi $M$ dibagi $N$.

Sekarang bagaimana cara kita menentukan apakah suatu pembagian grup benar?

Sebut array yang berisi tinggi suara para bebek sebagai $S$. Jika kita mengurutkan array $S$ dari kecil ke besar, kemudian kita memilih suatu indek $i$ dan meletakkan pembatas dengan nilai $S[i] + 1$, maka semua indeks dari $1$ hingga $i$ akan termasuk dalam 1 kelompok. Begitu pula bila kita memilih pembatas kedua, ketiga, dan seterusnya. Suatu pembatas disebut benar jika dan hanya jika nilai $S[i]$ dan $S[i+1]$ berbeda. Bila nilainya sama, mereka akan berada pada grup yang sama sehingga pembatas tidak dapat diletakkan di sana.

Kita sudah tahu bagaimana cara memilih pembatas yang valid. Untuk menyelesaikan soal ini, kita harus memilih indeks-indeks yang akan dijadikan pembatas, lalu mengeluarkan nilai pada indeks-indeks tersebut ditambah $1$. Karena nilai $N$ kecil ($N \leq 20$), maka kita dapat mengecek setiap kemungkinan memilih "grup berlebih".

Kompleksitas Waktu: $O(2^N)$

Kompleksitas Memori: $O(M + N)$

<details>
  <summary>Solution Code</summary>

    #include<bits/stdc++.h>
    using namespace std;

    int suara[10001], tambah[20];
    int M, N, ukuran, sisa;

    bool rekursi(int posisi, int grup, int lebih){
        if(grup == N - 1){
            if(sisa - lebih <= 1){ //bisa saja grup terakhir yang berlebih
                return true;
            }
            return false;
        }

        if(suara[posisi + ukuran - 1] != suara[posisi + ukuran]){
            if(rekursi(posisi + ukuran, grup + 1, lebih)){
                return true;
            }
        }
        if(lebih < sisa){
            if(suara[posisi + ukuran] != suara[posisi + ukuran + 1]){
                tambah[grup] = 1;
                if(rekursi(posisi + ukuran + 1, grup + 1, lebih + 1)){
                    return true;
                }
                tambah[grup] = 0;
            }
        }
        return false;
    }

    int main(){
        ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);

        cin >> M;

        for(int i = 0; i < M; ++i){
            cin >> suara[i];
        }

        sort(suara, suara + M);

        //Kita memilih nilai suara[M] = 0 untuk memastikan nilai suara[M - 1] dan suara[M] tidak akan pernah sama.
        suara[M] = 0; //Bagian ini sebenarnya tidak diperlukan karena secara `default` nilai suara[M] adalah 0.

        cin >> N;

        ukuran = M / N;
        sisa = M % N;

        rekursi(0, 0, 0);

        int pos = 0;
        for(int i = 0; i < N - 1; ++i){
            pos += ukuran;
            if(tambah[i]){
                pos++;
            }
            cout << suara[pos - 1] + 1 << " ";
        }

        return 0;
    }

</details>

## Komentar

Terdapat banyak solusi untuk soal ini, contoh lainnya adalah menggunakan fungsi `next_permutation` dan mengecek semua kemungkinan memilih "grup berlebih". Namun pada dasarnya idenya tetap sama.