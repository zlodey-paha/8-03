# Домашнее задание к занятию «GitLab»

---

### Задание 1

**Что нужно сделать:**

1. Разверните GitLab локально, используя Vagrantfile и инструкцию, описанные в [этом репозитории](https://github.com/netology-code/sdvps-materials/tree/main/gitlab).   
2. Создайте новый проект и пустой репозиторий в нём.
3. Зарегистрируйте gitlab-runner для этого проекта и запустите его в режиме Docker. Раннер можно регистрировать и запускать на той же виртуальной машине, на которой запущен GitLab.

В качестве ответа в репозиторий шаблона с решением добавьте скриншоты с настройками раннера в проекте.

### Решение 1

![Runner](https://github.com/zlodey-paha/8-03/blob/main/8-03/1.1.%20Runner.png)
![CI/CD Runners](https://github.com/zlodey-paha/8-03/blob/main/8-03/1.2.%20Runners.png)
![Jobs](https://github.com/zlodey-paha/8-03/blob/main/8-03/1.3.%20Jobs.png)
![.gitlab-ci.yml screen](https://github.com/zlodey-paha/8-03/blob/main/8-03/1.4.%20gitlag-ci.yml.png)
```
stages:
  - test
  - build

test-job:
  stage: test
  tags:
    - docker
  script:
    - echo "Hello gitlab!"
    - echo "Hello runner!"

build-job:
  stage: build
  tags:
    - docker
  script:
    - echo "building project"
```

---

### Задание 2

**Что нужно сделать:**

1. Запушьте [репозиторий](https://github.com/netology-code/sdvps-materials/tree/main/gitlab) на GitLab, изменив origin. Это изучалось на занятии по Git.
2. Создайте .gitlab-ci.yml, описав в нём все необходимые, на ваш взгляд, этапы.

В качестве ответа в шаблон с решением добавьте: 
   
 * файл gitlab-ci.yml для своего проекта или вставьте код в соответствующее поле в шаблоне; 
 * скриншоты с успешно собранными сборками.

### Решение 2

![Project](https://github.com/zlodey-paha/8-03/blob/main/8-03/2.1.%20Project.png)
![Piplines](https://github.com/zlodey-paha/8-03/blob/main/8-03/2.3.%20Piplines.png)
![.gitlab-ci.yml](https://github.com/zlodey-paha/8-03/blob/main/8-03/2.2.%20gitlab-ci.yml)
```
stages:
  - validate
  - test
  - build
  - deploy

validate-code:
  stage: validate
  tags:
    - docker
  image: alpine:latest
  script:
    - echo "Check file"
    - echo "OK"

run-tests:
  stage: test
  tags:
    - docker
  image: node:16-alpine
  script:
    - echo "Running test"
    - echo "Test OK"

build-app:
  stage: build
  tags:
    - docker
  image: node:16-alpine
  script:
    - echo "building"
    - echo "building complete"
  artifacts:
    paths:
      - build/

deploy-app:
  stage: deploy
  tags:
    - docker
  image: alpine:latest
  script:
    - echo "deploy-app"
    - echo "deploy OK"
  when: manual
```
 
---
## Дополнительные задания* (со звёздочкой)

Их выполнение необязательное и не влияет на получение зачёта по домашнему заданию. Можете их решить, если хотите лучше разобраться в материале.

---

### Задание 3*

Измените CI так, чтобы:

 - этап сборки запускался сразу, не дожидаясь результатов тестов;
 - тесты запускались только при изменении файлов с расширением *.go.

В качестве ответа добавьте в шаблон с решением файл gitlab-ci.yml своего проекта или вставьте код в соответсвующее поле в шаблоне.
