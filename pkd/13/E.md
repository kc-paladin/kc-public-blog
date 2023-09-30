# [Sang Pelompat](https://tlx.toki.id/courses/competitive/chapters/13/problems/E)

Author: Hamiz Ghani

Diberikan $N × M$ buah grid, masing-masing grid berisi antara batu (#) atau lautan magma yang tidak boleh dikunjungi (.). Kita akan menentukan berapa lompatan minimum yang diperlukan dari $S$ ke $C$ dengan ketentuan yang sudah ditulis dalam soal.

Kali ini, kita akan menggunakan algrotima djikstra yang didefinisikan sebagai berikut :
```c++
pq<{dis,{x,y}}>
```
dimana jarak lompatan yang diperlukan untuk mencapai grid $(x,y)$ dari titik mulai adalah sebanyak $dis$. Pada awalnya tentu kita akan melakukan push titik start itu sendiri.

note : `priority_queue` saya sudah dimodifikasi sehingga nilai terkecil berada di top.

Untuk setiap batu yang dikunjungi, lakukan looping ke arah atas, kiri, kanan dan bawah untuk melakukan pengecekan pada masing-masing grid. Definisikan $jump$ menyimpan banyak lompatan untuk sampai ke grid tujuan. Untuk suatu grid yang terhubung langsung dengan batu, dapat kita simpulkan nilai $jump=0$. Selain itu, kita hanya akan mencari grid pertama dengan $jump=1$, karena, grid setelahnya dapat dicari dari grid tersebut. Jangan lupa untuk menyimpan $visited$ masing-masing grid sehingga kita tidak akan memproses grid yang sudah pernah diproses.

Untuk setiap grid pada looping, lakukan : 
```c++
pq.push(dis+jump,{x,y});
```

Apabila titik harta karun tidak ditemukan pada proses djikstra, maka kita akan mengeluarkan `-1`.

Kompleksitas Waktu: $O(N*M)$

Kompleksitas Memori: $O(1)$

<details>
  <summary>Solution Code</summary>

```c++
#include<bits/stdc++.h>
#define pqueue priority_queue
#define fi first
#define se second
#define int long long
#define pii pair<int,int>
using namespace std;
int n,m;
pii st,ed;
pqueue<pair<int,pii>,vector<pair<int,pii>>,greater<pair<int,pii>>> pq;
char c[1005][1005];
bool vis[1005][1005];
main(){
	string s; cin>>s;
	cin>>n>>m;
	for(int i=1;i<=n;i++){
		for(int j=1;j<=m;j++){
			cin>>c[i][j];
			if(c[i][j]=='T'){
				ed.fi=i;
				ed.se=j;
			}
			else if(c[i][j]=='S'){
				pq.push({0,{i,j}});
			}
		}
	}
	while(!pq.empty()){
		int dis=pq.top().fi;
		int pr=pq.top().se.fi;
		int pc=pq.top().se.se;
		pq.pop();
		if(vis[pr][pc]) continue;
		vis[pr][pc]=1;
		if(pr==ed.fi&&pc==ed.se){
			cout<<dis<<endl;
			return 0;
		}
		//atas
		int jump=0;
		for(int i=pr-1;i>=1;i--){
			if(c[i][pc]=='.') jump=1;
			else{
				if(vis[i][pc]) break;
				pq.push({dis+jump,{i,pc}});
				break;
			}
		}
		//kiri
		jump=0;
		for(int i=pc-1;i>=1;i--){
			if(c[pr][i]=='.') jump=1;
			else{
				if(vis[pr][i]) break;
				pq.push({dis+jump,{pr,i}});
				break;
			}
		}
		//kanan
		jump=0;
		for(int i=pc+1;i<=m;i++){
			if(c[pr][i]=='.') jump=1;
			else{
				if(vis[pr][i]) break;
				pq.push({dis+jump,{pr,i}});
				break;
			}
		}
		//bawah
		jump=0;
		for(int i=pr+1;i<=n;i++){
			if(c[i][pc]=='.') jump=1;
			else{
				if(vis[i][pc]) break;
				pq.push({dis+jump,{i,pc}});
				break;
			}
		}
	}
	cout<<-1<<endl;
	return 0;
}
```
</details>



<!-- Tambahkan komentar apabila perlu

## Komentar
    
- Komentar I
- Komentar II

-->

<!-- Tambahkan referensi link materi yang berhubungan apabila perlu
-->
## Materi Yang Berhubungan
    
-  [Djikstra Algortihm](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)


<!-- Tambahkan referensi link soal yang berhubungan apabila perlu

## Soal Yang Berhubungan
    
- [Nama Soal 1](link-soal)
- [Nama Soal II](link-soal)

-->