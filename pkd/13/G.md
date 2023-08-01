# [G. Jawbreaker V: Cari Optimal](https://tlx.toki.id/courses/competitive/chapters/13/problems/G)

Author: Yose Yehezkiel Maranata 

Halo semua! :D

Di blog ini kita akan membuat AI yang lebih canggih **LAGI** untuk permainan JawBreaker! **OMGG!**

Pastikan kalian `AC` soal [Jawbreaker IV: Cari Terbesar 2 Langkah](https://tlx.toki.id/courses/competitive/chapters/04/problems/G) dan sudah mengerti konsep dari **floodfill(menggunakan BFS atau DFS)** dan **backtracking**. 

Soal ini adalah soal implementasi, idenya mudah namun implementasi terkadang akan stuck. Jangan cepat menyerah, sabar dalam implementasi supaya kalian makin terlatih implementasinya. 

Kunci dari soal ini adalah melakukan bruteforce pada setiap kemungkinan pemilihan, salah satu cara termudahnya menggunakan backtracking. Untuk memilih setiap kemungkinannya kalian tinggal menggunakan floodfill saja, apabila sudah belajar BFS implementasi kalian akan lebih clean, namun DFS pun tidak apa-apa. Apabila ingin latihan lebih lagi kalian boleh coba 22nya DFS dan BFS :D. 

Kompleksitas Waktu: $O(7! \times N \times M)$

Kompleksitas Memori: $O(7! \times N \times M)$

<details>
  <summary>Solution Code DFS</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int n, m;

int dr[4] = {0,0,1,-1};
int dc[4] = {1,-1,0,0};

bool inside(int x, int y) {
    return x>=0&&x<n&&y>=0&&y<m;
}

void klik(int i, int j, int warna, vector<vector<int>> &grid, vector<vector<bool>> &vis, int &tot) {
    vis[i][j] = 1;
    grid[i][j] = 0 ;
    tot++;
    
    for(int k=0;k<4;k++) {
        int tr = i+dr[k], tc = j+dc[k];
        if(!inside(tr,tc)) continue;
        if(vis[tr][tc]) continue;
        if(grid[tr][tc]!=warna) continue;
        klik(tr, tc, warna, grid, vis, tot);
    }
    return;
}

int coba(vector<vector<int>> grid) {
    vector<vector<int>> temp = grid;
    vector<vector<bool>> vis(n, vector<bool>(m, 0));
    int ans = 0;

    //runtuh
    for(int j=0;j<m;j++) {
        int prev = -1; 
        for(int i=n-1;i>=0;i--){
            if(prev == -1 && grid[i][j] == 0 ) prev = i;
            else if(prev != -1 && grid[i][j] != 0) {    
                grid[prev][j] = grid[i][j];
                grid[i][j] = 0;
                prev--;
            }
        }
    }

    for(int i=0;i<n;i++) {
        for(int j=0;j<m;j++) {
            if(grid[i][j] == 0) continue;
            if(vis[i][j]) continue;
            vector<vector<int>> temp  = grid;
            int warna = grid[i][j];
            int totalKlik = 0;
            klik(i, j, warna, temp, vis, totalKlik);
            if(totalKlik>1) {
                ans = max(ans, totalKlik*(totalKlik-1) + coba(temp));
            }
        }
    }
    return ans; 
}

int32_t main() {
    ios_base::sync_with_stdio(0); cin.tie(0);
    cin >> n >> m;
    vector<vector<int>> grid(n, vector<int>(m));
    for(int i=0;i<n;i++) {
        for(int j=0;j<m;j++) cin >> grid[i][j];
    }
    int ans = coba(grid);
    cout << ans << endl;
}
```
</details>
<details>
  <summary>Solution Code BFS</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

int n, m;

int dr[4] = {0,0,1,-1};
int dc[4] = {1,-1,0,0};

bool inside(int x, int y) {
    return x>=0&&x<n&&y>=0&&y<m;
}

int coba(vector<vector<int>> grid) {
    vector<vector<int>> temp = grid;
    vector<vector<bool>> vis(n, vector<bool>(m, 0));
    int ans = 0;

    //runtuh
    for(int j=0;j<m;j++) {
        int prev = -1; 
        for(int i=n-1;i>=0;i--){
            if(prev == -1 && grid[i][j] == 0 ) prev = i;
            else if(prev != -1 && grid[i][j] != 0) {
                grid[prev][j] = grid[i][j];
                grid[i][j] = 0;
                prev--;
            }
        }
    }

    for(int i=0;i<n;i++) {
        for(int j=0;j<m;j++) {
            if(vis[i][j]) continue;
            if(grid[i][j]==0) continue;
            temp = grid; // copy grid to temp
            int angka = grid[i][j];

            //bfs
            queue<pair<int,int>> q;
            q.push({i,j});
            int totalKlik = 0;
            while(!q.empty() ) { 
                pair<int,int> u = q.front(); q.pop();
                int x = u.first, y=u.second;
                if(vis[x][y]) continue;
                if(temp[x][y] != angka) continue;
                vis[x][y] = 1;
                temp[x][y] = 0;
                totalKlik++;
                for(int l=0;l<4;l++) {
                    int tr = x + dc[l], tc = y+dr[l];
                    if(!inside(tr,tc)) continue;
                    if(temp[tr][tc] != angka) continue;
                    if(vis[tr][tc]) continue;
                    q.push({tr,tc});
                }
            }
            // minimal bola harus lebih dari satu
            if(totalKlik>1) {
                ans = max(ans, totalKlik*(totalKlik-1) + coba(temp));
            }
        }
    }
    return ans;
}

int32_t main() {
    ios_base::sync_with_stdio(0); cin.tie(0);
    cin >> n >> m;
    vector<vector<int>> grid(n, vector<int>(m));
    for(int i=0;i<n;i++) {
        for(int j=0;j<m;j++) cin >> grid[i][j];
    }
    int ans = coba(grid);
    cout << ans << endl;
}
```
</details>

## Komentar
    
- Total kemungkinan yang bisa di dapat mencapai $7!$, karena dijamin bahwa dengan urutan pengambilan apapun, paling banyak hanya dibutuhkan 7 langkah pengambilan sampai permainan selesai. Total Kompleksitas waktu dan memori kita adalah $O(7! \times N \times M)$


