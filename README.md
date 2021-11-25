<h1 align="center">算法题解收录</h1>

# Tabel of Contents

- [Codeforces](#Codeforces)
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
