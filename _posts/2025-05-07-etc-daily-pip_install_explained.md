---
layout: post
title: pip install 원리
subtilte: pip install 한 줄짜리 명령어의 마법
date: 2025-05-07
categories: etc
tags: 기타
comments: true
typora-root-url: ../
---

# pip install 한 줄로 모듈이 설치되는 원리, 진짜로 이해해보기

개발을 하다 보면 너무나 자연스럽게 사용하는 명령어 중 하나가 `pip install`. 예를 들어:

```bash
pip install schedule
```

정말 한 줄만 입력했을 뿐인데, 이후로 `import schedule`이 아무 문제 없이 작동한다. 이게 너무 당연하게 느껴지지만, 잠시 멈추고 생각해보자. 도대체 이 한 줄짜리 명령어는 무슨 일을 하고 있는 걸까?

이 글에서는 그 과정을 하나씩 뜯어보면서, 우리가 자주 쓰는 `pip install`이 어떤 원리로 작동하는지, 왜 `import`가 가능한지를 정리해본다.

---

## pip는 정확히 무엇인가?

`pip`는 **Python의 공식 패키지 관리자**다. 우리가 작성하지 않은 외부 라이브러리를 인터넷에서 다운받아 설치해주는 도구다. 쉽게 말하면:

> 📦 PyPI(Python Package Index)라는 저장소에서 패키지를 찾아서  
> 🧰 내 Python 환경에 설치하고,  
> 🧠 `import`할 수 있게 연결해주는 역할을 한다.

---

## PyPI는 뭐하는 곳인가?

[https://pypi.org](https://pypi.org)는 전 세계의 Python 개발자들이 만든 패키지를 공유하는 저장소다. 수십만 개의 라이브러리가 올라와 있고, 우리가 `pip install` 할 때 기본적으로 이곳에서 패키지를 찾는다.

예를 들어 `schedule`을 설치하면, pip는 PyPI에 요청해서 해당 패키지의 `.whl`(wheel) 또는 `.tar.gz` 파일을 다운로드한다.

---

## 그럼 실제로 pip는 무슨 일을 하는가?

```bash
pip install schedule
```

이 명령어를 실행하면 다음과 같은 작업이 자동으로 이루어진다:

1. 📡 PyPI에 접속해서 `schedule`이라는 패키지 검색  
2. 📥 해당 패키지의 설치 파일(wheel)을 다운로드  
3. 📂 현재 사용 중인 Python의 `site-packages/` 디렉토리에 압축 해제 및 설치  
4. 📜 패키지 메타데이터 기록 (`installed-files.txt` 등)

설치된 모듈은 바로 이 `site-packages`라는 폴더에 들어간다. 이 폴더는 Python이 `import`할 때 자동으로 참조하는 경로 중 하나다.

---

## `import`가 바로 되는 이유는?

파이썬은 내부적으로 `sys.path`라는 리스트를 가지고 있는데, 여기에 여러 디렉토리 경로가 담겨 있다. 코드를 실행하면 `import schedule` 같은 문장을 만나게 될 때:

```python
import sys
print(sys.path)
```

이 리스트를 순차적으로 탐색해서 `schedule`이라는 모듈이 들어 있는 폴더를 찾는다. `pip install`로 설치된 모듈은 이 경로 중 하나인 `site-packages`에 들어가기 때문에 바로 인식이 되는 것이다.

예시 경로:

```
C:\Users\사용자\AppData\Local\Programs\Python\Python311\Lib\site-packages
```

---

## 진짜 마법 같은가? 사실은 엄청 정교한 생태계 덕분

`pip`는 단순히 설치만 해주는 게 아니라, 버전 충돌 관리, 의존성 패키지 처리, 업그레이드 및 제거까지 처리해준다. 그리고 그 기반엔 `setuptools`, `wheel`, `PyPI`, `PEP`들(파이썬 개선 제안서)까지 엮여 있다.

우리가 한 줄로 입력한 `pip install`은 사실 **파이썬 생태계의 모든 툴들이 협업해서 만들어내는 결과물**이다.

---

## 마무리

너무 당연하게만 느껴졌던 `pip install` 명령어. 사실 그 안에는 파이썬 생태계의 강력함과 유연함, 그리고 커뮤니티의 협업이 담겨 있다.

다음에 한 줄 입력할 때는, 그 뒤에서 움직이는 이 멋진 시스템을 한 번쯤 떠올려보면 어떨까?
