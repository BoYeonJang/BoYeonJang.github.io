---
layout: '../../layouts/PostLayout.astro'
title: 'Kyobook 팀 프로젝트 배포 (1/4)'
description: 'KAIT에서 주최한 2022년 제1기 ICT 경력전환 AI 교육(AI서비스 개발 과정)에서 2022년 07월 25일 ~ 10월 14일(약 3개월) 동안 교육을 받았다. 이 과정에서 진행된 팀 프로젝트를 단순 개발에서 끝내지 않고 배포까지하는 과정을 블로그에 남긴다.'
pubDate: 'Oct 18 2022'
heroImage: 'https://i.imgur.com/Q9U36kp.png'
---

<div tabindex="0" class="collapse collapse-arrow border border-base-300 bg-base-100 rounded-box">
  <input type="checkbox" /> 
  <div class="collapse-title text-xl font-medium">
    Kyobook 팀 프로젝트 배포
  </div>
  <div class="collapse-content"> 
    1. <a href="/blog/Kyobook-팀-프로젝트-배포-(1)" class="link-primary link-hover">Kyobook 팀 프로젝트 배포 (1/4)</a><br>
    2. <a href="/blog/Kyobook-팀-프로젝트-배포-(2)" class="link-hover">Kyobook 팀 프로젝트 배포 (2/4)</a><br>
    3. <a href="/blog/Kyobook-팀-프로젝트-배포-(3)" class="link-hover">Kyobook 팀 프로젝트 배포 (3/4)</a><br>
    4. <a href="/blog/Kyobook-팀-프로젝트-배포-(4)" class="link-hover">Kyobook 팀 프로젝트 배포 (4/4)</a>
  </div>
</div>
<br>

## 프로젝트 설명

[KAIT](https://www.kait.or.kr/)에서 주최한 [2022년 제1기 ICT 경력전환 AI 교육(AI서비스 개발 과정)](http://www.ict-aisw.kr/)에서 2022년 07월 25일 ~ 10월 14일(약 3개월) 동안 교육을 받았다. 이 과정에서 진행된 팀 프로젝트를 단순 개발에서 끝내지 않고 배포까지하는 과정을 블로그에 남긴다.

프로젝트 명은 `고객 리뷰 데이터를 활용한 ‘도서 구매 보조 솔루션’`이다. 간단하게 어떤 프로젝트인지 설명하자면 [교보문고](https://www.kyobobook.co.kr/)와 [yes24](http://www.yes24.com/Main/default.aspx)의 리뷰 데이터를 크롤링을 통해 수집하고 [KoBERT](https://github.com/SKTBrain/KoBERT)와 [KoGPT2](https://github.com/SKT-AI/KoGPT2) 모델로 학습하여 고객의 생각을 토대로 어떤 책이 알맞을지 추천해준다.

개발은 여기 [repository](https://github.com/BoYeonJang/kyobobook-review)에서 진행하였고, 폴더 구조는 다음와 같다.

```zsh
├── backend/
│   ├── ...
│   ├── app.py
│   ├── wsgi.py
│   ├── Dockerfile
│   └── README.md
├── frontend/
│   ├── ...
│   ├── src/
│   │   ├── components/
│   │   └── App.vue
│   ├── api.js nginx.conf
│   ├── nginx.conf
│   ├── Dockerfile
│   └── README.md
├── Code/
│   ├── Analysis/
│   ├── Classification/
│   ├── Crawling/
│   └── README.md
├── Data/
│   ├── 리뷰순/
│   ├── 모델/
│   │   ├── 분류기/
│   │   │   └── checkpoint-doccls/
│   │   └── 생성기/
│   │   │   └── checkpoint-generation/
│   ├── 분야별/
│   └── Top3/
├── docker-compose.yml
├── Pipfile
└── README.md
```

크게 `frontend`폴더와 `backend`폴더 그리고 크롤러 및 데이터 전처리를 진행하는 `Code`폴더와 크롤링을 통해 수집된 .csv파일과 모델이 저장 되있는 `Data`폴더로 나뉜다.

## 홈페이지

![Imgur](https://i.imgur.com/rLADWkp.png)
크롤링을 통해 수집된 리뷰 데이터를 `KoBERT` 모델로 학습하여 사용자의 생각을 입력하면 이에 알맞는 분야와 그 안에 있는 책 4권을 추천해준다.

![Imgur](https://i.imgur.com/ImYQEIY.png)
책 제목을 클릭하게 되면 해당하는 책의 워드클라우드를 보여준다.

![Imgur](https://i.imgur.com/FyEQqPW.png)
![Imgur](https://i.imgur.com/9uUQROz.png)
똑같이 수집되어 전처리를 통해 가공한 리뷰 데이터를 `KoGPT2` 모델로 학습하여 해당 책에 대한 한줄평을 보여준다.

![Imgur](https://i.imgur.com/ANJj7YN.png)

Front-end의 경우 [Vercel](https://vercel.com/)에서 배포하기로 하였고, Back-end의 경우 [AWS Elastic Beanstalk](https://aws.amazon.com/ko/elasticbeanstalk/)으로 배포하기로 하였다.

이를 배포하는 과정은 다음 포스트에서 진행하겠다. [Kyobook 팀 프로젝트 배포 (2/4)](</blog/Kyobook-팀-프로젝트-배포-(2)>)
