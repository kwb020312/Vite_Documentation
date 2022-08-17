# ⚡Vite

<img src="https://camo.githubusercontent.com/61e102d7c605ff91efedb9d7e47c1c4a07cef59d3e1da202fd74f4772122ca4e/68747470733a2f2f766974656a732e6465762f6c6f676f2e737667" />

해당 저장소는 요즘 급속도로 Vite가 유행해서 맛보고 싶어짐

본인 참지못하고 저장소 생성

# 😘시작하기-개요

Vite("빠른"에 대한 프랑스어 단어, 발음`/vit/`, 🔊"veet"과 같은)는 최신 웹 프로젝트에 `더 빠르고 간결한 개발 경험을 제공하는 것을 목표`로 하는 빌드 도구입니다. 두 가지 주요 부분으로 구성됩니다.

## 🎐설치

```npm
$ npm create vite@latest
```

```yarn
$ yarn create vite
```

### 템플릿 및 프로젝트명 지정

vue.js 기준

```
# npm 6.x
npm create vite@latest my-vue-app --template vue

# npm 7+, extra double-dash is needed:
npm create vite@latest my-vue-app -- --template vue

# yarn
yarn create vite my-vue-app --template vue

# pnpm
pnpm create vite my-vue-app --template vue
```

<img src="https://user-images.githubusercontent.com/46777310/185136822-aed7eb04-4c84-49a2-ae9d-8a0ba7cb6a54.png" />

리액트 설치 명령어는 위와 같았음

<img src="https://user-images.githubusercontent.com/46777310/185137977-16d1f5a1-ad57-4464-a248-54800aeeb93e.png" />

폴더 구조는 위와 같아용

# 🎃특징

## NPM 종속성 해결 및 사전 번들링

Vite에서 모듈 가져오기로 아래와 같은 형식은 지원하지 않습니다.

```javascript
import { someMethod } from "my-dep";
```

페이지 로딩 속도 향상 및 빠른 스타트를 위한 방안임

`/node_modules/.vite/deps/my-dep.js?v=f3sf2ebd` 브라우저에서 제대로 가져올 수 있도록 URL로 불러올 수 있음

_핫 리로딩_ 지원으로 새로고침과 동시에 자동으로 최신 내용을 반영합니다.

# 🙃플러그인 사용

플러그인 사용에 앞서 `devDependencies` 에 내용을 추가해야한다. `vite.config.js`를 생성하여 진행해보자면

우선 모듈을 설치한다

```npm
$ npm add -D @vitejs/plugin-legacy
```

```javascript
// vite.config.js
import legacy from "@vitejs/plugin-legacy";
import { defineConfig } from "vite";

export default defineConfig({
  plugins: [
    legacy({
      targets: ["defaults", "not IE 11"],
    }),
  ],
});
```

위는 플러그인 사용에 앞선 우선 준비과정이다.

링크 버전 및 목록과 소개는 <a href="https://vitejs.dev/plugins/">위 공식링크</a>에 기재되어있음

## 예시

```javascript
// image 플러그인을 가져옴
import image from "@rollup/plugin-image";
import { defineConfig } from "vite";

export default defineConfig({
  plugins: [
    {
      // Spread 연산자 이후 함수호출로 플러그인 사용
      ...image(),
      enforce: "pre",
    },
  ],
});
```

## 🥂종속성 사전 번들링

```
Pre-bundling dependencies:
  react
  react-dom
(this will be run only when your dependencies or config have changed)
```

Vite를 처음 실행하면 위와같은 메시지가 표시될 수 있다.

기존 CommonJS 또는 UMD로 제공되는 코드를 `Vite`는 `ESM`으로 변환하는 과정을 거치는데 이유는 기존의 많은 요청을 요구하는 모듈을 가볍게 변환하는 과정이라 생각하면 편하다
