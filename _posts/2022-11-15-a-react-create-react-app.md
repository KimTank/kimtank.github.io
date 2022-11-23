---
layout: post
title: "React create-react-app"
date: 2022-11-15
categories:
- React
tags:
- Javascript
- React
- npx
- npm
- template
- cra-template
- test
- build
- package.json
- src
- script
- eject
- polyfill
- es6
- exponentiation-operator
- rest
- spread
- proposal-dynamic-import
- proposal-class-public-fields
- jsx
- flow
- typescript
- browerslist
- babel-loader
- bundle
---

동생이 잘갔다. 온 친지들은 내가 동생인줄안다 히힛 좋아할거다. 안그러면 지는거같다. 어머니께서 가족들이 모인자리에서 "자식이 다 고만고만하면 걱정이 없지만, 하나는 잘살고 하나는 지지리도 궁상이면 걱정거리가 한가득"이라길래 왠지 찔렸다. 그래도 오랜만에 친지들과 어머니 아버지 지인들을 뵈서 좋았다. 좋다고 하자 아니면 지는거같다.

덤벼라 세상아 지지리 궁상맞을진 몰라도 다 박살내주지

---

## 1. create-react-app

원래 초기세팅이 오래걸린다. 그런걸로 보면 android는 매우 편하게 원하는 앱의 모양까지 초창기에 지정할 수 있다. 일반적으로 웹은 그런걸 본적이 없었는데 react는 지원하게 만들어놨다.(고마워 메타)

좀 더 들여다보자

## 2. 속성 시작

```bash
# path: 현재 경로에서 생성하고 싶으면 your-project-name, 그냥 거기 받고싶으면 .
$npx create-react-app {path}
# $cd your-project-name 경로에 생성하면 그경로로
$npm start
```

와아아아 설정이 한방에 끝.

## 3. template 지정

`--template [template-name]`옵션 추가로 템플릿을 입히고 시작할 수 있단다.

```bash
$npx create-react-app {path} --template [template-name]
```

[사용자 설정 템플릿 지정방법](https://create-react-app.dev/docs/custom-templates/)

문서는 늘 옳다. 문서를 읽자.

[npmjs: cra-template](https://www.npmjs.com/search?q=cra-template-*)

남에건 늘 옳지만은 않지만 생산성만은 무시할수없다.

```bash
$npx create-cra-template

# 각자 사용법이 다르다. 역시 남에겐 ㄷㄷ 문서와는 ㄷㄷ

$npx create-react-app %PROJECT_NAME% --template npm-library

$cd %PROJECT_NAME%
$node ./prepare.js
# makes required package.json configuration
```

## 4. 기본 제공 명령

- `npm start`: http://localhost:3000 지정 실행
- [`npm test`](https://create-react-app.dev/docs/running-tests): 기본적으로 마지막 커밋 이후 변경된 파일과 관련된 테스트를 실행한다.
- `npm run build`: 빌드를 하지 않으면 브라우저는 JSX를 모르기에 사용이 불가하다.

## 5. 폴더 구조

```
your-app/
  README.md
  node_modules/
  package.json
  public/
    index.html
    favicon.ico
  src/
    App.css
    App.js
    App.test.js
    index.css
    index.js
    logo.svg
```

- `public/index.html`페이지 템플릿
- `src/index.js` js 진입점
- `src` 내에서 webpack파일 처리

## 6. script

- `npm start`
- `npm test`
- [`npm run build`](https://create-react-app.dev/docs/production-build)
- `npm run eject`: 단일 빌드 종속성을 제거한다. 모든 구성파일과 전이적 종속성(webpack, Babel, ESLint 등) `package.json` 내를 재정렬하여 하는것이 낫다.
  - > 단방향적이다. 돌아갈수없음. 인생과 같네

## 7. 지원 브라우저 및 기능

### 7.1. 언어

IE 9, 10, 11 [폴리필](https://github.com/facebook/create-react-app/blob/main/packages/react-app-polyfill/README.md)이 필요하다.

- [ES6](https://github.com/lukehoban/es6features)
- [지수 연산자(ES2016)](https://github.com/rwaldron/exponentiation-operator)
- [오브젝트 레스트/스프레드 속성(ES2018)](https://github.com/tc39/proposal-object-rest-spread)
- [Dynamic import()](https://github.com/tc39/proposal-dynamic-import)
- [클래식 필드 및 정적 속성(3단계)](https://github.com/tc39/proposal-class-public-fields)
- [JSX](https://facebook.github.io/react/docs/introducing-jsx.html), [Flow](https://create-react-app.dev/docs/adding-flow), [TypeScript](https://create-react-app.dev/docs/adding-typescript)

[제안 단계](https://tc39.github.io/process-document/)

### 7.2. 지원 브라우저

[`browerslist`](https://github.com/browserslist/browserslist)구성이 파일에 포함된다. async/awit같은 언어 기능을 사용할 때 좋은 개발 환경을 제공하나 프로덕션 환경의 많은 브라우저와 호환성이 좋다. `package.json > 0.2%`

[지원브라우저를 확인할 수 있다.](https://browsersl.ist/#q=%3E+0.2%25%2C+not+dead%2C+not+op_mini+all) `build development start browserlist`

```json
"browerslist": {
  "production: [
    ">0.2%",
    "not dead",
    "not op_mini all"
  ],
  "development": [
    "last 1 chrome version",
    "last 1 firefox version",
    "last 1 safari version"
  ]
}
```

> 폴리필이 자동 포함되지 않으니, 지원하는 브라우저에 따라 필요한 언어 기능을 폴리필 해야한다.

> 편집 후 `browerslist`변경 사항이 즉시 적용되지 않는다. -> [`babel-loader`](https://github.com/babel/babel-loader/issues/690) `package.json`, 빠른 해결은 `node_modules/.cache`폴더 삭제 후 시도

---

## [8. Updating to New Releases](https://create-react-app.dev/docs/updating-to-new-releases)
## [9. Setting Up Your Editor](https://create-react-app.dev/docs/setting-up-your-editor)
## [10. Developing Components in Isolation](https://create-react-app.dev/docs/developing-components-in-isolation)
## [11. Analyzing the Bundle Size](https://create-react-app.dev/docs/analyzing-the-bundle-size)
## [12. Using HTTPS in Development](https://create-react-app.dev/docs/using-https-in-development)
## [13. Adding a Stylesheet](https://create-react-app.dev/docs/adding-a-stylesheet)
## [14. Adding a CSS Modules Stylesheet](https://create-react-app.dev/docs/adding-a-css-modules-stylesheet)
## [15. Adding a Sass Stylesheet](https://create-react-app.dev/docs/adding-a-sass-stylesheet)
## [16. Adding a CSS Reset](https://create-react-app.dev/docs/adding-css-reset)
## [17. Post-Processing CSS](https://create-react-app.dev/docs/post-processing-css)
## [18. Adding Images, Fonts, and Files](https://create-react-app.dev/docs/adding-images-fonts-and-files)
## [19. Loading .graphql Files](https://create-react-app.dev/docs/loading-graphql-files)
## [20. Using the Public Folder](https://create-react-app.dev/docs/using-the-public-folder)
## [21. Code Splitting](https://create-react-app.dev/docs/code-splitting)
## [22. Installing a Dependency](https://create-react-app.dev/docs/installing-a-dependency)
## [23. Importing a Component](https://create-react-app.dev/docs/importing-a-component)
## [24. Using Global Variables](https://create-react-app.dev/docs/using-global-variables)
## [25. Adding Bootstrap](https://create-react-app.dev/docs/adding-bootstrap)
## [26. Adding Flow](https://create-react-app.dev/docs/adding-flow)
## [27. Adding TypeScript](https://create-react-app.dev/docs/adding-typescript)
## [28. Adding Relay](https://create-react-app.dev/docs/adding-relay)
## [29. Adding a Router](https://create-react-app.dev/docs/adding-a-router)
## [30. Adding Custom Environment Variables](https://create-react-app.dev/docs/adding-custom-environment-variables)
## [31. Making a Progressive Web App](https://create-react-app.dev/docs/making-a-progressive-web-app)
## [32. Measuring Performance](https://create-react-app.dev/docs/measuring-performance)
## [33. Creating a Production Build](https://create-react-app.dev/docs/production-build)
## [34. Running Tests](https://create-react-app.dev/docs/running-tests)
## [35. Debugging Tests](https://create-react-app.dev/docs/debugging-tests)
## [36. Proxying API Requests in Development](https://create-react-app.dev/docs/proxying-api-requests-in-development)
## [37. Fetching Data with AJAX Requests](https://create-react-app.dev/docs/fetching-data-with-ajax-requests)
## [38. Integrating with an API Backend](https://create-react-app.dev/docs/integrating-with-an-api-backend)
## [39. Title and Meta Tags](https://create-react-app.dev/docs/title-and-meta-tags)
## [40. Deployment](https://create-react-app.dev/docs/deployment)
## [41. Custom Templates](https://create-react-app.dev/docs/custom-templates)
## [42. Can I Use Decorators?](https://create-react-app.dev/docs/can-i-use-decorators)
## [43. Pre-Rendering into Static HTML Files](https://create-react-app.dev/docs/pre-rendering-into-static-html-files)
## [44. Advanced Configuration](https://create-react-app.dev/docs/advanced-configuration)
## [45. Alternatives to Ejecting](https://create-react-app.dev/docs/alternatives-to-ejecting)
## [46. Troubleshooting](https://create-react-app.dev/docs/troubleshooting)

---

troubleshooting last updated 2/13/2020 by Lewis Llobera

양이 어마어마한지도 모르고 시작한 정리

react 세팅법이 다 나와있는거 같다.

---

## 참조

> [create-react-app: custom-templates](https://create-react-app.dev/docs/custom-templates/)   
> [npmjs: cra-template](https://www.npmjs.com/search?q=cra-template-*)   
> [npmjs: accordproject/concerto-ui-core](https://www.npmjs.com/package/@accordproject/concerto-ui-core)   
> [npmjs: create-cra-template](https://www.npmjs.com/package/create-cra-template)   
> [create-react-app: running-tests](https://create-react-app.dev/docs/running-tests)   
> [create-react-app: production-build](https://create-react-app.dev/docs/production-build)   
> [create-react-app: deployment](https://create-react-app.dev/docs/deployment)   
> [github: react-create-app/react-app-polifill](https://github.com/facebook/create-react-app/blob/main/packages/react-app-polyfill/README.md)   
> 본문 참조(너무많아요)