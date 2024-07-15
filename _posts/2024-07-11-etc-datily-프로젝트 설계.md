---
layout: post
title: 구인구직 사이트 pick_me 만들기(1)
subtitle: 아이디어, db 설계
date: 2024-07-11
categories: daily
tags: 
comments: true
typora-root-url: ../
---



>:notebook: `사람인`과 같은 구인구직 웹 사이트 만들기
>
>아마 똑같이 만들기는 어려울 것 같지만 gpt3.5 api를 사용해보는 것을 목표로 만들 예정



# 1. 아이디어

사람인과 같은 구인구직 사이트를 만들었다.

사실 사람이과 비슷하다고 했지만 기업/구직자 정보를 따로 받는 것이 아니라

기업 정보를 찾는 사이트에 가깝게 만들었다.



사실 이런 사이트는 많지만 나름의 차별점을 만들기는 했다..

- #### 차별점

  gpt3.5 api를 이용하여 매칭 서비스를 구현

  gpt3.5 api를 사용해 자기소개서를 작성하는 서비스 구현



---



# 2. 사용하는 것



- springboot
- db: mysql, amazon db
- saramin api
- gpt api





---



# 3. db 설계









# 4. 사람인 api 사용 신청

실시간 구직 정보를 받아오기 위해서 사람인 api를 사용한다.

[https://oapi.saramin.co.kr/](https://oapi.saramin.co.kr/) 여기서 사용 신청을 하면된다.

<img src="/images/2024-07-11-etc-datily-프로젝트 설계/image-20240711155756417.png" alt="image-20240711155756417" style="zoom: 25%;" />



생각보다 적을게 많다..  참고로 귀찮아서 아무 이유나 쓰면 승인을 안해 줄 수 있기 때문에 아무말이나 쓰면 안된다.

<img src="/images/2024-07-11-etc-datily-프로젝트 설계/image-20240711155842056.png" alt="image-20240711155842056" style="zoom: 50%;" />

이메일, 이름, .. 을 작성하고 신청하기 버튼을 누르면 신청이 완료된다. 하지만 승인이 나기까지 생각보다 오래걸린다.

사실 이렇게 오래 걸릴지







