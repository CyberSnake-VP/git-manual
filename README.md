# Мини-гайд по основным коммандам Git  

![Конец](https://www.simplilearn.com/ice9/free_resources_article_thumb/git_vs_github2.jpg)

### Создаем папку с репозиторием Git

Скачиваем и устанавливаем Git на компьютере и настраиваем файл конфигурации:  

```bash
git config --global user.name "ваше_имя"
git config --global user.email "электронная почта"

```
---
Создаем папку в компьютере в которой хотим создать репозиторий Git и заходим в нее через терминал, например:  

```terminal
  cd ./folder-git-repository

```
---
Cоздаем репозиторий Git:  

```bash
git init

```
---
Теперь наша папка стала репозиторием, Git будет отслеживать все изменение происходящие в ней.  
<mark>Репозиторий можно удалить!</mark>  
Удалив подкаталог:  

```bash
rm -rf .git

```

### Создание первого коммита

Теперь файлы и папки в локальном репозитории можно будет отправить в GitHub, для этого их нужно подготовить:  
Проверим состояние репозитория, если ли файлы, которые выделены красным:  

```bash
git status

```
Если мы сейчас создадим в каталоге с репозиторием файлы test.txt и test2.txt</br> 
то они отобразятся красным с состоянием create(созданы).</br>
Подготовим эти файлы:  

```bash
git add --all (ключом -all мы добавляем сразу все что есть)
git add _имя-файла_ (а тут избирательно)
git add . (а так же можно добавить всю текущую папку bash)

```
---
Файлы подготовлены, теперь можно их зафиксировать, закоммитить:  

```bash
git commit -m 'Краткая информация к коммиту'

```
---
Просмотр состояния коммитов:  

```bash
git log

```
### Создание SSH ключей и привязка их к GitHub

Чтобы отправлять в удаленный репозиторий файлы с локального, можно использовать SSH:<br>
и не вводить пароль каждый раз.  

Проверка наличия ключей:  

```bash
ls -la .ssh 

```
---
Если есть файлы типа: `id_ed25519.pub` тогда нужно их удалить:  

```bash
rm id_ed25519.pub

```
---
Создаем ключи:  

```bash
ssh-keygen -t ed25519 -C емаил_почта

```
---
Теперь можно скопировать <mark>публичный ключ!</mark> в буффер обмена инструкция bash для linux:   

```bash 
xclip -sel clip -i файл_ключей.pub 

```
---
После чего, в GitHub нужно в настройках аккаунта установить новый публичный ssh ключ и вставить из буфера его содержимое  

Проверяем состояние ключа:  
```bash
ssh -T git@github.com

```
---
Cвязываем наш локальный репозиторий с GitHub:  
```bash
git remote add origin git@github.com:логин_гитхаб/Название_созданного репозитория в GitHub.git

```
---
Проверяем, что репозиторий был связан:  
```bash
git remote -v

```
---

### Отправляем данные в GitHub

Отправляем данные:  
```bash
git branch -m main   (Даем название главной ветки)
git push -u origin main  (Делаем первый push с ключами и названием ветки)

```
В последующем будет использоваться сокращенная версия push:  
```bash
git push

```

### Клонирование репозитория

Удаленный репозиторий, любой, к которому имеется доступ, можно склонировать себе на компьютер.  
Имеенно склонировать а не скопировать, потому что будет происходить создание папки-репозитория с содержимым,  
после чего мы можем работать с данными как c нашим собственным репозиторием,изменять файлы, пушить их обратно. 
Причем короткой коммандой git push, ведь все зависимости будет скопированый, т.е. указание главное ветки и т.д.

Клоннирование репозитория c GitHub:  
```bash
git clone git@github.com:Giant-VP/git-basics.git

```
---

Если прав доступа к клонированию и редактированию нет, можно выполнить <mark>Fork</mark>, по-сути происходит коппирования  
в GitHub к собственным репозиториям, после чего его можно склоннировать к себе и работать с данными.  
Например развивать проект самостоятельно или отправить автору свои предложения и он уже внесет их в свой проект.

### Хэш - идентификатор коммита
![Hash](https://pictures.s3.yandex.net/resources/M2_T5_04-3_1705507764.png)

С помощью алгоритма SHA-1 для каждого коммита свой уникальный хеш.
результат хеширования в Git — символьная строка. Она относительно коротка (
40 символов в случае SHA-1) и состоит из цифр 0—9 и латинских букв A—F (неважно, заглавных или строчных).
Хеш обладает следующими важными свойствами:

* если хеш получить дважды для одного и того же набора входных данных,то 
результат будет гарантированно одинаковый;
* если хоть что-то в исходных данных поменяется (хотя бы один символ), то
хеш тоже изменится (причём сильно).

Все хеши и таблицу `хеш → информация о коммите` Git сохраняет в служебные файлы. Они находятся в скрытой папке `.git` в репозитории проекта.

### Лог
![GIT_LOG](https://pictures.s3.yandex.net/resources/M2_T5_02_1705508495.png)
### **`git log`**	   
Вот из каких элементов состоит описание:
1. > Строка из цифр и латинских букв после слова commit — это уже знакомый вам хеш коммита.
2. > **Author** — имя автора и его электронная почта.
3. > **Date** — дата и время создания коммита.
4. > Сообщение к коммиту.   

Сокращённый лог вызывают командой `git log` с флагом `--oneline`
![GIT_LOG](https://pictures.s3.yandex.net/resources/M2_T5_03_1705508703.png)

### HEAD

Файл `HEAD` (англ. «голова», «головной») — один из служебных файлов папки `.git.`
Он указывает на коммит, который сделан последним (то есть на самый новый).

Внутри `HEAD` — ссылка на служебный файл: `refs/heads/master` (или refs/heads/main в зависимости от названия ветки). 
Если заглянуть в этот файл, можно увидеть хеш последнего коммита.

Если нужно передать последний коммит, то вместо его хеша можно просто написать слово `HEAD` — Git поймёт, что 
это последний коммит.

### Git Status

Схема `MERMAID` для отображения возможных состояний файлов:

```mermaid
graph LR
  untracked -- "git add" --> staged;
  staged    -- "git commit"     --> tracked;
  tracked -- "Изменения" --> modified;
  modified -- "git add" --> staged;
  staged -- "Изменения" --> modified;
```
### Оформление сообщений к коммитам

#### Стили оформления
**Обычный**<br>
```bash
git commit -m "Изменить цвет кнопки выход на панеле задач"

```
**Корпоротивный**<br>   	
Во многих компаниях применяется Jira — система для организации проектов и задач. 
У каждой задачи в Jira есть идентификатор из нескольких заглавных латинских букв и номера. 
Например, `LGS-239` значит, что это 239-я задача в проекте **LGS** (сокращение от англ. logistics — «логистика»).
В корпоративном стиле в начале сообщения обычно указывают Jira-ID, а после — текст сообщения.
     
```bash
git commit -m "LGS-239: Дополнить список пасхалок новыми числами" 

```

**Conventional Commits**    
предлагает такой формат коммита: \<type>: <сообщение>. Первая часть type — это тип изменений.<br> 

```bash
git commit -m "feat: добавить подсчёт суммы заказов за неделю" 

```

GitHub-стиль
GitHub можно использовать не только для хранения файлов проекта, но и для ведения списка задач (англ. issue) этого проекта.
Если коммит «закрывает» или «решает» какую-то задачу, то в его сообщении удобно указывать ссылку на неё.  
Для этого в любом месте сообщения нужно указать #<номер задачи>.<br>    
Например, вот так.<br>

```bash
$ git commit -m "Исправить #334, добавить график температуры" 

```

![Конец](https://i.scdn.co/image/ab67616d0000b273f5566b1c4a3892ec6844af7c)































