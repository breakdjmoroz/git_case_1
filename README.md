# __Что такое Git и с чем его едят?__
---
## Системы контроля версий<br>
Дорогой друг!  
Первое, с чего мы начнём - это с понятия *системы контроля версий*.  
Система контроля версий - это программка, позволяющая нам хранить,  редактировать, откатываться, работать совместно над разными версиями файлов.<br>
Одна из таких программ называется Git. Она самая популярная среди других, поэтому её знание так востребованно.<br>


## Понятия Git<br>
Git ~~как и другие системы контроля версий~~ оперирует такими понятиями:  
1. Инициализация
2. Коммит
3. Ветка
4. Репозиторий (локальный/удалённый)<br>

Пройдёмся по каждому из них...<br>

### _Инициализация_<br>
Инициализация - это первая _развёртка_ Git-а для нашего файла или целого проекта.  
Эта операция необходима для первичной настройки нашей системы контроля версий.<br>
### _Коммит_  
Коммит - это "_снимок_" нашего файла/проекта в тот момент времени, когда мы решили его зафиксировать.  
По-сути, коммит работает как сохранение в игре.<br>
### _Ветка_  
Если коммит - это "_снимок_", то ветка - целая "_кинолента_", то есть несколько "_снимков_", расположенных в определённом порядке на временной шкале.  
Однако веток может быть сколько угодно много, поэтому в вашем "_кино_" возможны альтернативные Вселенные =)<br>
### _Репозиторий_  
Репозиторием называют директорию, хранящую изменения. Де-факто - это ваша рабочая папка, где вы вольны творить всё, что захотите!  
Git создаёт такой репозиторий на вашем компьютере, однако если вы хотите делиться изменениями с друзьями, то вы можете инициализировать удалённый репозиторий на таких платформах как [GitHub](https://github.com/ "Самая популярная платформа для создания удалённых репозиториев!") и [GitLab](https://gitlab.com/ "Не менее популярная git-платформа.").<br>

## Работа с Git<br>
Теперь, когда мы разобрались с основными понятиями, можно приступать к работе.  

Подробная [инструкция по установке](https://git-scm.com/book/ru/v2/%D0%92%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5-%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0-Gitl) Git поможет вам обзавестись этой программой под управлением любой из ОС (Windows, Linux, OSX).

Я же буду демонстрировать работу из-под Linux.  

Для начала настроим основные параметры:
```bash
git config --global user.name #ваше_имя#
git config --global user.email #ваша_электронная_почта#
```

Теперь создадим директорию, в которой будем сохранять наши файлы:<br>
```bash
mkdir first_git_repo
cd first_git_repo
```   

Далее воспользуемся командой
```bash
git init
```
для того чтобы инициализировать наш локальный репозиторий.<br>

Давайте создадим файл, версии которого мы хотим отслеживать!
```bash
touch some_file.txt
```  

Необходимо сказать Git-у, что мы хотим отслеживать изменения этого файла:  
```bash
git add some_file.txt
```   

Командой
```bash
git status
```
мы можем получить информацию о том, какие файлы мы отслеживаем в данный момент.  
Файл some_file.txt должен быть подсвечен зелёным цветом.  

Пришло время зафиксировать наши изменения (создание файла "some_file.txt"). Создадим наш первый коммит!  
```bash
git commit -m "Здесь оставляем свой комментарий к коммиту"
```  

Чтобы проверить, что коммит создался, введём команду
```bash
git log
```
для отслеживания истории коммитов.  

Поздравляю! Вы сделали свой первый шаг в ознакомлении с системой Git!!!

## Взаимодействие с удалённым репозиторием<br>
Одна из основных идей Git-а заключается в возможности редактировать файл совместно, при этом избегая конфликтов в версиях.  
Чтобы реализовать эту возможность нужно зарегистрироваться на одной из популярных платформ, например на [GitHub](https://github.com).

После успешной регистрации нам нужно обеспечить безопасность нашего удалённого репозитория.  
Для этих целей сгенерируем SSH-ключ:
```bash
ssh-keygen -t ed25519
```  
В домашней директории создастся каталог **~/.ssh** и в нём будут лежать два файла.  
Копируем содержимое файла с расширением **.pub** (_ни в коем случае не делитесь файлом без расширения!_).  

Затем переходим на страничку вашей платформы (я продолжу использовать GitHub) и в настройках находим опции SSH-ключей (для GitHub нажмите на иконку в правом верхнем углу, найдите пункт "Settings" в выпавшем меню, выберете "SSH and GPG keys").  

Создаём новый SSH-ключ нажатием на соответствующую кнопку и в поле "Key" вставляем скопированный заранее ключ.  

Готово!

Для того чтобы привязать локальный репозиторий к удалённому выполним:
```bash
git remote add origin #ссылка на репозиторий в ФОРМАТЕ SSH#
```  

Синхронизируем изменения с помощью команды:
```bash
git push -u origin main
```

В дальнейшем используем просто
```bash
git push
```

Теперь можете проверить наличие some_file.txt в вашем удалённом репозитории!

## Разбираемся в истории коммитов  
У каждого коммита есть набор информации, описывающей его:

- Автор коммита
- Дата создания
- Сообщение коммита

и др.

### Понятие хэша

Главным идентификатором коммита является строка из 40-ка символов (символ здесь - цифра от 0 до 9 или буквы латинского алфавита от a до f). Такая строка уникальна для каждого коммита и генерируется специальным алгоритмом на основе той самой информации, о которой мы говорили выше.  
Такая строка называется _хэшем_. Последовательность в хэше всегда одинаковая для одних и тех же данных (при использовании одного алгоритма хеширования), но абсолютно разная для данных, отличающихся хоть сколько-нибудь немного.<br>

### Указатель HEAD

Все операции, которые Git проводит с коммитами требуют хэш того коммита, над которым будет производится действие.  
В каталоге **.git** существует файл ``HEAD``, который содержит ссылку на файл, в котором хранится хэш самого последнего коммита. Таким образом, вы можете использовать _указатель_ `HEAD` в командах Git вместо хэша.

```mermaid
graph LR;
  HEAD-->file["refs/heads/main"];
  file["refs/heads/main"]-->hash["Хэш последнего коммита"];
```

### Ещё немного о `git log`

Для простоты вывода информации об истории коммитов на экран с помощью `git log` можно (и нужно!) использовать флаг `--oneline`:
```bash
git log --oneline
```  
Вывод будет содержать сокращённые хэши коммитов (Git сам обрезает хэш так, чтобы выведено было достаточное количество символов для однозначной идентификации коммита) и сообщение к каждому из них.

## Статусы файлов

Git устанавливает четыре статуса для файлов:

- untracked
- tracked
- staged
- modified

Проясним каждое состояние...<br>

### Untracked
Git увидел этот файл, но не отслеживает его изменения.

### Tracked
Отслеживаемый Git-ом файл.

### Staged
Такой статус означает, что файл готов к тому, чтобы войти в следующий коммит.

### Modified
Файл изменён. Это значит, что в следующий коммит он не будет включён.

Состояниями выше мы можем управлять используя `git add` или изменяя файлы.  
Сложность такой системы заключается в возможности нахождения одного и того же файла (но не его версий!) в разных состояниях.  

Пример возможных состояний можно увидеть здесь:

```mermaid
graph LR;
  untracked -- "git add" --> staged;
  modified -- "git add" --> staged;
  staged -- "Изменения в файле" --> modified;
  staged -- "git commit" --> tracked;
  tracked -- "Изменения в файле" --> modified;
```

## Рекомендации к оформлению коммитов
Цель сообщений к коммитам - сделать навигацию проще.  

Есть несколько способов достичь мастерства в написании сообщений к коммитам, но мы бы хотели остановиться на общих рекомендациях. Подробные техники описания коммитов можно найти [здесь](https://www.conventionalcommits.org/ru/v1.0.0/ "Одно из множества соглашений о написании сообщений к коммитам.").

Вот наши маленькие советы:

- Пишите ёмкие сообщения (`git log --oneline` показывает до 72 символов сообщения)
- Говорите по делу ("Исправлена ошибка в описании файла some_file.txt.", вместо "Исправлена ошибка.")
- Следуйте принятым в вашей компании правилам (Писать сообщения в повелительном наклонении, например)
