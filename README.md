# Lerna

Lerna 는 여러 프로젝트 를 관리하도록 도와주는 도구 이다. Lerna 를 이용하면, Mono Repo 를 구성하는데, 도움을 받을 수 있다.

> Mono Repo: 분산되어 관리되는 여러 Repository 를 한 Repository 안에서 관리

## 시작

관리하고자 하는 프로젝트에서 `npx lerna init` 명령을 실행하면 다음과 같은 파일들이 생성된다.

```
packages/*
lerna.json
package.json
```

Lerna는 `lerna.json` 파일의 설정 정보를 참조하여 프로젝트들을 관리한다.

```json
{
  "npmClient": "yarn",
  "bootstrap": {
    "ignore": "",
    "npmClientArg": []
  },
  "useWorkspaces": true,
  "packages": [
    "packages/*"
  ],
  "version": "0.0.1"
}
```

## 하위 프로젝트 관리 명령어

### 1. bootstrap

Lerna는 `lerna bootstrap --hosit` 명령을 통해 ignore로 설정된 프로젝트를 제외한 하위 프로젝트의 의존성들을 설치할 수 있다. 이때 공통된 module들은 root에 설치, 버전이 다른 경우는 warning을 출력하고 packages의 node_modules에 설치된다.

가끔 설치가 꼬이는 경우 `### 3. lerna clean` 으로 모든 package 의 node_modules 를 삭제하고 다시 설치할 수 있다.

### 2. link convert

`lerna link convert` 명령어를 실행하면, 모든 package 에 설정된 devDependencies 을 root devDependencies 으로 옮길 수 있다.


### 3. clean

`lerna clean` 명령어를 통해 관리 대상 프로젝트들의 node_modules를 비워준다.

### 4. exec

`lerna run --[option] [command]` 명령어를 통해 하위 프로젝트들에서 명령을 실행할 수 있다.

#### --scrope

`--scrope` 옵션은 인자로 들어온 패턴과 프로젝트들의 package.json 내 name과 일치한다면 해당 명령어를 실행시켜준다.

`lerna run --parallel --scrope @packages/* yarn build`

#### --parallel

명령을 병렬로 실행시켜주는 옵션이다.

#### --stream

명령의 결과를 지금 쓰는 터미널에서 확인할 수 있게 해준다.

### 5. run

root 에서 `lerna run --scope [package-name] [script command]` 로 실행하면 root 에 있는 devDependencies 를 참조할 수 있게 된다.

여기에서 `lerna run` 명령어는 package.json 에 있는 script 를 실행시킨다. 

```
lerna run --scope @packages/* start
```

## 참고자료

- [Lerna Docs](https://github.com/lerna/lerna)
- [Mono Repo 를 위한 Lerna 간단 정리하기](https://medium.com/@pks2974/mono-repo-%EB%A5%BC-%EC%9C%84%ED%95%9C-lerna-%EA%B0%84%EB%8B%A8-%EC%A0%95%EB%A6%AC%ED%95%98%EA%B8%B0-65c22029988)
