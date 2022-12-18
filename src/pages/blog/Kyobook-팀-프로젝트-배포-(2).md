---
layout: '../../layouts/PostLayout.astro'
title: 'Kyobook 팀 프로젝트 배포 (2/4)'
description: 'KAIT에서 주최한 2022년 제1기 ICT 경력전환 AI 교육(AI서비스 개발 과정)에서 2022년 07월 25일 ~ 10월 14일(약 3개월) 동안 교육을 받았다. 이 과정에서 진행된 팀 프로젝트를 단순 개발에서 끝내지 않고 배포까지하는 과정을 블로그에 남긴다.'
pubDate: 'Oct 21 2022'
heroImage: 'https://i.imgur.com/Q9U36kp.png'
---

<div tabindex="0" class="collapse collapse-arrow border border-base-300 bg-base-100 rounded-box">
  <input type="checkbox" /> 
  <div class="collapse-title text-xl font-medium">
    Kyobook 팀 프로젝트 배포
  </div>
  <div class="collapse-content"> 
    1. <a href="/blog/Kyobook-팀-프로젝트-배포-(1)" class="link-hover">Kyobook 팀 프로젝트 배포 (1/4)</a><br>
    2. <a href="/blog/Kyobook-팀-프로젝트-배포-(2)" class="link-primary link-hover">Kyobook 팀 프로젝트 배포 (2/4)</a><br>
    3. <a href="/blog/Kyobook-팀-프로젝트-배포-(3)" class="link-hover">Kyobook 팀 프로젝트 배포 (3/4)</a><br>
    4. <a href="/blog/Kyobook-팀-프로젝트-배포-(4)" class="link-hover">Kyobook 팀 프로젝트 배포 (4/4)</a>
  </div>
</div>
<br>

# Front-end 배포

## Netlify 설정

Front-end의 경우 [Vercel](https://vercel.com/)에서 배포하기로 했다. 정적 페이지를 배포하는 방법에 있어서 [Netlify](https://www.netlify.com/)이나 [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages)등 여러가지 방법이 있지만 `Vercel`에서 배포해 본 경험이 있기에 선택했다.

계정을 생성하고 나의 `GitHube` 계정을 연동했다.

![Imgur](https://i.imgur.com/M24vCaR.png)
연동 시에 나의 `repository`가 전부 나오게 되는데 거기서 이번에 배포할 [kyobobook-review](https://github.com/BoYeonJang/kyobobook-review)를 선택했다.

![Imgur](https://i.imgur.com/iAKPzK4.png)
폴더 구조가 나오고 배포할 `frontend` 폴더를 골랐다. Vue.js로 만들었기에 로고가 자동으로 나온다.

![Imgur](https://i.imgur.com/OMdslNg.png)
`Build and Output Settings`은 따로 건드리지 않아도 될 것 같아서 그대로 나두었다.

![Imgur](https://i.imgur.com/1pjypGR.png)
`Deploy`을 눌러 front-end를 배포한다.

![Imgur](https://i.imgur.com/Use7psa.png)
배포했다.

물론 정적 페이지이기 때문에 화면만 보이는 것이고 back-end를 연결해주어야한다.

![Imgur](https://i.imgur.com/3zPeDfn.png)
[https://kyobobook-review.vercel.app/](https://kyobobook-review.vercel.app/) 해당 주소로 접속하면 front 화면이 정상으로 나오는 것이 보인다. 입력창에 post 요청을 보내면

![Imgur](https://i.imgur.com/bboogqS.png)
back-end가 연결되어 있지 않기 때문에 API 요청이 실패하는 것을 볼 수 있다.

## Custom Domain 설정

```
https://neon-pony-14a28c.netlify.app
```

배포 후에 위와 같은 주소를 받는데 이를 개인 도메인으로 변경해보겠다. 개인 도메인이 없다면 위 경로를 사용하면 된다.

개인 도메인의 경우 여러 사이트에서 구매하고나 무료 도메인 사이트를 통해 구할 수 있지만 우리는 [Amazon Route 53](https://docs.aws.amazon.com/ko_kr/Route53/latest/DeveloperGuide/domain-register.html)에서 구매하였다.

![Imgur](https://i.imgur.com/f9cUigE.png)
오른쪽 상단에서 `View Domains`을 눌러 도메인 설정 페이지로 이동한다.

![Imgur](https://i.imgur.com/3lMD8T3.png)
구매한 주소를 입력해주고 `Add`를 눌러 추가한다.

![Imgur](https://i.imgur.com/7nipsCW.png)
세 가지 옵션 중에서 첫 번째는 www.도메인을 기본 도메인으로 설정하고 URL로 접속 시 리다이렉트한다.

두 번째는 www를 제외한 주소를 기본 도메인으로 설정하고 URL로 접속 시 리다이렉트한다.

세 번째는 도메인을 추가만 한다.

난 첫 번째를 선택했다.

## DNS 설정

![Imgur](https://i.imgur.com/eUCWfYF.png)

![Imgur](https://i.imgur.com/UBA6ODx.png)

화면에 나온 A Record와 CNAME를 설정해 주어야 하는데 도메인 구매한 곳에서 해주면 된다.

나는 Route 53에서 구매했기 때문에 거기서 설정했다.

![Imgur](https://i.imgur.com/iBmFr0C.png)
`레코드 생성`을 누른다.

![Imgur](https://i.imgur.com/zlxGLhf.png)
`레코드 유형`을 설정대로 A로 선택 후 값에 IP을 넣어주면 된다.

![Imgur](https://i.imgur.com/ZJXW6lG.png)
CNAME도 마찬가지로 `레코드 유형`을 선택해주고 레코드 이름에 www를 추가해주어야지 레코드 생성이 가능하다.

![Imgur](https://i.imgur.com/Oj2Pay8.png)
`Vercel`로 돌아와 새로고침 한 번 해주면 바뀐 도메인으로 접속이 된다.

## 배포 완료

front-end을 `Vercel`을 통해 배포 성공적으로 배포하였다. 프로젝트를 수정하여 본인 `GitHub`에 푸쉬한다면 `Vercel`에서 설정을 한 것대로 자동으로 빌드하여 배포한다. 이 후 자동 배포까지는 최대 5분 정도가 소요된다.

back-end을 배포하는 과정은 다음 포스트에서 진행하겠다. [Kyobook 팀 프로젝트 배포 (3/4)](</blog/Kyobook-팀-프로젝트-배포-(3)>)
