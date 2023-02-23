---
title: "proxy server"
excerpt: ""

categorise:
  - Blog
tags:
  - Blog
---

# proxy server

우리가 vue 를 사용하여 웹 개발을 진행하고 vue에서 backend 서버에 있는 api를 접속할려고 할 때 우리는 cors라는 에러 문구를 많이 봤을것이다.
CORS 는 아래에서 정확히 설명 하겠지만 간단히 말하면 다른 출처에서 오는 리소스를 공유받는 것이다. cors가 나게 된다는 것은 다른 출처에서 값을 받아오기 떄문인대 이 문제를 vue에서는 porxy server를 구축하는 것으로 간단하게 해결 할 수 있다.

```ts
  server: {
    proxy: {
      '/api' :{
        target:'http://localhost:8080/',
        changeOrigin: true,
      }
    }    
  },
```
바로 위의 코드이다. config.ts 파일에 해당 부분을 입력하게 되면 웹에서 서버로 api를 보낼 때 {target}/api가 붙은 api는 porxy server를 거쳐서 사용하겠다는것이다. 