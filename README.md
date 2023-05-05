

### Задание 1

![](ссылка на скриншот 1)`


---

### Задание 2-3

Чтобы билд запускался не дожидаясь теста, в билде указал
  dependencies: []

Тест запускается только при изменении файлов *.go
  only:
   changes:
     - '*.go'

```
stages:
  - test
  - build
  - analysis

test:
  stage: test
  image: golang:1.17
  script: 
   - go test .
  only:
   changes:
     - '*.go'
     
analysis:
  stage: test
  image:
    name: sonarsource/sonar-scanner-cli
    entrypoint: [""]
  variables:
  script:
  - sonar-scanner -Dsonar.projectKey=gitlab -Dsonar.sources=. -Dsonar.host.url=http://gitlab.localdomain:9000 -Dsonar.login=sqa_4508113f8a900343ddc6fa99d02dc81282d4bd05
 

build:
  stage: build
  image: golang:1.17
  script:
   - go build -a -installsuffix nocgo -o goapp .
  dependencies: []
```

![](ссылка на скриншот 2)`
