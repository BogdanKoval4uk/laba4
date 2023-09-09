# Лабораторная работа номер 4

##  Задание
1. Авторизоваться на сервисе Travis CI с использованием GitHub аккаунта
2. Создать публичный репозиторий с названием lab04 на сервисе GitHub
3. Ознакомиться со ссылками учебного материала
4. Включить интеграцию сервиса Travis CI с созданным репозиторием
5. Получить токен для Travis CLI с правами repo и user
6. Получить фрагмент вставки значка сервиса Travis CI в формате Markdown
7. Выполнить инструкцию учебного материала
8. Составить отчет и отправить ссылку личным сообщением в Slack

## Выполнение лабораторной работы
Вы продолжаете проходить стажировку в "Formatter Inc.".

В прошлый раз ваше задание заключалось в настройке автоматизированной системы CMake.

Сейчас вам требуется настроить систему непрерывной интеграции для библиотек и приложений, с которыми вы работали в прошлый раз. Настройте сборочные процедуры на различных платформах:

    используйте TravisCI для сборки на операционной системе Linux с использованием компиляторов gcc и clang;
    используйте AppVeyor для сборки на операционной системе Windows.
    используйте GitHub Actions и для того, и для того)

    
Клонируем репозиторий третьей лабы:
    $ git clone <ссылка на репу третьей лабы>
    $ cd <имя репы третьей лабы>
    $ git remote remove origin
    $ git remote add origin <ссылка на репу четвёртой лабы>

Создаём директорию .github/workflows в директории лабы

В ней создаём файл CI.yml:
name: CMake

    on:
     push:
     branches: [main]
     pull_request:
      branches: [main]

    jobs: 
     build_Linux:

      runs-on: ubuntu-latest

      steps:
      - uses: actions/checkout@v3

      - name: Configure Solver
      run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build

      - name: Build Solver
      run: cmake --build ${{github.workspace}}/solver_application/build

      - name: Configure HelloWorld
      run: cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build

      - name: Build HelloWorld
        run: cmake --build ${{github.workspace}}/hello_world_application/build

     build_Windows:

      runs-on: windows-latest

      steps:
      - uses: actions/checkout@v3

      - name: Configure Solver
        run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build

      - name: Build Solver
        run: cmake --build ${{github.workspace}}/solver_application/build

      - name: Configure HelloWorld
        run: cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build

      - name: Build HelloWorld
        run: cmake --build ${{github.workspace}}/hello_world_application/build
Добавляем файл в проект и пушим на гитхаб:
       $ git add .github
       $ git commit -m "added CI.yml"
       $ git push origin main

Заходим на гитхаб, во вкладку Actions, и проверяем, что процесс выполнен успешно.





