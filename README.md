# 제로초 TypeScript + React 강좌.
## 강좌 1일차(2월3일)
* 링크
  - [TypeScript 공식문서](https://www.typescriptlang.org/)
  - [zerocho github ts-react](https://github.com/ZeroCho/ts-react)

* IDE 선택
  - jet brains의 [webstorm](https://www.jetbrains.com/ko-kr/webstorm/)
  - [Visual Studio Code](https://code.visualstudio.com/)

* 시작
* npm init
  - package.json 생성됨.
* npm i typescript.. 등등 설치
* babel을 쓰진 않을거지만 쓰는경우도 있음.
* webpack과 typescript를 이어주는 loader가 필요. 
  - ts-loader가 있으나 이건 안쓰고 awesome-typescript-loader를 쓸꺼임.
    - useBabel이라는 옵션이 있어서 babel과 함께 쓸수 있다.
    - 뭔가 처리해서 빠르다.
    - 뭐 이런저런 이유로 awesome을 쓸거임.
* react, react-dom둘다 js로 만들어져있고 자체적으로 types를 제공하지 않음
  - 그래서 definitelyTyped에서 찾아서 설치 해야함.
  - npm i @types/react   npm i @types/react-dom 설치
* npx webpack이렇게 실행해서 쓸꺼임.
* 가끔 커뮤니티의 @types가 버전을 못따라가는 경우가 있어서 서로 호환이 안될 경우도 가끔있음... 하지만 첫째 자리가 버전이 맞으면 맞다고 할 수 있음.
* webpack셋팅은 react무료강좌에서 참고해도 됨.
* ts설정은 tsconfig.json 
```
"compilerOptions": {
    "strict": true,
    "lib": [
        "es5",
        "es2015",
        "dom",
    ],
    "jsx": "react",
}
```
* webpack.config.js 설정
```
const webpack = require('webpack');

module.exports = {
    mode: 'development', // production
    devtool: 'eval',    // hidden-source-map
    resolve: {
        extensions: ['jsx', 'js', 'tsx', 'ts'],
    },
    entry: {
        app: './client'
    },
    module: {
        rules: [{
            test: /\.tsx?$/,
            loader: 'awesome-typescript-loader',
        }]
    },
    plugins: [
        new webpack.LoaderOptionsPlugin({debug: true}),
    ],
    output: {
        filename: '[name].js',
        path: path.join(__dirname, 'dist'),
    }
}
```

* 코딩은 client.tsx에서 하지만 결과는 dist/app.js에 만들어 지므로 index.html 에 script를 dist/app.js를 로드한다.
* react는 export default가 없으므로 import react from ... 이렇게 쓰지 않고 import * as react from ... 이렇게 쓴다.
  - 그냥 import하려면 tsconfig.json에 esModuleInterop: true한다... 하지만 왠만하면 이렇게 하지 않는다... 모듈시스템 이해를 위해.
* client.tsx에 구구단 코딩을 한다.
* 코딩방식을 훅스방식, class방식 두가지를 한다. 먼저 훅스방식을 먼저한다.
* <></> 이거 하려면 import * as React from 'react';를 꼭 해줘야 한다. // React.Fragment
* e파라미터 event를 함수랑 같이 쓰면 타입추론이 되지만 함수를 따로 빼면 type추론이 안돼므로 type을 적어줘야한다.
* client.tsx코딩을 하고 빌드를 해서 index.html열어 확인해보기.
* npx webpack해서 빌드해서 확인해보기.
* 저장 확인하기.
* 첫번째 예제 실습 완료.
* 훅스방식 코드완료.
* CLASS방식의 코드 작성.
  - 컴포넌트는 제너릭첫번재 props, 두번째 state이다.
  - 함수나 class가 타입추론을 하지 못하면 손 올려보고 제너릭을 쓴다.
* 코드는 github에서 확인하여 직접 실행해보기.
* 2강 끝말잇기 코딩 진행.
  - npm i react-hot-loader를 설치
    - import {hot} form 'react-hot-loader/root';  이것은 d.ts를 제공해줌.
    - 하이오더 import WordRelay from './WordRelay'; const Hot = hot(WordRelay); // hoc 이것을 시작점에 코딩한다.
  - useCallback 함수 공부를 위한 강좌.
  - 제너릭 사용 여러가지 방법 코딩.
  - class버전 코딩.



### SideBar.vue
* 메뉴 데이터에서 가져와 보여주기.
  - [X] 데이터는 store에 만들어서 가져오기.
  - [X] store개발방법 정리.
* 메뉴 클릭시 화면전환 라우터 작업하기.
  - [X] 메뉴클릭시 화면전환
  - [ ] 화면이동 후 메뉴선택 모양 UI 유지