## 🚿 로컬 세팅

### commit 시 lint체크는 제거 함
  .husky/commitmsg 파일 제거

### 로컬 구동 전 assets 빌드

```bash
npm i && npm run build
```

### 로컬 구동

```bash
bundle exec jekyll serve
```

## 🥐 GitHub Actions

Github Pages의 Build and deployment를 `GitHub Actions`로 지정

자동으로 만들어지는 jekyll.yml 을 저장.

아마도 실패할 껀데 다시 로컬로 돌아와서 git pull 한 뒤에

예제로 들어있던 ./github/workflows/starter/pages-deploy.yml을 ./github/workflows/jekyll.yml 로 덮어 씌움

test 부분일 제거
```yml
- name: Test site
  run: |
    bundle exec htmlproofer _site \
      \-\-disable-external \
      \-\-ignore-urls "/^http:\/\/127.0.0.1/,/^http:\/\/0.0.0.0/,/^http:\/\/localhost/"
```

`Build site` 전 단계에 ci.yml의 `Setup Node, Build Assets`을 추가
```yml
- name: Setup Node
  uses: actions/setup-node@v4
  with:
    node-version: lts/*

- name: Build Assets
  run: npm i && npm run build
```


## 참고사이트

- [깃헙블로그만들기 (다소 오류가 있다)](https://devpro.kr/posts/Github-블로그-만들기-(4)/)
