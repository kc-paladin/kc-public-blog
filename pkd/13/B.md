# [B. Tebak Himpunan](https://tlx.toki.id/courses/competitive/chapters/13/problems/B)

Author: Muhammad Hasan

Untuk soal ini, kita dapat melakukan solusi yang berbeda untuk beberapa subtask.

**Catatan:** Untuk setiap penyelesaian dibawah, apabila kita telah mendapatkan jawaban `ya`, harus langsung kita selesaikan program.

## Subtask $1$, $3$, $4$

Pada subtasks ini, $K=1$ dan kita bisa menyelesaikan persoalan ini dengan mencoba tebak satu-satu untuk setiap angka dari $1$ sampai $N$, apabila suatu bilangan $X$ dijawab `bisajadi` maka kita masukkan bilangan tersebut kedalam suatu list $S$.

Pada akhirnya bisa kita tanyakan $S$.

Kompleksitas Waktu: $O(N)$

Kompleksitas Memori: $O(N)$

## Subtask $5$

Kita dapat melakukan **Binary Search** untuk persoalan ini, kita akan mencoba mencari bilangan $X$ terbesar sedemikian sehingga apabila kita tanyakan $X$ maka akan dijawab `bisajadi` oleh *grader*.

Pada akhirnya kita cukup output $1, 2, \dots, X$.

Kompleksitas Waktu: $O(N)$

Kompleksitas Memori: $O(N)$

## Subtask $2$, $6$

Pada subtasks ini, $K=2$, perhatikan bahwa $Q = N^2$ (dan $Q > N^2$ untuk subtask $2$) salah satu cara menyelesaikan-nya adalah kita dapat melakukan query antar pair $(i, j)$ dengan $1 \leq i < j \leq N$.

Kemudian apabila hasil pair $(i, j)$ menghasilkan `tidak` maka kita bisa mark $i$ dan $j$ sebagai "Bad Numbers".

Kemudian kita bisa iterasi $X$ dari $1$ sampai $N$, dan kita masukkan $X$ kedalam list $S$ apbila $X$ bukan suatu "Bad Numbers".

Terakhir kita cukup output $S$, namun karena disini kita masih ada sisa $\displaystyle Q - \frac{N \times (N - 1)}{2}$ bisa kita coba output setiap $S'$ dimana $S' \in S$ dan $|S'| = |S| - 1$.

Kompleksitas Waktu: $O(N^2)$

Kompleksitas Memori: $O(N)$

<details>
  <summary>Solution Code</summary>

```c++
#include <bits/stdc++.h>

using namespace std;

string str;
int subsoal;
int n, k, q;

int ask(vector<int>& v) {
  int m = (int)v.size();
  assert(m > 0);
  cout << m << " ";
  for (int i = 0; i < m; i++) {
    cout << v[i];
    if (i + 1 < m) {
      cout << " ";
    } else {
      cout << endl;
    }
  }
  string ret;
  cin >> ret;
  if (ret == "tidak") {
    return 0;
  }
  if (ret == "bisajadi") {
    return 1;
  }
  assert(ret == "ya");
  return 2;
}

void solveForOne() {
  vector<int> S;
  for (int i = 1; i <= n; i++) {
    vector<int> v = {i};
    int cur = ask(v);
    if (cur == 2) {
      return;
    }
    if (cur == 1) {
      S.emplace_back(i);
    }
  }
  assert(ask(S) == 2);
}

void solveSubtaskFive() {
  int l = 1, r = n, at = -1;
  while (l <= r) {
    int mid = (l + r) >> 1;
    vector<int> v = {mid};
    int cur = ask(v);
    if (cur == 2) {
      return;
    }
    if (cur == 1) {
      l = mid + 1;
      at = mid;
    } else {
      r = mid - 1;
    }
  }
  assert(at != -1);
  vector<int> S(at);
  iota(S.begin(), S.end(), 1);
  assert(ask(S) == 2);
}

void solveForTwo() {
  vector<bool> badNumber(n + 1);
  for (int i = 1; i < n; i++) {
    for (int j = i + 1; j <= n; j++) {
      vector<int> v = {i, j};
      int cur = ask(v);
      if (cur == 2) {
        return;
      }
      if (cur == 0) {
        badNumber[i] = badNumber[j] = true;
      }
    }
  }
  vector<int> S;
  for (int i = 1; i <= n; i++) {
    if (badNumber[i]) {
      continue;
    }
    S.emplace_back(i);
  }
  if (ask(S) == 2) {
    return;
  }
  int m = (int)S.size();
  for (int i = 0; i < m; i++) {
    vector<int> SS(m - 1);
    for (int j = 0, x = 0; j < m; j++) {
      if (j == i) {
        continue;
      }
      SS[x++] = S[j];
    }
    if (ask(SS) == 2) {
      return;
    }
  }
  assert(false);
}

int main() {
  ios_base::sync_with_stdio(0);
  cin.tie(0);

  cin >> str >> subsoal;
  cin >> n >> k >> q;
  if (subsoal == 5) {
    solveSubtaskFive();
  } else if (k == 1) {
    solveForOne();
  } else if (k == 2) {
    solveForTwo();
  }

  return 0;
}
```
</details>