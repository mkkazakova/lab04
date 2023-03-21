# lab04

## Подготовка

```
$ sudo apt install git
```

Устанвливаем имя пользователя и email

```
$ git config --global user.name "Masha"
$ git config --global user.email "mkkazakova@yandex.ru"
```

В гитхабе создаем свой токен

Создаём репозиторий lab04

Клонируем 3 лабу в 4. И заходим в папку lab-04

```
$ git clone https://github.com/mkkazakova/lab03 lab-04
$ cd lab-04
$ git remote remove origin
$ git remote add origin https://github.com/mkkazakova/lab04.git
```

> команда git clone делает git init + git pull. Т.е. делает копию другого репозитория
> git init применяться для того, что бы создать пустой репозиторий, а git pull - его наполнить с другого репозитория.

> git remote remove origin удаляет подключение к удаленному репозиторию

> git remote add используется для создания записи о новом подключении к удаленному репозиторию


Создаём папку .github в lab-04 и заходим туда. Создаём папку workflows в .github и заходим туда.

```
$ mkdir .github
$ cd .github
$ mkdir workflows
$ cd workflows
```

В папке "~/lab-04/.github/workflows" создадим файл Linux.yml. Затем редактируем его.

.yml — расширение файла в формате YAML

```
$ cat >> Linux.yml << EOF
$ nano Linux.yml
```

Содержимое файла Linux.yml:

```
name: CMake
# Имя процесса

on:
 push:
  branches: [master]
 pull_request:
  branches: [master]
# В данном случае процесс запустится при push и pull-request в ветку master

jobs: 
# Список задач

 build_Linux:
 # Название задачи
	
  runs-on: ubuntu-latest
  # Система, на которой будет запущена задача
  # В данном случае это будет последняя версия Ubuntu

  steps:
  # Шаги задачи

  - uses: actions/checkout@v3
    # Извлекает репозиторий в $GITHUB_WORKSPACE, чтобы рабочий процесс мог получить к нему доступ.

  - name: Configure Solver
    # Имя шага (настройка Solver)
    run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build

  - name: Build Solver
    run: cmake --build ${{github.workspace}}/solver_application/build
    # Запускаем Solver

  - name: Configure HelloWorld
    # Имя шага (настройка HelloWorld)
    run: cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build

  - name: Build HelloWorld
    run: cmake --build ${{github.workspace}}/hello_world_application/build
    # Запускаем HelloWorld
```

Пушим коммитим изменения

```
$ git add Linux.yml
$ git commit -m "Linux.yml"
$ git push origin master
```

Далее требуется ввести логин (своё имя на GitHub), затем пароль (свой токен)

## Вторая часть

В папке "~/lab-04/.github/workflows" создадим файл Windows.yml. Затем редактируем его.

```
$ cat >> Windows.yml << EOF
$ nano Windows.yml
```

Содержимое файла Windows.yml:

```
name: CMake
# Имя процесса

on:
 push:
  branches: [master]
 pull_request:
  branches: [master]

jobs: 
# Список задач

 build_Windows:
 # Название задачи

  runs-on: windows-latest
  # Система, на которой будет запущена задача
  # В данном случае это будет последняя версия Windows

  steps:
  - uses: actions/checkout@v3

  - name: Configure Solver
    # Имя шага (настройка Solver)
    run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build

  - name: Build Solver
    run: cmake --build ${{github.workspace}}/solver_application/build
    # Запускаем Solver

  - name: Configure HelloWorld
    # Имя шага (настройка HelloWorld)
    run: cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build

  - name: Build HelloWorld
    run: cmake --build ${{github.workspace}}/hello_world_application/build
    # Запускаем HelloWorld
```

Пушим коммитим изменения

```
$ git add Windows.yml
$ git commit -m "Windows.yml"
$ git push origin master
```

Далее требуется ввести логин (своё имя на GitHub), затем пароль (свой токен)


## Скрины

![image](https://user-images.githubusercontent.com/125077130/226405331-1ad0eecb-fc2e-4867-9ff2-7ef6687c8fed.png)

![image](https://user-images.githubusercontent.com/125077130/226405408-a04ec934-2cd0-41ae-bed8-09fad0887fae.png)

![image](https://user-images.githubusercontent.com/125077130/226405466-62725550-fc5f-4622-bf22-6308ee3dac00.png)

