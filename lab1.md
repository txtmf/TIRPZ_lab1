## Національний технічний університет України<br>“Київський політехнічний інститут ім. Ігоря Сікорського”

## Факультет прикладної математики<br>Кафедра системного програмування і спеціалізованих комп’ютерних систем


# Лабораторна робота №1<br>"Базова робота з git"

## КВ-13 Дімова Марія

## Хід виконання роботи

### 1. Зклонувати будь-який невеликий проєкт open-source з github

#### 1. Зклонувати двічі: повний репозиторій, а також частковий, що міститиме лише один коміт однієї гілки за вашим вибором.

Створюємо теку для ЛР:

```
student@virt-linux:~$ mkdir ~/TIRPZ
student@virt-linux:~$ mkdir ~/TIRPZ/lab1
student@virt-linux:~$ cd ~/TIRPZ/lab1
student@virt-linux:~/TIRPZ/lab1$ 
```

Клонуємо репозиторій:

```
student@virt-linux:~/TIRPZ/lab1$ git clone https://github.com/SFML/SFML
Cloning into 'SFML'...
remote: Enumerating objects: 44873, done.
remote: Counting objects: 100% (1266/1266), done.
remote: Compressing objects: 100% (544/544), done.
remote: Total 44873 (delta 747), reused 962 (delta 610), pack-reused 43607
Receiving objects: 100% (44873/44873), 100.71 MiB | 8.07 MiB/s, done.
Resolving deltas: 100% (32446/32446), done.
```

Частково клонуємо репозиторій:

```
student@virt-linux:~/TIRPZ/lab1$ git clone https://github.com/SFML/SFML --depth=1 --single-branch --branch=lifetimes SFML-shallow
Cloning into 'SFML-shallow'...
remote: Enumerating objects: 1009, done.
remote: Counting objects: 100% (1009/1009), done.
remote: Compressing objects: 100% (818/818), done.
remote: Total 1009 (delta 340), reused 447 (delta 151), pack-reused 0
Receiving objects: 100% (1009/1009), 21.20 MiB | 4.10 MiB/s, done.
Resolving deltas: 100% (340/340), done.
```

#### 2. Показати різницю в розмірі баз даних двох клонів.

Порінюємо отримані репозиторії:

```
student@virt-linux:~/TIRPZ/lab1$ du -sh ./*/.git
103M	./SFML/.git
22M	./SFML-shallow/.git
```
### 2. Зробити не менше трьох локальних комітів

Створено три файли `1.txt`, `2.txt`, `3.txt`

Статус гілки після створення файлів:

```
student@virt-linux:~/TIRPZ/lab1$ cd SFML
student@virt-linux:~/TIRPZ/lab1/SFML$ git status
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	1.txt
	2.txt
	3.txt
nothing added to commit but untracked files present (use "git add" to track)
```
#### 1. Продемонструвати різні способи додавання файлів до індексу.

Додаємо файл `2.txt` до індексу командою `git add <files>`:

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git add 2.txt
```
Додаємо усі створені файли одразу командою `git add .`:

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git add .
```

Статус гілки після додавання файлів:

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   1.txt
	new file:   2.txt
	new file:   3.txt
```
#### 2. Продемонструвати різні способи вказання повідомлення коміту.

Коміт командою `git commit -m "<commit message>"`

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git commit -m "adding new files"
[master e53f0742] adding new files
 3 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 1.txt
 create mode 100644 2.txt
 create mode 100644 3.txt

```

Модифікуємо файл `2.txt` та `3.txt` та додаємо ці файли командою `git add .`. Робимо коміт командою `git commit`:

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git add .
student@virt-linux:~/TIRPZ/lab1/SFML$ git commit
[master 0885a95a] Modifying files 2.txt and 3.txt
 2 files changed, 2 insertions(+)
```

Текст вікна вводу повідомлення коміта:

```
Modifying files 2.txt and 3.txt
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# Your branch is ahead of 'origin/master' by 1 commit.
#   (use "git push" to publish your local commits)
#
# Changes to be committed:
#       modified:   2.txt
#       modified:   3.txt
#
```

Модифікуємо файл `1.txt` та робимо коміт командою `git commit -a`:

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git commit -a -m "Modifying file 1.txt"
[master 6f92ab3a] Modifying file 1.txt
 1 file changed, 1 insertion(+)

```

### 3. Продемонструвати уміння вносити зміни до останнього коміту за допомогою опції --amend.

Додаємо новий файл `text.txt` та модифікований файл `2.txt`. Вносимо зміни до останнього коміту:

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git add .
student@virt-linux:~/TIRPZ/lab1/SFML$ git commit --amend -m "adding text.txt and modifying 2.txt"
[master 32d052b5] adding text.txt and modifying 2.txt
 Date: Thu Oct 26 02:40:44 2023 +0300
 3 files changed, 2 insertions(+), 1 deletion(-)
 create mode 100644 text.txt
```

Статус гілки:

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git status
On branch master
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

Бачимо, що кількість комітів не змінилася, але змінився опис та наповнення останнього коміту.

### 4. Продемонструвати уміння об'єднати кілька останніх комітів в один за допомогою git reset.

Скасовуємо останні 2 коміта командою `git reset HEAD~2`, додаємо змінені файли та робимо один коміт.

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git reset HEAD~2
Unstaged changes after reset:
M	1.txt
M	2.txt
M	3.txt
student@virt-linux:~/TIRPZ/lab1/SFML$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   1.txt
	modified:   2.txt
	modified:   3.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	text.txt

no changes added to commit (use "git add" and/or "git commit -a")
student@virt-linux:~/TIRPZ/lab1/SFML$ git add .
student@virt-linux:~/TIRPZ/lab1/SFML$ git commit -m "joined commit"
[master a259871b] joined commit
 4 files changed, 3 insertions(+)
 create mode 100644 text.txt
```
### 5. Видалити файл(и) одним способом на вибір.

Видаляємо файл `text.txt` командою `git rm`:
```
student@virt-linux:~/TIRPZ/lab1/SFML$ git rm text.txt
rm 'text.txt'
```

Передивляємося статус гілки та робимо коміт:

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git status -uno
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	deleted:    text.txt

Untracked files not listed (use -u option to show untracked files)
student@virt-linux:~/TIRPZ/lab1/SFML$ git commit -m "deleting text.txt"
[master 94ed63ec] deleting text.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 text.txt

```

### 6. Перемістити файл(и) одним способом на вибір.

Переміщуємо файл `1.txt` командою `git mv`:

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git mv 1.txt 4.txt
```

Передивляємося статус гілки та робимо коміт:

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git status -uno
On branch master
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    1.txt -> 4.txt

Untracked files not listed (use -u option to show untracked files)
student@virt-linux:~/TIRPZ/lab1/SFML$ git commit -m "renaming 1.txt to 4.txt"
[master 6feaf465] renaming 1.txt to 4.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename 1.txt => 4.txt (100%)

```

### 7. Гілкування

#### 1. Створити три гілки, принаймні з одним унікальним комітом кожна

#### 2. Показати уміння переключатися між гілками

Створюємо гілку `my-local-branch-1` командою `git branch`:

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git branch my-local-branch-1
```
Переключаємось на створену гілку командою `git checkout`. Модифікуємо файл `2.txt` та робимо коміт:

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git checkout my-local-branch-1
Switched to branch 'my-local-branch-1'
student@virt-linux:~/TIRPZ/lab1/SFML$ git commit -a -m "modifying 2.txt"
[my-local-branch-1 a401886a] modifying 2.txt
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Створюємо нову гілку та одразу переключаємось на неї командою `git checkout -b`. Модифікуємо файл `3.txt` та робимо коміт.

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git checkout -b my-local-branch-2
Switched to a new branch 'my-local-branch-2'
student@virt-linux:~/TIRPZ/lab1/SFML$ git commit -a -m "Modifying 3.txt"
[my-local-branch-2 bb166f75] Modifying 3.txt
 1 file changed, 1 insertion(+), 1 deletion(-)
 ```
 
Аналогічно створюємо та переключаємось на нову гілку. Модифікуємо файл `4.txt` та робимо коміт.

 ```
student@virt-linux:~/TIRPZ/lab1/SFML$ git checkout -b my-local-branch-3
Switched to a new branch 'my-local-branch-3'
student@virt-linux:~/TIRPZ/lab1/SFML$ git commit -a -m "Modifying 4.txt"
[my-local-branch-3 75122c41] Modifying 4.txt
 1 file changed, 1 insertion(+), 1 deletion(-)
 ```

### 8. Продемонструвати уміння знайти в історії комітів набір комітів, в яких була зміна по конкретному шаблону в конкретному файлі.

Виведемо історію комітів командою `git log -G` із шаблонним текстом `"Hello"` у файлі `2.txt`:

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git log -G "Hello" 2.txt
commit a401886ae7f9e6a017616ad42cadcb9283bfd444 (my-local-branch-1)
Author: student <dimova.mariia@lll.kpi.ua>
Date:   Thu Oct 26 14:40:15 2023 +0300

    modifying 2.txt

commit a259871b7a4689023f64e240a222ea2d7d0b5a9b
Author: student <dimova.mariia@lll.kpi.ua>
Date:   Thu Oct 26 03:17:23 2023 +0300

    joined commit
```

Тепер порівняємо ці 2 коміти командою `git diff`:

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git diff a259871b7a4689023f64e240a222ea2d7d0b5a9b..a401886ae7f9e6a017616ad42cadcb9283bfd444 2.txt
diff --git a/2.txt b/2.txt
index 10ddd6d2..7da92cd4 100644
--- a/2.txt
+++ b/2.txt
@@ -1 +1 @@
-Hello!
+Hello)!
```

По виводу можна зробити висновок, що у старій версії файл мав рядок `Hello!`, а на його місці у новому файлі є рядок `Hello)!`.