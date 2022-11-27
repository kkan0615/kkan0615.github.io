---
title: Express JS + Typescript 로깅 시스템
author: Youngjin Kwak
date: 2022-11-27 12:21:00 +0800
categories: [expressjs, typescript, nodejs]
tags: [expressjs, typescript, nodejs]
image:
path: ../images/expressjs-logo.png
width: 800
height: 500
alt: express-logo.
---
---
# Overview
winston 라이브러리를 사용해서 로깅 시스템을 만들 것입니다. winston은 node js에서 사용 할 수 있는 logger 입니다. 기본적으로 많은 기능을 제공하기 때문에, winston은 많은 곳에서 사용 되고 있습니다.
이 포스팅은 3.8.2 버전을 사용 중에 있습니다.

# winston 설치
```
npm install winston
```

# Winston 설정
일단 Typescript 파일을 하나 만들어 줍니다. 이 포스팅의 경우 ```logger.ts```라는 이름을 사용했습니다.
일단 풀 코드를 보고 해당 내용에 대한 설명은 아래에 적어 두었습니다.
```typescript
import winston from 'winston'

const colors = {
  error: 'red',
  warn: 'yellow',
  info: 'green',
  http: 'magenta',
  debug: 'white',
}
winston.addColors(colors)

const level = () => {
  const env = process.env.NODE_ENV || 'development'
  const isDevelopment = env === 'development'
  return isDevelopment ? 'debug' : 'warn'
}

const format = winston.format.combine(
  winston.format.timestamp({ format: 'YYYY-MM-DD HH:mm:ss:ms' }),
  winston.format.colorize({ all: true }),
  winston.format.printf(
    (info) => `${info.timestamp} ${info.level}: ${info.message}`,
  ),
)

const transports = [
  new winston.transports.Console(),
  new winston.transports.File({
    filename: `logs/${new Date().toLocaleDateString('en-CA')}-error.log`,
    level: 'error',
  }),
  new winston.transports.File({ filename: `logs/${new Date().toLocaleDateString('en-CA')}.log` }),
]

const logger = winston.createLogger({
  level: level(),
  format,
  transports,
})

export default logger
```

## 로깅에 스타일을 넣는 작업
이 과정의 경우 필수 적인 과정은 아니지만 console 창에서 모든 로깅을 색깔 별로 그리고 폰트 나눌 수 있습니다.
[문서 참조](https://github.com/winstonjs/winston#using-custom-logging-levels)
```typescript
const exampleColors = {
  baz: 'italic yellow',
  foobar: 'bold red cyanBG'
}
```

## Level 작성
위 코드는 최소 로그 레벨을 설정하기 위해 만들었습니다. development 환경에서는 debug 까지 호출하며, production 환경에서는 warn 레벨까지 호출합니다.
```typescript
const level = () => {
  const env = process.env.NODE_ENV || 'development'
  const isDevelopment = env === 'development'
  return isDevelopment ? 'debug' : 'warn'
}
```
### Level 순서
```
{
  error: 0,
  warn: 1,
  info: 2,
  http: 3,
  verbose: 4,
  debug: 5,
  silly: 6
```

### Custom Level 사용
미리 정해진 Level 순서 말고 나만의 Level를 사용 할 수 도 있습니다.
```typescript
const myCustomLevels = {
  levels: {
    foo: 0,
    bar: 1,
    baz: 2,
    foobar: 3
  },
  colors: {
    foo: 'blue',
    bar: 'green',
    baz: 'yellow',
    foobar: 'red'
  }
};

// createLogger 함수에 관해서는 아래에 추후 자세히 다룰 것입니다.
const customLevelLogger = winston.createLogger({
  levels: myCustomLevels.levels
});
```

### format 설정
```format.combine()``` 함수를 사용하여 formatting 사용 할 수 있습니다. 이 포스팅에서 다루지 않는 많은 설정이 있습니다. 이는 참고해주세요 공식 문서를 참고해주세요.
[공식 문서](https://github.com/winstonjs/winston#formats)
```typescript
const format = winston.format.combine(...)
```
### timestamp 설정
```typescript
winston.format.timestamp({ format: 'YYYY-MM-DD HH:mm:ss:ms' })
```
### 컬러 사용 설정
```typescript
winston.format.colorize({ all: true })
```
### Print format 설정
```typescript
winston.format.printf(
  (info) => `${info.timestamp} ${info.level}: ${info.message}`,
),
```

## Transport 설정
```createLogger()```함수 내 argument option으로써 설정 할 수 있습니다.
```typescript
const logger = winston.createLogger({
  transports: [...]
})
```
### Console 사용
아래 코드는 console창에 log를 보이게 할 때 사용합니다.
```typescript
new winston.transports.Console()
```
### 파일 Export
아래 코드는 "logs" 라는 이름을 가진 폴더를 생성 혹은 읽고 현재 날짜를 통해서 log 파일을 생성합니다.
```typescript
new winston.transports.File({ filename: `logs/${new Date().toLocaleDateString('ko-kr')}.log` })
```
### Http
HTTP 통신에 관한 log 내용을 저장 할 수 있습니다.
```typescript
new winston.transports.Http()
```

### Option 설정
Log Level에 따라 logging 다르게 관리 할 수 있습니다.
```typescript
[
  // error 로그만
  new winston.transports.File({
    filename: `logs/${new Date().toLocaleDateString('ko-kr')}-error.log`,
    level: 'error',
  }),
  // 모든 로그
  new winston.transports.File({ filename: `logs/${new Date().toLocaleDateString('ko-kr')}.log` })
]
```
또한 Format 역시 변경 할 수 있습니다
```typescript
new winston.transports.File({
  filename: `logs/${new Date().toLocaleDateString('ko-kr')}-debug.log`,
  level: 'debug',
  format: winston.format.combine(
    winston.format.colorize(),
    winston.format.simple()
  )
})
```

## ```createLogger()``` 함수 사용해서 logger 인스턴스 생성
위ㅔ서 작성한 내용을 토대로 logger 인스턴스를 생성하고 이를 module화하여 프로젝트 내에서 사용 할 수 있게 export 해줍니다.
```typescript
const logger = winston.createLogger({
  level: level(),
  format,
  transports,
})

export default logger
```

# 테스팅
```typescript
const app: Express = express()

app.get('/logger', (req: Request, res: Response) => {
  logger.error('This is an error log')
  logger.warn('This is a warn log')
  logger.info('This is a info log')
  logger.http('This is a http log')
  logger.debug('This is a debug log')
  res.send('Logging test...')
})
```
logger 테스트용 API를 만들 어 줍니다. 그리고 해당 API 주소로 들어가게 되면 Console 창 및 logs 폴더가 생성되며 안에 log 파일이 있는 것을 확인해 볼 수 있습니다.

# Ref
- [공식 문서 README.md](https://github.com/winstonjs/winston)
- [Better logs for ExpressJS using winston and Morgan with Typescript](https://levelup.gitconnected.com/better-logs-for-expressjs-using-winston-and-morgan-with-typescript-1c31c1ab9342)

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
