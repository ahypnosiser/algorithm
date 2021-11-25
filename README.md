<h1 align="center">算法题解收录</h1>

# Tabel of Contents

- [Codeforces](#Codeforces)
- [Google Kickstart](#Google_Kickstart)
- [Problems from Uva](#Problems_from_Uva)
  - [Brute force](#Brute_force)

# Codeforces
### ▶ Round #753(Div.3)

A\. Linear Keyboard

#### 💡 Explanation:
+ tags: Implementation
+ <p align="center"><img src="/images/CodeCogsEqn.png" alt=""></p>
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
