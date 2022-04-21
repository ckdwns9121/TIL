# React + Typescript + CEP Motion kits

# 개발 환경 설정

## 1. webpack 설치 및 셋팅

웹팩은 모듈 번들러 라이브러리 입니다.

### 프로젝트 설정하기

- 초기화 하기

```
$ yarn init -y
```

- 필요한 패키지 설치

```
$ yarn add -D @babel/core @babel/preset-env @babel/preset-react babel-loader clean-webpack-plugin css-loader html-loader html-webpack-plugin mini-css-extract-plugin node-sass react react-dom sass-loader style-loader webpack webpack-cli webpack-dev-server
```

### webpack.config.js 작성

```js
const path = require("path");

module.exports = {
  entry: "./src/test.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname + "/build"),
  },
  mode: "none",
};
```

- entry: 웹팩이 빌드할 파일을 알려주는 역할
- output: 웹팩에서 빌드를 완료하면 output에 명시되어 있는 정보를 통해 빌드파일 생성
- mode: 빌드 옵션

### package.json 수정

```json
{
  "scripts": {
    "build": "webpack"
  }
}
```

위와 같이 수정후 `yarn build` 명령어를 실행하면 `bundle.js` 파일이 나온다.

### 웹팩으로 HTML 빌드하기

웹팩은 자바스크립트 파일 뿐만아니라 HTML, CSS, IMAGE등의 파일도 모듈로 관리할 수 있다.

바로 웹팩에는 로더라는 기능이 있는데 로더는 자바스크립트 파일 이외의 파일을 웹팩이 이해할 수 있게 도와준다.  
로더를 사용하는 방법은 아래와 같다.

```
module : {
	rules: {
		test: '가지고올 파일 정규식',
		use: [
			{
				loader: '사용할 로더 이름',
				options: { 사용할 로더 옵션 }
			}
		]
	}
}
```

`public` 디렉토리에 `index.html` 파일을 만들고 html을 작성한다.

아래와 같이 `webpack.config.js`파일을 수정한다.

```js
const path = require("path");
const HtmlWebPackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: "./src/test.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname + "/build"),
  },
  mode: "none",
  module: {
    rules: [
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true },
          },
        ],
      },
    ],
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./public/index.html", // public/index.html 파일을 읽는다.
      filename: "index.html", // output으로 출력할 파일은 index.html 이다.
    }),
  ],
};
```

## 2. React 빌드하기

### index.jsx 작성

`src/index.jsx` 파일을 만들고 아래와 같이 작성한다.

```js
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

const rootNode = document.getElementById("root");

ReactDOM.createRoot(rootNode).render(<App />);
```

React18 버전 부터는 `ReactDOM.render`함수를 사용하면 오류가 발생하기 때문에 `ReactDOM.createRoot`함수를 사용한다.

### webpack에 바벨 옵션 추가

- 바벨은 es6문법을 다른 브라우저가 이해할 수 있게끔 변환해주는 트랜스파일러이다.

```js
{
    test: /\.(js|jsx)$/,
    loader: "babel-loader",
    options: {
        presets: ["@babel/preset-env", "@babel/preset-react"],
         plugins: ["@babel/plugin-proposal-class-properties"],
    },
},
```

이제 `webpack.config.js` 파일에 entry와 rules에 babel-loader를 추가한다.

```js
 entry: "./src/index.jsx",
 ...//
 rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: "/node_modules",
        use: ['babel-loader'],
      },
```

## 웹팩에서 CSS 사용하기

웹팩설정중 `yarn build`를 입력하면 css를 읽을 수 없다고 뜬다.  
css는 `css-loader`를 사용하면 CSS를 읽을 수 있다.

```js
rules: [
  {
    test: /\.css$/,
    use: ["css-loader"],
  },
];
```

하지만 build된 html 파일에서는 css가 없기 때문에 css 파일을 어딘가 저장해야한다.

webpack.config.js에 CSS를 추출해서 파일로 저장하는 플러그인을 적용해보자.

```js
const path = require("path");
const HtmlWebPackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname + "/client"),
  },
  mode: "none",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: "/node_modules",
        use: ["babel-loader"],
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true },
          },
        ],
      },
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, "css-loader"],
      },
    ],
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./public/index.html", // public/index.html 파일을 읽는다.
      filename: "index.html", // output으로 출력할 파일은 index.html 이다.
    }),
    new MiniCssExtractPlugin({
      filename: "style.css",
    }),
  ],
};
```

## 웹팩에서 SCSS 사용하기

웹팩에서 SCSS를 사용하려면 `sass-loader`를 사용하면 된다.

`webpack.config.js`에 아래와 같이 추가하자.

```js
{
    test: /\.scss$/,
    use: [MiniCssExtractPlugin.loader, "css-loader", "sass-loader"]
}
```

## 웹팩에서 svg 로드

```js
{
    test: /\.svg$/,
    loader: "file-loader",
},
```

## 웹팩에서 개발서버 사용하기

코드를 수정하면 바로바로 웹팩이 빌드해주는 `webpack-dev-server`가 있다.

webpack.config.js에 아래와 같이 추가해준다.

```js
devServer: {
    static: {
      directory: path.join(__dirname, "client"),
    },
    compress: true,
    port: 9000,
},
```

## 3. TypeScript 적용하기

### 패키지 설치

```
$ npm i -D typescript @babel/preset-typescript ts-loader fork-ts-checker-webpack-plugin
```

- typescript: Typescript(타입스크립트) 필수 라이브러리
- @babel/preset-typescript: babel(바벨)에서 Typescript(타입스크립트)를 빌드하기 위해 필료한 라이브러리
- ts-loader: Webpack(웹팩)에서 Typescript(타입스크립트)를 컴파일 하기 위해 필요한 라이브러리
- fork-ts-checker-webpack-plugin: ts-loader의 성능을 향상시키기 위한 라이브러리

### webpack.config.js 수정

```js
  entry: "./src/index.tsx",
    rules: [
      {
        test: /\.(ts|tsx)$/,
        use: "ts-loader",
        exclude: /node_modules/,
      },
    ],
  },
  resolve: {
    extensions: [".tsx", ".ts", ".js"],
  },
```

### 바벨 설정

```
$ npm install @babel/typescript
```

`루트디렉토리`의 `.babelrc`를 아래와 같이 수정

```json
{
  "presets": ["@babel/preset-env", "@babel/preset-react", "@babel/typescript"],
  "compact": false
}
```

## 4. React + TypeScript eslint, prettier 설정 방법

```
npm i -D eslint prettier
npm i -D @typescript-eslint/eslint-plugin @typescript-eslint/parser
npm i -D eslint-config-airbnb
npm i -D eslint-config-prettier eslint-plugin-prettier
npm i -D eslint-plugin-react eslint-plugin-react-hooks
npm i -D eslint-plugin-jsx-a11y eslint-plugin-import
```

### EsLint 설정

프로젝트 루트에 `.eslintrc.js`파일을 생성

```js
module.exports = {
  parser: "@typescript-eslint/parser",
  plugins: ["@typescript-eslint", "prettier"],
  extends: [
    "airbnb",
    "plugin:import/errors",
    "plugin:import/warnings",
    "plugin:prettier/recommended",
    "plugin:@typescript-eslint/recommended",
    "prettier/@typescript-eslint",
  ],
  rules: {
    "linebreak-style": 0,
    "import/prefer-default-export": 0,
    "prettier/prettier": 0,
    "import/extensions": 0,
    "no-use-before-define": 0,
    "import/no-unresolved": 0,
    "import/no-extraneous-dependencies": 0, // 테스트 또는 개발환경을 구성하는 파일에서는 devDependency 사용을 허용
    "no-shadow": 0,
    "react/prop-types": 0,
    "react/jsx-filename-extension": [2, { extensions: [".js", ".jsx", ".ts", ".tsx"] }],
    "jsx-a11y/no-noninteractive-element-interactions": 0,
  },
};
```

### Prettier 설정

프로젝트 최상단에 `.prettierrc` 파일을 생성

```json
{
  "singleQuote": true,
  "semi": true,
  "useTabs": false,
  "tabWidth": 2,
  "trailingComma": "all",
  "printWidth": 120,
  "arrowParens": "always"
}
```
