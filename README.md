<h1 align="center">算法题解收录</h1>

# Tabel of Contents

- [Codeforces](#Codeforces)
  - [Round #753 div.3](#Round_#753_div.3)
- [Google Kickstart](#Google_Kickstart)
- [Problems from Uva](#Problems_from_Uva)
  - [Brute force](#Brute_force)

# Codeforces
## ▶ Round #753(Div.3)

### A\. Linear Keyboard

#### 💡 Explanation:
+ tags: Implementation
+ All we have to do is find the index of each letter in the string s on the keyboard. And the answer is the sum of difference between two adjacent letters in the string s.
+ In other word, the answer is <img src="/images/cd753-A.png" alt=""></p>
```cpp
#include<bits/stdc++.h>
using namespace std;

int n;
string str1, str2;

int find(char x)
{
	for(int i = 0; i < str1.size(); i ++ )
		if(str1[i] == x)
			return i;
			
	return 0;
}

int main()
{
	cin >> n;
	while(n -- )
	{
		cin >> str1 >> str2;
		
		int res = 0;
		for(int i = 1; i < str2.size(); i ++ )
			res += abs(find(str2[i]) - find(str2[i - 1]));
			
		cout << res << endl;
	}
	
	return 0;
}
```
### B\. Odd Grasshopper

#### 💡 Explanation:
+ tags: math
+ We can select 0 and 1 respectively as the coordinate of the grasshopper's initial position. Then we have:
 0 as initial position: -1+2+3-4-5+6+7...  	
 1 as initial position: 1-2-3+4+5-6-7...   
 We can find that both jump to the left twice and then to the right twice      
 According to this pattern, we can have the following tabel:  
 |The number of jumps|distance from initial coordinate(starting point is even)|distance from initial coordinate(starting point is even)|
 -:|:-:|:-
 |k%4==0|0|0|   
 |k%4==1|-k|k|    
 |k%4==2|1|-1| 
 |k%4==3|1+k|-1-k|     
 ```cpp
 #include<bits/stdc++.h>
using namespace std;

typedef long long LL;

int main()
{
	int n;
	cin >> n;
	while(n -- )
	{
		LL st, k;
		cin >> st >> k;
		
		LL res = 0, change = 0;
		if(k % 4 == 0) change = 0;
		else if(k % 4 == 1) change = -k;
		else if(k % 4 == 2) change = 1;
		else	change = 1 + k;
		
		//change for odd number as starting point is just right opposite to that for even number
		if(st % 2)	res = st - change;
		else	res = st + change;
		
		cout << res << endl;	
	}
	
	return 0;
}
 ```
### C\. Minimum Extraction

#### 💡 Explanation:
+
```cpp
#include<bits/stdc++.h>
using namespace std;

const int N = 200010;
int a[N];

int main()
{
	int t;
	cin >> t;
	while(t -- )
	{
		int n;
		cin >> n;
		for(int i = 1; i <= n; i ++ )	scanf("%d", &a[i]);
		
		sort(a + 1, a + n + 1);
		
		int res = a[1];
		for(int i = 1; i < n; i ++ )
			res = max(res, a[i + 1] - a[i]);
		
		printf("%d\n", res);
	}
	
	return 0;
}
```
### D\. Blue-red Permutation

#### 💡 Explanation:
+
```cpp
#include<bits/stdc++.h>
using namespace std;

const int N = 200010;
int a[N];

vector<int> l, r;

int main()
{
	int t;
	cin >> t;
	while(t -- )
	{
		int n;
		cin >> n;
		for(int i = 1; i <= n; i ++ )	scanf("%d", &a[i]);
		for(int i = 1; i <= n; i ++ )
		{
			char op;
			cin >> op;
			if(op == 'B')	l.push_back(a[i]);
			else	r.push_back(a[i]);
		}
		
		sort(l.begin(), l.end());
		sort(r.begin(), r.end(), greater<int>());
		
		for(int i = 0; i < n; i ++ ) cout << l[i] << " ";
		cout << endl;
		for(int i = 0; i < n; i ++ ) cout << r[i] << " ";
	}
}
```


# Google Kickstart
## ▶ 2021 Round A

### 1\. K-goodness string

#### 💡 Explanation:
+
```cpp
#include<bits/stdc++.h>
using namespace std;

const int N = 1000100;
char s[N];

int main()
{
	int T;
	cin >> T;
	for(int C = 1; C <= T; C ++ )
	{
		int n, k, now = 0;
		cin >> n >> k;
		for(int i = 0; i < n; i ++ )	cin >> s[i];
		for(int i = 0; i < n / 2; i ++ )
			if(s[i] != s[n - i - 1])
				now ++ ;
			
		
		printf("Case #%d: %d\n", C, abs(now - k));
	}	
	
	return 0;
}
```
### 2\. L-Shaped Plots

#### 💡 Explanation:
+
```cpp
#include<bits/stdc++.h>
using namespace std;

const int N = 1100;
char g[N][N];
int t[N][N], b[N][N], l[N][N], r[N][N];
int R, C, ans;

void initial()
{
	for(int i = 1; i <= R; i ++ )
		for(int j = 1; j <= C; j ++ )
		{
			t[i][j] = 0, b[i][j] = 0, l[i][j] = 0, r[i][j] = 0, g[i][j] = '0';
		}
}

int count(int x, int y)
{
	if(x < 2 || y < 2)	return 0;
	return min(x / 2, y) + min(x, y / 2) - 2;
}

int main()
{
	int T;
	cin >> T;
	for(int K = 1; K <= T; K ++ )
	{
		initial();
		ans = 0;
		cin >> R >> C;
		for(int i = 1; i <= R; i ++ )
			for(int j = 1; j <= C; j ++ )
				cin >> g[i][j];
		
		for(int i = 1; i <= R; i ++ )
			for(int j = 1; j <= C; j ++ )
					if(g[i][j] != '0')
					{
						t[i][j] = t[i - 1][j] + 1;
						l[i][j] = l[i][j - 1] + 1;
					}
			
		for(int i = R; i >= 1; i -- )
			for(int j = C; j >= 1; j -- )
					if(g[i][j] != '0')
					{
						b[i][j] = b[i + 1][j] + 1;
						r[i][j] = r[i][j + 1] + 1;
					}

		for(int i = 1; i <= R; i ++ )
			for(int j = 1; j <= C; j ++ )
			{
				ans += count(t[i][j], l[i][j]);
				ans += count(t[i][j], r[i][j]);
				ans += count(b[i][j], l[i][j]);
				ans += count(b[i][j], r[i][j]);
			}
		
		printf("Case #%d: %d\n", K, ans);
	}
}
```
## ▶ Other

### 1\. Training

#### 💡 Explanation:
```cpp
```


# Prolems from Uva
## ▶ Brute force and search
### Brute Force
