# yarn-workspaces-monorepo

<br />

모노레포 구조
```
apps
 ├── admin # 어드민 서비스
 └── cmc # 본 서비스
common
 ├── ui # 공유 컴포넌트
 └── utils # 공유 util 함수, 훅 등
```

<br />

1. yarn berry 세팅
```
yarn set version berry
```
```
// .yarnrc.yml
yarnPath: .yarn/releases/yarn-4.0.2.cjs
nodeLinker: node-modules
```
```
yarn install
```

<br />

2. yarn init
```
yarn init
```

<br />

3. root package.json 설정
```
{
  "name": "monorepo",
  "packageManager": "yarn@3.6.3",
  "private": true,
  "workspaces": {
    "packages": [
      "apps/*",
      "common/*"
    ]
  },
  "scripts": {
    "admin": "yarn workspace admin dev",
    "cmc": "yarn workspace cmc dev",
    "admin:build": "yarn workspace admin build",
    "cmc:build": "yarn workspace cmc build",
    "storybook": "yarn workspace ui storybook"
  }
}
```

<br />

4. tsconfig.json
```
{
  "compilerOptions": {},  // 공통 컴파일러 옵션
  "references": [  // root tsconfig.json에 개별 tsconfig.json 경로를 알려주는 역할
    {
      "path": "apps/admin"
    },
    {
      "path": "apps/test"
    },
    {
      "path": "common/ui"
    },
    {
      "path": "common/utils"
    }
  ],
  "exclude": ["node_modules"]
}
```

<br />

5. root 프로젝트 세팅 (react, emotion, typescript)
```
yarn add @emotion/react @emotion/styled
```
```
yarn add -D @types/eslint @types/node @types/react @types/react-dom @typescript-eslint/eslint-plugin @typescript-eslint/parser typescript
```
```
yarn add -D eslint eslint-config-prettier eslint-plugin-prettier eslint-plugin-react
```     

<br />

6. admin, cmc 프로젝트 세팅 (react, vite, typescript)
```
yarn init
```
```
yarn create vite admin --template react-ts
```
```
yarn workspace admin install
```
```
yarn workspace admin dev
```

<br />

7. ui 프로젝트 세팅 (storybook)
```
yarn init
```
```
yarn workspace ui dlx sb init --builder webpack5
```
```
// root package.json에 추가
"resolutions": {
    "webpack": "5",
    "@storybook/core-common/webpack": "^5",
    "@storybook/core-server/webpack": "^5",
    "@storybook/react/webpack": "^5"
},
```

<br />

8. utils yarn init
```
yarn init
```
