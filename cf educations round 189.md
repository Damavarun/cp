### A. A Number Between Two Others
## sol :

```
 #include <bits/stdc++.h>
using namespace std;
 
int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
 
    int t;
    cin >> t;
 
    while (t--) {
        long long x, y;
        cin >> x >> y;
 
        if (y / x == 2)
            cout << "NO\n";
        else
            cout << "YES\n";
    }
 
    return 0;
}

```

### ----------------------------------
## B. Alternating String
## sol : 
```
#include<bits/stdc++.h>
using namespace std;
 
bool isPossible(string s, char firstChar) {
    int n = s.size();
 
    
    vector<int> badPositions;
 
    for (int i = 0; i < n; i++) {
        char expected;
 
        if (i % 2 == 0) {
            expected = firstChar;
        } else {
            expected = (firstChar == 'a' ? 'b' : 'a');
        }
 
        if (s[i] != expected) {
            badPositions.push_back(i);
        }
    }
 
    if (badPositions.empty()) {
        return true;
    }
 
    
    for (int i = 1; i < badPositions.size(); i++) {
        if (badPositions[i] != badPositions[i - 1] + 1) {
            return false;
        }
    }
 
    return true;
}
 
int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
 
    int testCases;
    cin >> testCases;
 
    while (testCases--) {
        string s;
        cin >> s;
 
        bool answer = false;
 
       
        if (isPossible(s, 'a') || isPossible(s, 'b')) {
            answer = true;
        }
 
        if (answer) {
            cout << "YES\n";
        } else {
            cout << "NO\n";
        }
    }
 
    return 0;
}

```


### ----------------------------------
  
## C - Red-Black Pairs
## sol : 
```
 #include <iostream>
#include <vector>
#include <string>
using namespace std;
 
const int INF = 1e9;
 
int n;
string topRow, bottomRow;
vector<vector<int>> memo;
 
int dfs(int col, int mask) {
    
    if (col == n) {
        return (mask == 0 ? 0 : INF);
    }
 
    
    if (memo[col][mask] != -1) {
        return memo[col][mask];
    }
 
    int answer = INF;
 
   
    if (mask == 3) {
        answer = dfs(col + 1, 0);
    }
 
   
    else if (mask == 0) {
 
        
        int costVertical = (topRow[col] != bottomRow[col]);
        answer = min(answer, costVertical + dfs(col + 1, 0));
 
       
        if (col + 1 < n) {
            int costTop = (topRow[col] != topRow[col + 1]);
            int costBottom = (bottomRow[col] != bottomRow[col + 1]);
 
            answer = min(
                answer,
                costTop + costBottom + dfs(col + 1, 3)
            );
        }
    }
 
  
    else if (mask == 2) {
        if (col + 1 < n) {
            int cost = (topRow[col] != topRow[col + 1]);
            answer = min(answer, cost + dfs(col + 1, 1));
        }
    }
 
 
    else if (mask == 1) {
        if (col + 1 < n) {
            int cost = (bottomRow[col] != bottomRow[col + 1]);
            answer = min(answer, cost + dfs(col + 1, 2));
        }
    }
 
    return memo[col][mask] = answer;
}
 
int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
 
    int testCases;
    cin >> testCases;
 
    while (testCases--) {
        cin >> n;
        cin >> topRow >> bottomRow;
 
        memo.assign(n + 1, vector<int>(4, -1));
 
        cout << dfs(0, 0) << '\n';
    }
 
    return 0;
}
```

### ----------------------------------

##  D - Exceptional Segments
```
#include <bits/stdc++.h>
using namespace std;
 
const long long MOD = 998244353;
 
long long countZero(long long m) {
    if (m < 0) return 0;
    return 1 + (m + 1) / 4;
}
 
long long countOne(long long m) {
    if (m < 1) return 0;
    return (m + 3) / 4;
}
 
int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
 
    int t;
    cin >> t;
 
    while (t--) {
        long long n, x;
        cin >> n >> x;
 
        long long leftZero = countZero(x - 1);
        long long rightZero = countZero(n) - countZero(x - 1);
 
        long long leftOne = countOne(x - 1);
        long long rightOne = countOne(n) - countOne(x - 1);
 
        long long answer = 0;
        answer = (answer + (leftZero % MOD) * (rightZero % MOD)) % MOD;
        answer = (answer + (leftOne % MOD) * (rightOne % MOD)) % MOD;
 
        cout << answer % MOD << '\n';
    }
 
    return 0;
}
```
-------
