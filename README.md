# What do you say - Server

![What do you say Server - CI](https://github.com/Nexters/what-do-you-say-server/workflows/What%20do%20you%20say%20Server%20-%20CI/badge.svg)
![Production Server Deploy to AWS EC2](https://github.com/Nexters/what-do-you-say-server/workflows/Production%20Server%20Deploy%20to%20AWS%20EC2/badge.svg)

### :question: 뭐라하지? - 인사말을 대신 작성해주는 서비스

<br>

## :rocket: Main Modules

- `express`
- `awilix`
- `awilix-express`
- `mysql2`
- `typeorm`
- `ts-jest`

<br>

## :octocat: Git Branch Strategy

- 3개의 브랜치로 구성되어 있다. (`feature/issue-이슈번호` -> `dev` -> `master` 순으로 작업해야 함)

  - `master`
  - `dev`
  - `feature/issue-이슈 번호`

- `dev` 브랜치를 clone 받은 후(Repository Fork :x:), `feature/issue-이슈 번호` 브랜치를 만들어서 개발한다.

  ```zsh
  # dev branch clone
  $ git clone -b dev --single-branch https://github.com/Nexters/what-do-you-say-server.git
  ```

- `feature/issue-이슈 번호` 브랜치가 `dev` 브랜치에 머지 되면, 반드시 삭제해야 한다.

- Github Action에서 CI/CD 를 통과해야 Merge 할 수 있다.

<br>

## :airplane: CI / CD

- github actions를 활용해서 지속적 통합 및 배포
- `feature` 브랜치에서 `dev`로 Pull Request를 보내면, CI가 동작된다.
- `dev`에서 `master`로 Pull Request를 보내면, CI가 동작되고 Merge가 되면, 운영 리소스에 배포된다.

<br>

## :green_book: How to run test code locally

```zsh
# mysql container 실행
$ docker-compose -f docker-compose.mysql.yml up -d

# lint 체크 하고, type-check 후, 테스트 코드 실행하는 스크립트
$ npm run test # or npm test
```

<br>

## :blue_book: How to run the server locally

1. ts-node를 사용해서 실행하는 경우

```zsh
$ npm install

$ cp .env.sample ./.env

# mysql container 실행
$ docker-compose -f docker-compose.mysql.yml up -d

# lint
$ npm run lint

# type-check
$ npm run type-check

# local에서 Server 실행
$ npm start
```

2. babel을 사용해서 빌드 후, 실행하는 경우

```zsh
$ npm install

$ cp .env.sample ./.env

# mysql container 실행
$ docker-compose -f docker-compose.mysql.yml up -d

# babel을 사용하여 js파일로 변환
$ npm run build

# dist에 있는 js파일 실행
$ npm run prod
```

3. docker를 사용해서 실행하는 경우

   > .env 파일에 DB Host가 `host.docker.internal`로 되어 있어야 합니다.

```zsh
# what-do-you-say-server 이미지를 생성한다.
$ docker build -t what-do-you-say-server .

# 이미지를 기반으로 컨테이너를 실행한다.
$ docker-compose up # 또는 docker-compose -f docker-compose.yml up
```

<br>

## :open_file_folder: Project Structure

```markdown
src
├── common
│   ├── config
│   ├── types
│   └── utils
├── controller
├── entity
├── infrastructure
│   ├── express
│   └── typeorm
├── repository
└── service
```
