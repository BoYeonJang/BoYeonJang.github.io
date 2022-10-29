---
layout: '../../layouts/PostLayout.astro'
title: '명령줄 도구가 macOS 13을 지원하지 않는 오류'
description: 'Error: Your Command Line Tools (CLT) does not support macOS 13.
It is either outdated or was modified.
Please update your Command Line Tools (CLT) or delete it if no updates are available.'
pubDate: 'Oct 30 2022'
heroImage: 'https://i.imgur.com/UTnS79d.png'
---

```json
Error: Your Command Line Tools (CLT) does not support macOS 13.
It is either outdated or was modified.
Please update your Command Line Tools (CLT) or delete it if no updates are available.
Update them from Software Update in System Preferences or run:
  softwareupdate --all --install --force

If that doesn't show you any updates, run:
  sudo rm -rf /Library/Developer/CommandLineTools
  sudo xcode-select --install

Alternatively, manually download them from:
  https://developer.apple.com/download/all/.
You should download the Command Line Tools for Xcode 14.1.
```

`pscale`을 설치하려할 때 위와 같은 오류가 나왔다. 마침 `macOS Ventura`업데이트가 있어서 업데이트 했더니 오류가 나온 것 같았다.

```
sudo rm -rf /Library/Developer/CommandLineTools
```

```
sudo xcode-select --install
```

오류 메시지대로 최신버전으로 `Xcode 14.1`도 설치하고 위 커맨드도 실행해봤지만 해결되지 않았다. 하지만 역시 구글신은 답을 알고 있었다. 나와 같은 오류가 레딧에 올라와있었고 답변대로 커맨드 실행하여 해결했다. [출처](https://www.reddit.com/r/MacOSBeta/comments/xdptho/ventura_and_xcode_clt/)

```zsh
sudo rm -rf /Library/Developer/CommandLineTools
```

```zsh
# Xcode가 베타일 때
sudo xcode-select --switch /Applications/Xcode-beta.app

# Xcode가 베타가 아닐 때
sudo xcode-select --switch /Applications/Xcode.app
```

```zsh
brew doctor
```

![Imgur](https://i.imgur.com/ZD1NyZe.png)
해결 완료
