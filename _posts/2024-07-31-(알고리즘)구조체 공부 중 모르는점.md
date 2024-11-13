---
layout: post
title: 구조체 공부 중 헷갈리는 점 정리 
subtilte:
date: 2024-07-31
categories: algorithm
tags:
comments: true
typora-root-url: ../
---



> c++ 구조체 공부 중 헷갈렸던 점을 정리 :pencil:



## 1. 고민인 점

구조체를 정렬할 때 사용하는 cmp 멤버 함수를 만들면서 헷갈리는 점이 생겼다.

첫 번째로 만든 간단한 구조체는 그냥 멤버 변수 2개가 매개변수로 사용되었고 그것을 이용해 비교하는 함수이다.

```c++
#include <bits/stdc++.h>
using namespace std;

struct Point{
	int a, b;
};

bool cmp(Point A, Point B){
	if(A.a == B.a) return A.b < B.b;
	return A.a < B.a;
}

int main(){
	sort(a, a+3, cmp);
	for(Ralo A : a) cout << A.a << " : " << A.b << "\n";
}
```

첫 번째로 a를 기준으로 오름차순으로 정렬하고 만약 a 값이 같다면 b로 비교하는 간단한 cmp 함수를 만들었다.



근데 내가 공부하는 교제에서 다음 실습으로 vector에다 struct 넣고 정렬하는 코드가 나왔다. 코드가 앞의 코드와 비슷했지만 조금씩 달랐는데 왜 달라졌는지 모르겠다..



```
struct Point{
	int y, x;
};

bool cmp(const Point & a, const Point & b) {
	
}
```



const는 변화 안시키고 싶다는 강한 의지로 판단이 되지만 & 참조는 왜 있는지 모르겠다.. 30분간 고민한 결과를 적어보면

1. 위의 자료와 너무 똑같이 만들고 싶지 않다는 작가의 의지
2. 참조를 사용하면 멋져보여서

이딴 생각밖에 들지 않았다... 하지만 일단 이 페이지를 넘어가고 더 교재를 읽어보니 `참조`에 대한 설명이 나왔고 자세히 읽어 보고 난 후에야 이해할 수 있었다!

**primitive**한 타입, double, int 등은 *call by value*로 넘기는게 좋다. 복사가 일어나기는 하지만 간단하기 때문에 복사할 때 무리가 적다는 것이다. 반대로 **reference**한 타입, 복잡한 struct나 많은 요소를 가진 배열 등 이러한 것들은 *call by reference*로 매개변수를 넘기는 것이 더 좋다. 왜냐면 참조가 없을 경우 전체 복사에서 드는 코스트가 부담이 되기 때문이다.

그래서 앞에서 `const Point & a, const Point & b` 가 사용된 것!! Point가 뭐 엄청 복잡한 구조는 아니지만 struct이기 때문에 참조로 넘긴 것이고 참조 때문에 값이 변경될 것을 고려해 const가 붙은 것이였다..



