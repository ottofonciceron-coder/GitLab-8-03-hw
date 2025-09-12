# Занятие: Развертывание "GitLab 8-03" - Марчук Кирилл

### Задание 1 Разверните GitLab 
 

1.  `Развернул GitLab CE на VM:** [http://158.160.199.220](http://158.160.199.220)`
2. `Создал тестовый проект `my-first-project`
3.  `Зарегистрировал gitlab-runner для этого проекта и запустил его в режиме Docker`

1.   --url `http://158.160.199.220/`
2.   --description `my-docker-runner`
3.   --tag-list `docker`
4.   --executor 'docker'
5.   --docker-image 'alpine:latest'

![Развернули gitlab]https://drive.google.com/file/d/13exMLJJZooNh8xcUYlzPy7UmsPa4L8wZ/view?usp=sharing
![Создали Проект]https://drive.google.com/file/d/1VcCH5gfhp-XjdepNZFtcdDn5R5WskZUE/view?usp=sharing
![Зарегистрировал gitlab-runner]https://drive.google.com/file/d/1wIjv-8XOXNz1BezbI3G5GXWnGG3gb4Fw/view?usp=sharing

---

### Задание 2 Запуск Runner

`Пушим Репозиторий на GitLab.`

1. `Создаём файл .gitlab-ci.yml`
2.  `Пушим репозиторий на gitlab,git push -u origin master`
3. `Проверяем логи Пайплайн и сам Runner`


```
Поле для вставки кода...
```yaml
stages:
  - test
  - build

test-job:
  stage: test
  image: alpine:latest
  tags:
    - docker
  script:
    - echo "Hello from GitLab Runner!"
    - uname -a

build-job:
  stage: build
  image: alpine:latest
  tags:
    - docker
  script:
    - echo "Building project..."
    - echo "Build completed!"
```


![Проверка раннера]https://drive.google.com/file/d/11G5loSTxA3vf-0qQnu-X_HKRYTvaXN7-/view?usp=sharing
![ПРоверка]https://drive.google.com/file/d/1Zw3wow1RW8nJ2_GXe7s3-j46OXjEA2ML/view?usp=sharing
![Логи Job]https://drive.google.com/file/d/1JxAlH2Wud1KqXXkgcp6PugfzSNLipDNE/view?usp=sharing
![Логи Тестов]https://drive.google.com/file/d/1pXL0rMDYwrhsx7Yi_Kz7D7yWWzRM45_O/view?usp=sharing



