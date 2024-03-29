# Подготовка

Для выполнения данной ЛР я использовал машину созданную в предыдущей работе. 
Далее, в новой машине прописываем команды `git clone <URL-репозитория>` и `sudo apt-get install git-flow` (на будущее).

# Введение

Создадим файл example.txt и запишем туда _какой-нибудь текст_ и с помощью команд:

```
git add example.txt
git commit -m "File added example.txt"
git push origin main
```

запушим его. 

Далее перейдём к работе с ветками. С помощью команд 

```
git branch feature-branch
git checkout feature-branch
```

создадим веткуfeature-branch и переключемся на неё. Теперь дополним example.txt и повторно введём вышеуказаные команды(но меняем имя комита на `"New file added example.txt"`). Таким образом пушим example.txt на текущую ветку и получаем следущее:

![image](https://github.com/Nirolok/-_5/assets/40453222/a9772817-9683-4f82-9444-ada0ed3e4758)


После данной операции, с помощью команды `git checkout main` возвращаемся к  основной ветке и с помощью команд `git merge feature-branch` и `git push origin main` сливаем изменения из ветки feature-branch в main. Так у нас получаются две ветки и изменения в обоих ветках.

# Работа с ветками

Создаём README.md файл, в котором создаём базовую структуру книги и комитим его в main

![image](https://github.com/Nirolok/-_5/assets/40453222/47686ce7-a00a-4c5e-a652-0d41a546ae41)


Далее создаём и переходим в ветку feature-login, с помощью команды `git checkout -b feature-login`.
В README вносим изменения (добавляем третью главу) и комитим его на feature-login.

![image](https://github.com/Nirolok/-_5/assets/40453222/b5a36925-71e4-4494-a2c6-dd2207779485)


# Работа с удалённым репозиторием

Возвращаемся на ветку main, вносим в файл изменения и соответсвенно комитим

![image](https://github.com/Nirolok/-_5/assets/40453222/e00b2611-b223-46a6-9faf-966b3b6fdb11)


# Моделирование конфликта

Переходим на ветку feature-login, изменяем файл и комитим 

![image](https://github.com/Nirolok/-_5/assets/40453222/cc7b5777-f733-48c8-b134-70836887775e)


# Разрешение конфликта

С помощью команд

```
git checkout main
git pull origin main
```
прыгаем на ветку main и пытаемся слить изменения, но ловим конфликт

![Снимок экрана 2024-01-22 234009](https://github.com/Nirolok/-_5/assets/40453222/72ff7485-21f2-4223-95b8-8f1e1dd76616)


Переходим в файл и удаляем всё лишнее

![Снимок экрана 2024-01-22 234140](https://github.com/Nirolok/-_5/assets/40453222/c4a867aa-450f-4718-8477-58d81e781c7c)

![Снимок экрана 2024-01-22 234223](https://github.com/Nirolok/-_5/assets/40453222/167cd50b-7fc3-44b8-a6c1-d90045238a92)


Комитим решение конфликта 

![image](https://github.com/Nirolok/-_5/assets/40453222/d903d0fe-e1c1-4c3b-8461-9fe12aa085a9)


# Автоматизация проверки файлов при коммите

Переходим в .git/hooks (предварительно ставим галочку на "показывать скрытые файлы") и создаём там файл с названием pre-commit(ему необходимо дать право на выполнение).

В данном файле мы напишем скрипт, который будет проверять файлы на наличие "ключа" (ну или просто наличия "===" в файле).
Что делает скрипт:
Проверяет файл на наличие "===". В случае если "ключ" не найден выводим " okay", иначе выводим "not okay" и завершаем скрипт с кодом 1. Данный скрипт применяется ко всем переданным файлам, и если все проходят проверку выводи "All okay", завершаем скрипт с кодом 0.

![image](https://github.com/Nirolok/-_5/assets/40453222/86d60266-3d43-49ee-9f5a-8f38ce98b8a5)

(not okay)

![Снимок экрана 2024-01-23 010522](https://github.com/Nirolok/-_5/assets/40453222/fb27bca3-d1bf-48bd-ba3a-868e76d5808f)


![Снимок экрана 2024-01-23 010406](https://github.com/Nirolok/-_5/assets/40453222/2ac9dcb6-e627-4489-8d70-db5110cedcf4)

(Okay)
(All okay)

![Снимок экрана 2024-01-23 010604](https://github.com/Nirolok/-_5/assets/40453222/8abbeb0b-bbc9-445a-aedd-296684f67712)

![Снимок экрана 2024-01-23 010954](https://github.com/Nirolok/-_5/assets/40453222/6c8ec14e-753c-480b-9f7d-98a24f1c7e94)





# Использование Git Flow в проекте 

Перед тем как начать работать с git flow необхлдимо ~~трижды перекриститься~~~ установить git flow на локальную машину, что мы сделали ещё в самом начале.

Для нормальной работы git flow нам нужно создать ветку develop (по аналогии с предыдущими), после чего можно инициализировать git flow с помощью команды `git flow init`.

(В случае успешной инициализации увидим вот это)

![image](https://github.com/Nirolok/-_5/assets/40453222/8f6f1f69-3aae-49d5-80c4-3e6cf23adbdc)


Затем, командой `git flow feature start task-management` фетку новой функциональности. В ней создаём файл task_manager.py, в который вставляем код

~~~
def create_task(title, description):
    # Логика создания задачи
    print(f"Создана новая задача: {title}")
~~~

И соответсвенно комитим файл

~~~
git add task_manager.py
git commit -m "Добавлен функционал управления задачами"
~~~

После этого завершаем "фичу" и  объеденяем с основной веткой, с помощью команды `git flow feature finish task-management`.
После этого мы должны автоматически оказаться в ветке develop (что и происходит). Вводим следующие команды 

~~~
git checkout develop
git flow release start v1.0.0
~~~

и начинаем создание релиза.
Создаём файл version.txt и обновляем версию в нём, изпользуя следующие команды 

~~~
echo "v1.0.0" > version.txt
git add version.txt
git commit -m "Обновлена версия для релиза v1.0.0"
~~~

После этого можно завершить релиз командой `git flow release finish v1.0.0` и объкдкняем его с основной веткой.

![image](https://github.com/Nirolok/-_5/assets/40453222/b81dff8c-b77e-4c3c-8086-f65d63f42102)


Создадим хотфикс

~~~
git flow hotfix start hotfix-1.0.1
~~~


Внесём изменения и коммитим

~~~
git add file_with_error.py
git commit -m "Исправлена критическая ошибка"
~~~

Соответсвенно завершаем работу hotfix-1.0.1 и объеденяем с основной веткой

~~~
git flow hotfix finish hotfix-1.0.1
~~~

![image](https://github.com/Nirolok/-_5/assets/40453222/8b0d5528-454e-4ac3-a7eb-f339a8cb1a59)

В конце завершаем работы и отравляем изменения на наш репозиторий.

![image](https://github.com/Nirolok/-_5/assets/40453222/3d4220e6-6db1-47c0-b51a-3c71aed91ede)


~~~
git push origin develop
git push origin main
~~~
