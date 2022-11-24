---
layout: post
title: "Web Bundling & Webpack usage"
date: 2022-11-24
categories:
  - Web
tags:
  - Javascript
  - Web
  - Bundle
  - Webpack
  - codestates
  - entry
  - output
  - loader
  - plugin
---

은에 빠졌다. 정군의 말에 따르면 반도체에 금이 은으로 대체된다고하니 지금은 은이고 성공하면 금으로 가자 꺄륵

오늘도 개발을 더 편하게 할 수 있게 자동으로 배포파일을 만들어주는 웹팩 가자.

---

## 1. without react

튜토리얼로 정리하려고 했더니 끝이없어.. 지금까지의 정리본은 보존하고, 최종코드와 필요한 명령어 및 중간중간의 첨언만 정리한다.

출처: [codestates](https://www.codestates.com)

```bash
# 1. 프로젝트폴더 생성
$npm init -y # 2. npm 초기화
# 3. src폴더 및 src/index.js 파일 생성
# 4. 동작을 담은 예시 action.js파일 생성
$npm install -D webpack webpack-cli # 5. 웹팩 설치
111111111111111111111111111111111111111111111111111
5.1. webpack을 이용해 하나로 합친다.
# #5.2. webpack은 번들링을 원하는 파일을 먼저 확인, import한 라이브러리나 코드가 있으면 해당 코드도 모두 인식하여 하나 의 번들안으로 모두 넌흔다. 번들링을 원하는 파일의 위치를 entry, 번들링의 결과물을 output
111111111111111111111111111111111111111111111111111
# 6. 웹팩 config파일 작성: entry와 output정보를 적을 수 있다.
$npx webpack # 7. 번들링하기
# 8. npm run build설정: npm run build script 추가
  #  package.json > "script" > "build": "webpack" 추가
# 9. src/index.html 생성
$npm i -D css-loader style-loader # 10. 로더 설치
  # 10.1. loader 설정이 없으면 require, css 등 에러발생
2222222222222222222222222222222222222222222222222222
# 10.2. loader Styling
  # style-loader: Add exports of a module as style to DOM
  # css-loader: Loads CSS file with resolved imports and return CSS code
  # less-loader: Loads and compiles a LESS file
  # sass-loader: Loads and complies a SASS/SCSS file
  # postcss-loader: Loads and transforms a CSS/SSS file using PostCSS
  # stylus-loader: Loads and complites a Stylus file
  # 10.3. loader: JS, json이 아닌 파일을 불러오는 역할을 한다.
22222222222222222222222222222222222222222222222222222
# 11. 파일트리
  # .
  # ├── LICENSE
  # ├── dist
  # │   └── app.bundle.js
  # ├── package-lock.json
  # ├── package.json
  # ├── src
  # │   ├── index.html # here
  # │   ├── index.js
  # │   ├── style.css
  # │   └── underbar.js
  # └── webpack.config.js
  #
  # 2 directories, 9 files
# 12. html webpack plugin: 번들링에 유용한 다양한 툴이 적용가능하다.
$npm i -D html-webpack-plugin
33333333333333333333333333333333333333333333333333333
# 12.1. plugin
  # 번들링 과정 중 개발자가 원하는 다양한 작업을 할 수 있도록 돕는다.
  # html-webpack-plugin은 번들링 과정 중 html파일을 자신이 원하는 형태로 가공하여 번들에 포함할 수 있게 돕는다.
33333333333333333333333333333333333333333333333333333
```

## 2. 완성코드

```html
<!-- ./src/index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="style.css" />
    <title>Shout Lorem Ipsum Once</title>
  </head>
  <body>
    <main>
      <h1>Shout Lorem Ipsum Once</h1>
      <div id="app"></div>
    </main>
    <script src="app.bundle.js"></script>
  </body>
</html>
```

```javascript
// ./src/index.js
const _ = require("./underbar.js");
require("./style.css");

const shout = (...sentences) => console.log(...sentences);
const shoutToHTML = (...sentences) => {
  const app = document.querySelector("#app");
  app.append(
    ...sentences.map((sentence) => {
      const shoutHere = document.createElement("div");
      shoutHere.className = "shout";
      shoutHere.textContent = sentence;
      return shoutHere;
    })
  );
  return;
};

const loremIpsum =
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis egestas feugiat elit, ac tincidunt neque vestibulum at. Mauris a eros sit amet urna efficitur tempus.";

const shoutOnce = _.once(shout);
const shoutToHTMLOnce = _.once(shoutToHTML);

shoutOnce(loremIpsum);
shoutOnce(loremIpsum);
shoutOnce(loremIpsum);
shoutOnce(loremIpsum);

shoutToHTMLOnce(loremIpsum);
shoutToHTMLOnce(loremIpsum);
shoutToHTMLOnce(loremIpsum);
shoutToHTMLOnce(loremIpsum);
```

```css
/* ./src/style.css */
/* dist/style.css */
* {
  box-sizing: border-box;
  border: 0;
  padding: 0;
  margin: 0;
}

main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

div.shout {
  padding: 12px;
  margin: 4px;
  border-radius: 8px;
  border: 0.5px solid gray;
}
```

```javascript
// ./src/underbar.js
const _ = {
  once(func) {
    // 아래 변수들은 아래 선언/리턴되는 함수 안에서 참조됩니다.
    // 리턴되는 함수의 scope 내에 존재하므로, 리턴되는 함수를 언제 실행해도 이 변수들에 접근할 수 있습니다.
    let result;
    let alreadyCalled = false;

    return function (...args) {
      // TIP: arguments 키워드 혹은, spread operator를 사용하세요.
      if (!alreadyCalled) {
        alreadyCalled = true;
        result = func(...args);
      }
      return result;
    };
  },
};

module.exports = _; // 다른 파일에서 사용할 수 있게 export
```

```json
// .package.json
{
  "name": "fe-sprint-webpack-tutorial",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "build": "webpack",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "devDependencies": {
    "css-loader": "^6.7.2",
    "html-webpack-plugin": "^5.5.0",
    "style-loader": "^3.3.1",
    "webpack": "^5.73.0",
    "webpack-cli": "^4.10.0"
  }
}
```

```javascript
// .webpack.config.js
const path = require("path");
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "app.bundle.js",
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"],
        exclude: /node_modules/,
      },
    ],
  },
  plugins: [new HtmlWebpackPlugin({
    template: path.resolve(__dirname, "src", "index.html")
  })]
};
```

## deprecated

```bash
# your home
$mkdir without-react
$cd without-react

# home/without-react
$npm init -y
Wrote to /home/ty/Workspace/without-react/package.json:

{
  "name": "without-react",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
$mkdir src
$cd src

# home/without-react/src
$touch action.js
$vim action.js
```

```javascript
// src/action.js
const _ = {
  once(func) {
    // 아래 변수들은 아래 선언/리턴되는 함수 안에서 참조됩니다.
    // 리턴되는 함수의 scope 내에 존재하므로, 리턴되는 함수를 언제 실행해도 이 변수들에 접근할 수 있습니다.
    let result;
    let alreadyCalled = false;

    return function (...args) {
      // TIP: arguments 키워드 혹은, spread operator를 사용하세요.
      if (!alreadyCalled) {
        alreadyCalled = true;
        result = func(...args);
      }
      return result;
    };
  },
};

module.exports = _; // 다른 파일에서 사용할 수 있게 export
```

```bash
# vim :wq 저장 후 종료
# home/without-react/src
$touch index.js
$vim index.js
```

```javascript
// src/index.js
const _ = require("./action.js");

const shout = (...sentences) => console.log(...sentences);
const shoutToHTML = (...sentences) => {
  const app = document.querySelector("#app");
  app.append(
    ...sentences.map((sentence) => {
      const shoutHere = document.createElement("div");
      shoutHere.className = "shout";
      shoutHere.textContent = sentence;
      return shoutHere;
    })
  );
  return;
};

const loremIpsum =
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis egestas feugiat elit, ac tincidunt neque vestibulum at. Mauris a eros sit amet urna efficitur tempus.";

const shoutOnce = _.once(shout);
const shoutToHTMLOnce = _.once(shoutToHTML);

shoutOnce(loremIpsum);
shoutOnce(loremIpsum);
shoutOnce(loremIpsum);
shoutOnce(loremIpsum);

shoutToHTMLOnce(loremIpsum);
shoutToHTMLOnce(loremIpsum);
shoutToHTMLOnce(loremIpsum);
shoutToHTMLOnce(loremIpsum);
```

```bash
# vim :wq 저장 후 종료
# home/without-react/src
$npm install -D webpack webpack-cli

$touch webpack.config.js
$vim webpack.config.js
```

```javascript
// webpack.config.js
const path = require("path");

module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.resolve(__dirname, "dist"), // './dist'의 절대 경로를 리턴합니다.
    filename: "app.bundle.js",
  },
};
```

```bash
# vim :wq 저장 후 종료
# home/without-react/src
$npx webpack
# dist/app.bundle.js 생성됬으면 빌드 성공

$..

# home/without-react
$vim packgae.json
```

```json
{
  "name": "fe-sprint-webpack-tutorial",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "build": "webpack", // 추가코드
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "devDependencies": {
    "webpack": "^5.73.0",
    "webpack-cli": "^4.10.0"
  }
}
```

```bash
# vim :wq 저장 후 종료
# home/without-react
$cd src

# home/without-react/src
$touch index.html
$vim index.html
```

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="style.css" />
    <title>Shout Lorem Ipsum Once</title>
  </head>
  <body>
    <main>
      <h1>Shout Lorem Ipsum Once</h1>
      <div id="app"></div>
    </main>
    <script src="app.bundle.js"></script>
  </body>
</html>
```

추후 과정의 경우에는 bundle로 지정한 dist폴더와 src폴더를 오가면서 동작을 이해시켜주는 과정이다. 최종코드와 문서를 확인하여 동작을 이해하는것이 더 효율적이다.

---

webpack도 사용하다보면 편리한 툴일 수 밖에 없을거란 생각이들고, 금일 들었던 github 배포방식만 제대로 알아도 따로 빌드해서 파일을 물리적으로 올려줄 필요없이, 기존 방식대로 git으로 push하는 방식을 사용할 수 있다.

---

## 참조

> [webpack.kr: main](https://webpack.kr/)   
> [webpack.org: main](https://webpack.js.org/)