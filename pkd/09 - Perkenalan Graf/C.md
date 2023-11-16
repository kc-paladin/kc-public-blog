# [C. Evolusi](https://tlx.toki.id/courses/competitive/chapters/09/problems/C)

Author: Joceline Araki

Prerequisite: DFS

Sebenarnya, soal ini hanya meminta kita untuk mencetak _path_ atau jalur dari suatu node $A$ ke node $B$ atau sebaliknya. Tapi disini, masalah yang kita hadapi adalah node yang diberikan bukanlah angka, tapi string! Untuk mengakali hal ini, kita bisa menggunakan struktur data `map`.

Penjelasan map secara singkat (kalau udah tau bagian ini boleh diskip):
Cara declare map: `map<tipe_data_key, tipe_data_value>[nama variabel]`  

Intinya, map punya $2$ komponen, yaitu `key` dan `value`. Key dan value ini bisa berupa tipe data apapun. Kita bisa memberikan suatu value kepada setiap key. Key ini hanya "menunjuk" ke satu value saja. Anggap aja map itu array tapi lebih keren :D Kita bisa anggap keynya sebagai "index" dari array, dan valuenya sebagai nilai yang tersimpan di index tersebut. Cara akses map pun sama dengan cara akses array.

Cara akses map: `m[key]` dimana m itu nama mapnya

Nah kalau gitu, kita bisa buat adjacency list dalam bentuk map `map<string, vector<string>>adj`, dimana keynya adalah nama spesiesnya dan valuenya adalah spesies yang terhubung langsung dengan keynya.

Untuk output dari soal ini, kita cukup jalankan DFS dari $A$ ke $B$. Jika ada path yang valid, maka print path tersebut. Jika tidak, maka kita harus coba DFS dari $B$ ke $A$ (sebaliknya). Jika masih tidak ada path yang valid, maka outputnya adalah `"TIDAK MUNGKIN"`.

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

map<string, vector<string>> adj;
vector<string> ans;

bool dfs(string cur, string goal) {
  if (cur == goal) return true;

  bool connected = false;
  for (auto &nxt : adj[cur]) {
    connected |= dfs(nxt, goal);

    if (connected) {
      ans.push_back(nxt);
      return true;
    }
  }

  return false;
}

int main() {
  int n, m;
  cin >> n >> m;
  string p, c;

  for (int i = 0; i < m; i++) {
    cin >> p >> c;
    adj[p].push_back(c);
  }

  string a, b;
  cin >> a >> b;

  bool tmpA = dfs(a, b);
  bool tmpB = dfs(b, a);

  if (tmpA) {
    cout << a << '\n';
    for (int i = ans.size() - 1; i >= 0; i--) cout << ans[i] << '\n';
  } else if (tmpB) {
    cout << b << '\n';
    for (int i = ans.size() - 1; i >= 0; i--) cout << ans[i] << '\n';
  } else {
    cout << "TIDAK MUNGKIN" << '\n';
  }

  return 0;
}
```
</details>

## Materi Yang Berhubungan

- [GeeksForGeeks - Introduction to map data structure](https://www.geeksforgeeks.org/introduction-to-map-data-structure-and-algorithm-tutorials/)
- [GeeksForGeeks - Map in C++](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)
