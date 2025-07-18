[[Proect]]
Отлично! Вот все основные команды Git в одном блоке Markdown, готовом для копирования.

```markdown
# Основные команды Git

Git — это распределенная система контроля версий, предназначенная для отслеживания изменений в исходном коде во время разработки программного обеспечения. Она помогает командам разработчиков сотрудничать и вести историю изменений.

## 1. Начало работы с репозиторием

### `git init`
Инициализирует новый пустой Git-репозиторий в текущей директории. Создает скрытую папку `.git/`.
```bash
git init
```

### `git clone <URL>`
Клонирует (копирует) существующий удаленный репозиторий на ваш локальный компьютер.
```bash
git clone https://github.com/пользователь/репозиторий.git
```

## 2. Ежедневная работа с файлами

### `git status`
Показывает текущее состояние рабочего каталога и области индексации (staging area). Выводит информацию о новых, измененных и удаленных файлах.
```bash
git status
```

### `git add <файл>`
Добавляет изменения из рабочего каталога в область индексации (staging area). Это первый шаг перед коммитом.
```bash
git add index.html          # Добавить один файл
git add css/style.css       # Добавить файл из поддиректории
git add .                   # Добавить все изменения в текущей директории и поддиректориях
```

### `git commit -m "Сообщение"`
Сохраняет проиндексированные изменения в историю репозитория как новый коммит. Сообщение коммита (`-m`) должно быть кратким и информативным.
```bash
git commit -m "Добавлена начальная разметка HTML"
```
*   **Совет:** Используйте `git commit` без `-m`, чтобы открыть текстовый редактор для более подробного сообщения коммита.

### `git log`
Показывает историю коммитов. Каждый коммит отображается с его хэшем, автором, датой и сообщением.
```bash
git log                         # Полная история коммитов
git log --oneline               # Краткая история коммитов (одна строка на коммит)
git log --graph --oneline --all # Визуализация веток и коммитов в компактном виде
```

### `git diff`
Показывает различия между двумя состояниями:
*   **`git diff`**: Различия между рабочим каталогом и областью индексации (что еще не добавлено в индекс).
*   **`git diff --staged` (или `--cached`)**: Различия между областью индексации и последним коммитом (что будет включено в следующий коммит).
*   **`git diff <commit1> <commit2>`**: Различия между двумя конкретными коммитами.
```bash
git diff
git diff --staged
git diff HEAD~1 HEAD   # Различия между предпоследним и последним коммитом
```

## 3. Ветвление (Branches)

Ветвление позволяет вам работать над разными функциями или исправлениями независимо друг от друга.

### `git branch`
*   **`git branch`**: Выводит список всех локальных веток. Текущая ветка помечена звездочкой.
*   **`git branch <имя_ветки>`**: Создает новую ветку.
```bash
git branch              # Показать все ветки
git branch new-feature  # Создать новую ветку 'new-feature'
```

### `git checkout <имя_ветки>`
Переключает вас на указанную ветку.
```bash
git checkout new-feature    # Переключиться на ветку 'new-feature'
git checkout -b new-branch  # Создать новую ветку и сразу на нее переключиться
```
*   **Примечание:** В современных версиях Git предпочтительнее использовать `git switch` и `git restore` вместо `git checkout` для ясности.
    *   `git switch <имя_ветки>`: Для переключения веток.
    *   `git switch -c <имя_новой_ветки>`: Для создания и переключения.

### `git merge <имя_ветки>`
Объединяет историю указанной ветки с текущей веткой.
```bash
git checkout master     # Переключиться на ветку, в которую нужно объединить
git merge new-feature   # Объединить 'new-feature' в 'master'
```

### `git branch -d <имя_ветки>`
Удаляет указанную локальную ветку (только если она уже объединена).
```bash
git branch -d new-feature
```
*   **`git branch -D <имя_ветки>`**: Удалить ветку принудительно (даже если она не объединена).

## 4. Работа с удаленными репозиториями

### `git remote`
Управляет удаленными репозиториями.
*   **`git remote -v`**: Показывает список удаленных репозиториев и их URL.
*   **`git remote add <имя> <URL>`**: Добавляет новый удаленный репозиторий.
```bash
git remote -v
git remote add upstream https://github.com/оригинал/репозиторий.git
```

### `git push <удаленный> <ветка>`
Отправляет ваши локальные коммиты на удаленный репозиторий.
```bash
git push origin master          # Отправить изменения на ветку 'master' удаленного репозитория 'origin'
git push -u origin new-feature  # Отправить и установить 'new-feature' как отслеживаемую ветку (для удобства последующих push/pull)
```

### `git pull <удаленный> <ветка>`
Загружает изменения с удаленного репозитория и автоматически объединяет их с вашей текущей локальной веткой.
```bash
git pull origin master          # Загрузить и объединить изменения с 'master' из 'origin'
```

### `git fetch <удаленный> <ветка>`
Загружает изменения с удаленного репозитория, но **не объединяет** их с вашей текущей локальной веткой. Изменения сохраняются в виде новой удаленной ветки (например, `origin/master`). Это позволяет вам просмотреть изменения перед их объединением.
```bash
git fetch origin master
```

## 5. Отмена изменений (Undo)

### `git restore <файл>` (или `git checkout -- <файл>`)
Отменяет локальные изменения в файле, возвращая его к состоянию последнего коммита (или области индексации).
```bash
git restore index.html          # Отменить изменения в index.html
git restore .                   # Отменить все изменения в рабочем каталоге
```

### `git restore --staged <файл>` (или `git reset HEAD <файл>`)
Убирает файл из области индексации, оставляя изменения в рабочем каталоге.
```bash
git restore --staged index.html # Убрать index.html из индекса
```

### `git reset`
Изменяет указатель `HEAD` (ссылку на текущий коммит) и опционально рабочий каталог и/или область индексации.
*   **`git reset --soft <commit_hash>`**: Перемещает `HEAD`, но оставляет изменения в области индексации.
*   **`git reset --mixed <commit_hash>` (по умолчанию)**: Перемещает `HEAD` и очищает область индексации, оставляя изменения в рабочем каталоге.
*   **`git reset --hard <commit_hash>`**: **Опасная команда!** Перемещает `HEAD`, очищает область индексации и **удаляет все изменения** в рабочем каталоге до указанного коммита. Используйте осторожно!
```bash
git reset --soft HEAD~1         # Отменить последний коммит, оставив изменения в индексе
git reset --hard <commit_hash>  # Вернуться к указанному коммиту, удалив все последующие изменения
```

### `git revert <commit_hash>`
Создает новый коммит, который отменяет изменения, внесенные указанным коммитом. Это безопасный способ отмены изменений в общей истории, так как не переписывает ее.
```bash
git revert <commit_hash>
```

## 6. Конфигурация

### `git config`
Настраивает глобальные или локальные параметры Git.
```bash
git config --global user.name "Ваше Имя"        # Установить глобальное имя пользователя
git config --global user.email "ваш@email.com"  # Установить глобальный email пользователя
git config --list                             # Показать все настройки Git
```

---

**Важные советы:**
*   Всегда начинайте с `git status`, чтобы понять текущее состояние вашего репозитория.
*   Пишите осмысленные сообщения коммитов.
*   Не бойтесь экспериментировать с Git, но будьте осторожны с командами, которые переписывают историю (`git reset --hard`, `git push --force`).
*   Используйте `git help <команда>` (например, `git help commit`) для получения подробной документации по любой команде Git.
```