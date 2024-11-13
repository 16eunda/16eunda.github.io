---
layout: post
title: 백준 문제풀이 1주차
subtilte:
date: 2024-08-01
categories: algorithm
tags:
comments: true
typora-root-url: ../
---



> c++ 을 이용해서 백준 문제 풀이 1주차 (1) :pencil:



인프런에서 코테 강의를 들으면서 거기서 제공하는 문제를 풀었다. 

내가 스스로 푼 문제가 거의 없당.. ㅎㅎ 그래도 문제당 1~2시간 생각해보는 습관은 가지려고 한다.



## 1. 일곱난쟁이

백준: 2309  - 일곱난쟁이 문제

9명의 난쟁이 키가 주어지고 진짜 난쟁이 7명의 키가 100이 되는 것을 이용해서 진짜 난쟁이 7명을 찾는 문제이다. 처음에는 진짜 어떻게 푸는지 모르겠어서 인프런 강의를 그냥 봤다. 9명 중 7명을 찾으면 되는 것이니깐 조합으로 풀면 되는 문제였다.

```c++
#include <bits/stdc++.h>
using namespace std;

int sum = 0;
vector<int> arr;
int a;
int n = 9;

int main() {
	for (int i = 0; i < 9; i++) {
		cin >> a;
		arr.push_back(a);
		sum += a;
	}


	for (int i = 0; i < n; i++) {
		for (int j = 0; j < i; j++) {
			cout << i << " : " << j << "\n";
			if ((sum - arr[i] - arr[j]) == 100) {
				arr.erase(arr.begin() + i);
				arr.erase(arr.begin() + j);

				sort(arr.begin(), arr.end());

				for (int i : arr) cout << i << "\n";

				return 0;
			}
		}
	}

}
```





## 2. 알파벳 개수

백준: 10808 - 알파벳 개수 문제

알파벳 소문자로만 들어오는 문자열 s에서 a~z가 각각 몇개인지 출력하는 문제.

처음에는 왠지 모르겠는데 그냥 배열 보다 map이 먼저 떠올라서 아래처럼 코드를 만들었다.

map 변수에  a : 0 ~ z : 0 개 이런식으로 초기화 하고 구지 find 함수까지 써서 알파벳을 찾고 증가시켰다.. 맞기는 했는데.. 여러 문제 풀고 지금 정리하다 보니 과거에 내가 왜 이렇게 풀었는지 모르겠당..

```c++
#include <bits/stdc++.h>
using namespace std;

string s;
map<char, int> map1;

void solve() {
	for (int i = 0; i < 26; i++) {
		char c = 'a' + i;
		map1.insert({ c, 0 });
	}
}

int main() {
	cin >> s;

	solve();

	for (int i = 0; i < s.size(); i++) {
		char c = s[i];
		if (map1.find(c) != map1.end()) {
			map1[c]++;
		}
	}

	for (auto a : map1) cout << a.second << " ";
}
```



그래서 아래 처럼 그냥 map 말고 배열로하고 좀 간단하게 바꿔서 다시 풀었다.

```c++
#include <bits/stdc++.h>
using namespace std;

string s;
int cnt[26];

int main() {
	cin >> s;

	for (char c : s) {
		cnt[c - 'a']++;
	}
	for (int i : cnt) {
		cout << i << " ";
	}
}
```



## 3. 트럭주차

백준: 2979 - 트럭주차 문제

진짜 처음 풀때 생각이 안나서 머리 깨지는 줄 알았다

```c++
#include <bits/stdc++.h>
using namespace std;

int price[3];
int a;
int b;
int cnt[104];
int ret;


int main() {
	for (int i = 0; i < 3; i++) cin >> price[i];
	for (int i = 0; i < 3; i++) {
		cin >> a >> b;
		for (int j = a; j < b; j++) cnt[j]++;
	}

	for (int i = 1; i < 100; i++) {
		if (cnt[i] == 1) ret += price[0];
		else if (cnt[i] == 2) ret += 2 * price[1];
		else if (cnt[i] == 3) ret += 3 * price[2];
	}

	cout << ret;
}
```



## 4. 팰린드롬인지 확인하기

백준: 10988 - 팰린드롬인지 확인하기

처음에 reverse 기억을 못해서 for문으로 내가 직접 뒤집어서 풀었다.. reverse().. 마음에 새기기

```c++
#include <bits/stdc++.h>
using namespace std;

string s, r;
int main() {
	cin >> s;
	r = s;

	reverse(s.begin(), s.end());
	
	if (s == r) {
		cout << 1 << "\n";
	}
	else {
		cout << 0 << "\n";
	}
}
```



## 5. 농구 경기

백준: 1159 - 농구경기

이름 첫 글자만 필요! 이걸 또 배열이나 map으로 정리해서 5개 이상인 것을 추려서 넣으면 됨

```c++
#include <bits/stdc++.h>
using namespace std;

int n;
string mem;
vector<string> name;
map<char, int> map1;
vector<char> ret;

int main() {

	cin >> n;
	for (int i = 0; i < n; i++) {
		cin >> mem;
		if (map1.find(*mem.begin()) != map1.end()) {
			map1[*mem.begin()]++;
		}
		else {
			map1.insert({ *mem.begin(), 1 });
		}
	}

	for (auto s : map1) {
		if (s.second >= 5) ret.push_back(s.first);
	}
	
	if(ret.empty()) cout << "PREDAJA";
	for (char c : ret) cout << c;
}
```



## 6. ROT13

백준: 11655 - ROT13

입력방은 문자열을 각 단어들을 13씩 밀어서 암호문을 만드는 문제. 처음에 그냥 -13만 하면 되는 줄 알고 신나서 풀었지만 뭔가 이상..ㅜ 1. 알파벳인지 확인 2. 소문자 대문자 나누기 3. 13씩 미는데 만약 범위를 넘어가는 경우도 고려

```c++
#include <bits/stdc++.h>
using namespace std;

string s;

int main() {
	getline(cin, s);

	for (int i = 0; i < s.size(); i++) {
		if ((s[i] >= 'A') && (s[i] <= 'Z')) {
			if (s[i] + 13 > 'Z') s[i] = s[i] + 13 - 26;
			else s[i] = s[i] + 13;
		}
		if ((s[i] >= 'a') && (s[i] <= 'z')) {
			if (s[i] + 13 > 'z') s[i] = s[i] + 13 - 26;
			else s[i] = s[i] + 13;
		}
	}

	cout << s;
}
```



처음에 if문을 아래처럼 만들었는데 답이 이상한게 나왔다. 내 생각에는 우선 13을 더한 다음 이상한게 나와도 -26을 하면 다시 알파벳이 나올 줄 알았는데 생각과 다르게 s[i] + 13을 더한 후 이상한 쓰래기값? 이 들어가게 됬다. 그러니깐 알파벳일 때 처럼 -26을 해도 알파벳 처럼 자동으로 문자가 들어가는게 아니라 아예 계산이 안되는 것 같았다.. 주의해야겠다.. 그냥 if문으로 검사를 먼저 하는 습관을 들여야 하나..?

```c++
if ((s[i] >= 'A') && (s[i] <= 'Z')) {
	s[i] = s[i] + 13;
	if (s[i] > 'Z') s[i] -= 26;
}
```





## 7. 한국이 그리울 땐 서버에 접속하지

백준: 9996 - 한국이 그리울 땐 서버에 접속하지

패턴이 맞는지 확인하는 문제. 처음에는 * 문자를 기준으로 split을 하는 줄 알았지만 어짜피 * 문자는 하나만 있으므로 안써도 상관 없었다.. 그리고 substr 함수가 있는 것을 또 까먹어서 푸는데 너무 오래걸렸다. erase()만 자꾸 생각나고 substr()이 자꾸 생각이 안난다..ㅜ 마음에 새길 것..

```c++
#include <bits/stdc++.h>
using namespace std;

int n;
string p;
string f[104];
string s;
vector<string> ret;

bool check(string f, string p) {

	int pos = p.find("*");
	string pre = p.substr(0, pos);
	string suf = p.substr(pos + 1);

	if (pre.size() + suf.size() > f.size()) return 0;
	else {
		if ((pre == f.substr(0, pre.size())) && (suf == f.substr(f.size() - suf.size()))) return 1;
		else return 0;
	}
}

int main() {

	cin >> n;
	cin >> p;

	for (int i = 0; i < n; i++) {
		cin >> f[i];
		if (check(f[i], p)) {
			ret.push_back("DA");
		}
		else ret.push_back("NE");
	}

	for (auto a : ret) cout << a << "\n";

}
```



그리고 if (pre.size() + suf.size() > f.size()) return 0; 조건을 생각을 못했다.. 이게 없으면 컴파일 에러가 뜨니깐 주의해야한다. 근데 혼자서 풀때는 도저히 생각이 안나는데.. 어ㅉㅓ지..



## 8. 수열

백준: 2559 - 수열

처음 문제풀때 n개의 수를 받아야 했다. n이 입력하기 전까지 미정이기 때문에 계속 vector를 문제를 풀었다. 근데 그냥 n의 범위가 나와있으므로 n을 최대 범위로 잡고 문제를 풀면 됬었다. 

해답을 보기 전 내가 생각해서 풀 때는 구간합이라는 것을 생각하지 못했다. 그래서 그냥 요령없이 계속 합해서 구하는 방식으로 풀었다. 근데 뭐.. 문제 없이 맞았다.. 지금 다시 정리해서 풀 때는 구간의 합들을 일단 먼저 만들고,

k=5이면 1~5까지의 합부터 구하면 되니깐 k부터 시작하고 그 전의 값을 빼 주는 방식으로 문제를 푸었다!

```c++
#include <bits/stdc++.h>
using namespace std;

int n, k;
int psum[100004];
vector<int> ret;

int main() {
	cin >> n >> k;
	for (int i = 1; i <= n; i++) {
		cin >> psum[i];
		psum[i] = psum[i - 1] + psum[i];
	}

	for (int i = k; i <= n; i++) {
		ret.push_back(psum[i]-psum[i-k]);
	}

	cout << *max_element(ret.begin(), ret.end());
}
```



## 9. 나는야 포켓몬 마스터 이다솜

백준: 1620 - 나는야 포켓몬 마스터 이다솜

n개의 포켓몬 문자열을 받아서 도감을 만들고 입력오르로 m개의 문제가 들어오는데 숫자가 들어오면 도감을 보고 그 번째의 포켓몬 이름,  이름이 들어오면 도감에서 해당 이름의 번호를 출력하는 문제이다.

처음에 map을 쓰는 문제인 것은 금방 알아서 쉽다고 생각하면서 풀었는데 시간초과가 나왔다. 아래처럼 코드를 만들어서 였다. n, m이 100,000이 최대여서  이중 for문으로 만들게 되면 100,000 * 100,000 이 되서 시간이 초과된 것 같다..

```c++
for (int i = 0; i < m; i++) {
	cin >> s;
	//s가 숫자 문자이면
	if (atoi(s.c_str()) != 0) { 
		int num = atoi(s.c_str());
		ret.push_back(book[num]);
	}
	else {
		for (auto i : book) {
			if (i.second == s) {
				ret.push_back(to_string(i.first));
			}
		}
	}
}
```



그래서 끙끙 대면서 풀다가 그냥 map을 두개 쓰면 되는 거였다. map을 1개를 써서 만약 문자이면 이 값을 for문을 돌면서 찾아야 했는데 그냥 map 2개를 쓰면 그냥 풀리는 거였다.

```c++
#include <bits/stdc++.h>
using namespace std;

vector<string> ret;
string s;
map<string, int> book;
map<int, string> book2;
int n, m;

int main() {
	cin >> n >> m;

	for (int i = 1; i <= n; i++) {
		cin >> s;
		book.insert({ s, i });
		book2.insert({ i, s });
	}

	for (int i = 0; i < m; i++) {
		cin >> s;
		//s가 숫자 문자이면
		if (atoi(s.c_str()) != 0) { 
			//몇번째 포켓몬인지 입력됨
			int num = atoi(s.c_str());
			ret.push_back(book2[num]);
		}
		else {
			//걍 포켓몬 이름
			string temp = to_string(book[s]);
			ret.push_back(temp);
		}
	}

	for (string s : ret) cout << s << "\n";
	
}
```

반성: `atoi, to_string` 함수가 기억이 안 났다... atoi는 기억은 났는데 반환값이 어떻게 되는지 까먹었다. atoi(string이 이니라 char가 들어가야 함) `c_str()`을 기억, 그리고 숫자로 바꿀 수 있는 문자열이면 바꿔주고 못 바꾸는 문자이면 0을 반환함



## 10. 패션왕 신해빈

백준: 9375 - 패션왕 신해빈 

이거 도저히 어떻게 푸는 건 줄 모르겠다.. 2시간 동안 끙끙 대다가 머리가 터질 것 같아서 답을 봤다..

```c++
#include <bits/stdc++.h>
using namespace std;

int _case;
int n;
map<string, int> _map;
string a, b;
vector<long long> ans;

int main() {
	cin >> _case;

	while (_case--) {

		cin >> n;

		for (int i = 0; i < n; i++) {
			cin >> a >> b;
			_map[b]++;
		}
		long long ret = 1;

		for (auto i : _map) {
			ret *= ((long long)i.second + 1);
		}
		ret--;
		ans.push_back(ret);
		_map.clear();
	}

	for (auto i : ans) cout << i << "\n";
}
```



## 11. 팰린드롬 만들기

백준: 1213 - 팰린드롬 만들기

이것도 간단 할 줄 알았는데 생각보다 고려해야 할 점이 너무 많았다. 1. 홀수가 2개 이상이면 만들기 불가능. 2. 홀수가 1개 있으면 그거는 마지막에 가운데 넣어야 함. 3. 짝수인 것들을 차곡차곡 넣기. 4. 사전 순인 것을 고려하기

```c++
#include <bits/stdc++.h>
using namespace std;

int cnt[26];
int flag;
string s;
char mid;
string ret;

int main() {
	cin >> s;

	for (char c : s) cnt[c]++;
	for (int i = 'Z'; i >= 'A'; i--) {
		if (cnt[i]) {
			if (cnt[i] & 1) {
				mid = char(i);
				flag++;
				cnt[i]--;
			}
			if (flag == 2) break;
			for (int j = 0; j < cnt[i]; j += 2) {
				ret = char(i) + ret;
				ret += char(i);
			}
		}
	}
	if (mid) ret.insert(ret.begin() + ret.size() / 2, mid);
	if (flag == 2) cout << "I'm Sorry Hansoo";
	else cout << ret << "\n";
}
```



## 12. 주몽

백준: 1940 - 주몽

이건 처음에 조합으로 풀면 시간 초과 날 것 같아서 조합을 쓰지 않고 풀었다. 그냥 n개의 숫자를 arr에 저장하고 합 했을 때 m을 만들 수 있는 숫자를 찾는 방법으로 풀었다. m-arr[i] 의 값이 arr에 있는지, 만약 있다면 ret++ 한 후, 한 번 카운팅을 했으면 나중에 또 찾으면 안되므로 배열에서 지워버렸다.

```c++
#include <bits/stdc++.h>
using namespace std;

int n, m;
int ret = 0;
vector<int> arr;
int num;

int main() {
	cin >> n;
	cin >> m;
	for (int i = 0; i < n; i++) {
		cin >> num;
		arr.push_back(num);
	}
	for (int i = 0; i < arr.size(); i++) {
		int num = m - arr[i];
		auto it = find(arr.begin() + i + 1, arr.end(), num);
		if (it != arr.end()) {
			ret++;
			arr.erase(it);
		}
	}
	cout << ret;
}
```

근데 다 풀고 강의를 보니깐 조합으로 풀어도 됬었다.. 어쩔 때 시간 초과가 나는지 잘 모르겠다..ㅜ 아래는 조합으로 푼 풀이 이다.

```c++
#include <bits/stdc++.h>
using namespace std;

int n, m;
int ret = 0;
int arr[15004];

int main() {
	cin >> n;
	cin >> m;

	for (int i = 0; i < n; i++) {
		cin >> arr[i];
	}

	if (m > 200000) cout << 0;
	else {
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < i; j++) {
				if (arr[i] + arr[j] == m) {
					ret++;
				}
			}
		}
	}
	cout << ret;
}

```



## 13. 좋은 단어

백준: 3986 - 좋은 단어

진짜 이 문제 좋은 단어 규칙이 도저히 생각이 안났다. 진짜 하루종일 이 생각만 했는데도 도저히 모르겠어서 그냥 강의 보고 풀었다.. ㅜ 진짜 개멍청:sob: 

스택을 이용해서 풀어야하는 문제였다. 모르겠으면 단어를 뒤집고 다 해봤어야 했는데.. 스택으로 단어를 넣고 만약 스택에 단어가 이미 있고 단어를 넣으려고 할 때 비교해서 같은면 pop 아니면 넣고 이런식으로 반복하고 입력한 단어가 다 끝났는데 스택에 값이 없어야 좋은 단어. 아니면 나쁜 단어였다.

계속 단어가 홀수개면 나쁜단어.. 그 다음에 어떤 문자가 있으면 나쁜단어라고 생각해서 안풀렸다..

```

```



## 14. 곱셈

백준: 1629 - 곱셈

자연수 A를 B번 곱한 수를 알고 싶다. 단 구하려는 수가 매우 커질 수 있으므로 이를 C로 나눈 나머지를 구하는 프로그램을 작성하시오.  A, B 가 미친 듯이 크기 때문에 이걸 구하는 것은 불가능.. 이게 대충 느낌이 와서 손으로 풀면 알겠지만 실제 코드로 구현을 하려고 하니깐 감이 안왔다. 

```c++
#include <bits/stdc++.h>
using namespace std;

long long ret;
int a, b, c;
int final;

long long fast_pos(int a, int b) {
	if (b == 1) return a % c;
	long long ret = fast_pos(a, b / 2);
	ret = ret * ret % c;
	if (b % 2) ret = (ret * a) % c;
	return ret;
}

int main() {

	cin >> a >> b >> c;

	ret = fast_pos(a, b);

	cout << ret;

}
```



## 15. 1

백준: 4375 - 1

미친 듯이 어려웠음..  진짜 종이에 계속 이상한 문자만 적어가면서 열심히 풀려고 노력은 했지만.. 포기.. 머리가 과부화 :weary: 아직도 이해가 안되고 있음



