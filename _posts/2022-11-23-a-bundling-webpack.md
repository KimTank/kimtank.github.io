---
layout: post
title: "Web Bundling & Webpack"
date: 2022-11-22
categories:
  - Web
tags:
  - Javascript
  - Web
  - Bundling
  - 
---

실제로 구현할때 마음대로 되지않는 것이 문제다. 덕분에 시간을 녹여버리고, 문서를 뒤지는 시간보다 구글링이 빠르다고 판단해서 그렇게했더니, 언제나 그렇듯이 문서가 최고다. 결과적으로는 문서를 참조하는것이 더 빠른경우가 많은거같다.

---

## 1. Bundle

Bundling이란 여러 제품이나, 코드, 프로그램을 묶어서 패키지로 제공하는 행위를 말한다. 저장공간에 한계가 있었던 과거에 플로피 디스크 여러장을 사용하여 게임을 했던것이나, 게임잡지를 사면 제공해주던 무료 cd역시 bundle의 한 예이다.

front-end developer에게는 사용자에게 웹애플리케이션을 제공하기 위한 파일 묶음이다.

### 2. Webpack

webpack은 bundler로 여러개의 파일을 하나로 합쳐주는 module bundler이다.

### 2.1. Module Bundler

HTML, CSS, JavaScript 등의 resouce를 각각 module로 보고 이를 합쳐 하나의 묶음으로 bundling, build한느 도구이다.

모던 웹의 시대로 접어들고, 발전하며 코드의 양이 증가했고, 고도화됨에 따라 유지보수비용이 늘어났고, 한정된 자원(ex. 하드웨어 등)에서의 비용도 고려하는 복잡성이 늘어감에 따라 시작점으로부터 dependancy를 가지는 module을 trace하여 결과물을 내는 module bundler가 등장하였다.

HTML, CSS, JavaScript, media 등의 resource를 loader를 통해 bundling이 가능하다.

- build: 개발이 완료된 앱을 배포하기 위해 한 폴더로 구성하여 준비하는 것을 의미한다.
- bundling: 묶음이라는 개념으로 파일을 묶는 작업 자체를 말하며, 의존적 관계에 있는 파일들(import, export) 자체 혹은 내부적으로 포함 되어 있는 모듈을 의미한다. 모듈간의 의존성을 파악해 그룹화하는 것이 정확하다.

### 2.2 개념

```javascript
0 module.exports = {
1   target: ["web", "es5"],
2   entry: "./src/script.js",
3   output: {
4     path: path.resolve(__dirname, "docs"),
5     filename: "app.bundle.js",
6     clean: true
7   },
8   module: {
9     rules: [
10      {
11        test: /\.css$/,
12        use: [MiniCssExtractPlugin.loader, "css-loader"],
13        exclude: /node_modules/,
14      },
15    ],
16  },
17  plugins: [
18    new HtmlWebpackPlugin({
19      template: path.resolve(__dirname, "src", "index.html"),
20    }),
21    new MiniCssExtractPlugin(),
22  ],
23  optimization: {
24    minimizer: [
25      new CssMinimizerPlugin(),
26    ]
27  }
28};
```

- target: 기본값(적용안할시)은 web, esX를 넣으면 지정된 ECMAScript버전으로 컴파일 할 수 있다. 브라우저와 동일한 환경에서 사용하기 위해 컴파일하는 버전(ex: ES5, ES6...)을 지정하는 것이다. Browser Compatibility와 연관된 속성이다.
- Entry: 시작점으로 index, main같이 웹페이지의 진입이 시작되는 곳을 말한다.
- Output: bundle을 내보낼 위치
- Loaders: Webpack은 JS와 JSON만 컴파일 가능하다. loader를 사용하면 다른 유형의 파일을 처리하거나, 그들을 유효한 module로 변환해 사용하거나 dependency graph에 추가할 수 있다.
  - test(필수): 변환이 필요한 파일들을 식별하기 위한 속성
  - use(필수): 변환을 수행하는데 사용되는 로더를 가르킴
  - exclude: 바벨로 컴파일하지 않을 파일이나 폴더를 지정
  - include: 반드시 컴파일해야될 파일이나 폴더 지정
  module.rules아래 정의하지 않고, rules아래 정의 시 warning throw
- Plugins: bundle을 최적화하거나 asset을 관리, 환경변수 주입 등의 광범위작업 수행 가능하다. require()을 통해 플러인을 요청, plugins 배열에 사용하고자 하는 plugin 추가한다. 대부분 플러그인은 사용자가 옵션을 통해 지정할 수 있다. 다른 목적으로 플러그인을 여러번 사용할 수 있기에 new 연산자를 사용해 호출하여 plugin의 instance를 생성해야한다.
- Optimization: 최척화에 대표적으로 minimize, minimizer가 있다.
  - minimize: TerserPlugin 또는 optimization.minimize에 명시된 plugins로 bundle파일을 최소로 압축시키는 작업 여부를 결정한다.
  - minmizer: default minimizer를 커스텀된 TerserPlugin instance를 제공해서 재정의 가능하다.
- Mode
  - 매개변수
    - development: 개발모드
    - production(default): 배포모드
    - none: 기본 최적화 옵션 설정 해제
- Browser Compatibility

---

실제로 설정 세팅을 하는 법은 따로 기록해야 기억할거라 예상함.

---

## 참조

> [webpack: 왜 웹팩이야?](https://webpack.kr/concepts/why-webpack/)   
> [webpack: main](https://webpack.kr/)   
> [github: mini-css-extract-plugin](https://github.com/webpack-contrib/mini-css-extract-plugin)   
> [github: css-minimizer-webpack-plugin](https://github.com/webpack-contrib/css-minimizer-webpack-plugin)   
> [webpack: output-management#cleaning-up-the-dist-folder](https://webpack.kr/guides/output-management/#cleaning-up-the-dist-folder)   
> [webpack: using-webpack-dev-server](https://webpack.kr/guides/development/#using-webpack-dev-server)   
> [webpack: target#string](https://webpack.kr/configuration/target/#string-1)   
> [webpack: concepts#loaders](https://webpack.js.org/concepts#loaders)   
> []()   
> []()   
> []()   
> []()   