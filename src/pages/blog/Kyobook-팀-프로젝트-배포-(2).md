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

Front-end의 경우 [Netlify](https://www.netlify.com/)에서 배포하기로 했다. 정적 페이지를 배포하는 방법에 있어서 [Vercel](https://vercel.com/)이나 [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages)등 여러가지 방법이 있지만 `Netlify`가 간단해 보여 선택했다. 실제로도 간단하다.

우선 계정이 없다면 만들어야 한다. 나는 처음이니 계정 생성부터 진행하였다.

![Imgur](https://i.imgur.com/KsQFonj.png)
`Sign up`으로 계정을 생성하면 첫 번째 프로젝트를 연결하라고 한다.

![Imgur](https://i.imgur.com/xfth133.png)
`GitHube` 계정을 연동한다. `GitLab`이나 `Bitbucket`, `Azure DevOps`의 계정을 연동할 수도 있다.

![Imgur](https://i.imgur.com/GTWrspU.png)
계정을 연동하면 내 `repository`가 전부 나오게 된다. 거기서 배포할 [repository](https://github.com/BoYeonJang/kyobobook-review)를 선택했다.

![Imgur](https://i.imgur.com/Z09RRl0.png)
`Branch`도 선택한다. 우리는 별도로 나누지 않고 `main branch`하나에 개발했다.

![Imgur](https://i.imgur.com/Ie48CSI.png)
`build Setting`을 해준다.

`Base directory`을 설정한다.<br>
front 개발 폴더가 root에 위치한다면 상관없지만 우리 `repository` 개발 폴더의 경우 backend와 모델 폴더, 크롤러 폴더가 전부 같이 있기 때문에 `frontend`로 front 폴더를 가리키게 해주었다.

다음으로 `Build command`을 설정한다.<br>
각자의 커맨드로 build용 커맨드를 적어주면 되는데 Vue CLI의 경우 `npm run build`로 빌드하기에 이를 적어주었다. 필요하지 않다면 적어주지 않아도 된다.

마지막으로 `Public director`을 설정한다.<br>
public/이나 dist/가 정적 경로이다. 나는 dist/로 적어주었다.

`Deploy site`을 눌러 front-end 사이트를 배포한다.

![Imgur](https://i.imgur.com/Tw4KW9T.png)
바로 배포가 되는 것은 아니고 조금 기다려야 한다.

![Imgur](https://i.imgur.com/PwCgyXy.png)
약간의 로딩이 끝나고 해당 주소로 frontend 정적 페이지가 배포되었다.

![Imgur](https://i.imgur.com/3zPeDfn.png)
해당 주소로 접속하면 front 화면이 정상으로 나오는 것이 보인다. 입력창에 post 요청을 보내면

![Imgur](https://i.imgur.com/bboogqS.png)
back-end가 실행되지 않았기 때문에 API 요청이 실패하는 것을 볼 수 있다.

## Custom Domain 설정

```
https://neon-pony-14a28c.netlify.app
```

배포 후에 위와 같은 주소를 받는데 이를 개인 도메인으로 변경해보겠다. 개인 도메인이 없다면 위 경로를 사용하면 된다.

개인 도메인의 경우 여러 사이트에서 구매하고나 무료 도메인 사이트를 통해 구할 수 있지만 우리는 [Amazon Route 53](https://docs.aws.amazon.com/ko_kr/Route53/latest/DeveloperGuide/domain-register.html)에서 구매하였다.

![Imgur](https://i.imgur.com/hAiWdB2.png)
`Set up a custom domain`을 눌러 도메인을 연결한다.

![Imgur](https://i.imgur.com/N3L8QcB.png)
`Custom domain`에 도메인을 입력한 후 `Verify` 버튼을 누른다.

![Imgur](https://i.imgur.com/59Wedhl.png)
다른 곳에서 구매한 도메인이기 때문에 이미 등록되어 있다고 알려준다. 이를 Netlify에 위임한다.

## DNS 설정

![Imgur](https://i.imgur.com/Axmttb4.png)
위임 후 사용자 지정 도메인에 대해 인증서를 프로비저닝할 수 없다고 오류가 나온다. DNS 설정을 해주어야한다.

![Imgur](https://i.imgur.com/AfjXDMg.png)
`Check DNS configuration`을 눌러 도메인을 설정하기 위한 지침을 볼 수 있다.

![Imgur](https://i.imgur.com/pRyOziF.png)
설정대로 레코드 유형을 Route53에서 설정해보겠다.

![Imgur](https://i.imgur.com/iBmFr0C.png)
`레코드 생성`을 누른다.

![Imgur](https://i.imgur.com/zlxGLhf.png)
`레코드 유형`을 설정대로 A로 선택 후 값에 IP을 넣어주면 된다.

![Imgur](https://i.imgur.com/rbtam68.png)
`레코드 생성`을 눌러 완료하고 `Netlify`으로 돌아와보면 사이트 주소가 우리의 도메인으로 바뀌어서 정상적으로 접속이 된다.

![Imgur](https://i.imgur.com/d6w6Gig.png)
인증서가 발급되어 사이트에 HTTPS가 활성화 된 것을 볼 수 있다.

## 배포 완료

front-end을 `Netlify`을 통해 배포 성공적으로 배포하였다. 프로젝트를 수정하여 본인 `GitHub`에 푸쉬한다면 `Netlify`에서 설정을 한 것대로 자동으로 빌드하여 배포한다. 이 후 자동 배포까지는 최대 5분 정도가 소요된다.

back-end을 배포하는 과정은 다음 포스트에서 진행하겠다. [Kyobook 팀 프로젝트 배포 (3/4)](</blog/Kyobook-팀-프로젝트-배포-(3)>)
