## Національний технічний університет України<br>“Київський політехнічний інститут ім. Ігоря Сікорського”

## Факультет прикладної математики<br>Кафедра системного програмування і спеціалізованих комп’ютерних систем


# Лабораторна робота №2<br>"Розширена робота з git"

## КВ-13 Дімова Марія

## Хід виконання роботи

### 1. Зклонувати репозиторій для ЛР2 використавши локальний репозиторій від ЛР1 в якості <br>"віддаленого".

Створюємо папку для ЛР2:

```
student@virt-linux:~/TIRPZ$ mkdir ~/TIRPZ/lab2
student@virt-linux:~/TIRPZ$ cd ~/TIRPZ/lab2
student@virt-linux:~/TIRPZ/lab2$ 
```

Клонуємо репозиторій для ЛР2. Для цього використовуємо абсолютний шлях до локальної папки з репозиторієм від ЛР1:

```
student@virt-linux:~/TIRPZ/lab2$ git clone file:///home/student/TIRPZ/lab1/SFML
Cloning into 'SFML'...
remote: Enumerating objects: 43845, done.
remote: Counting objects: 100% (43845/43845), done.
remote: Compressing objects: 100% (8936/8936), done.
remote: Total 43845 (delta 31784), reused 43785 (delta 31756)
Receiving objects: 100% (43845/43845), 96.96 MiB | 42.89 MiB/s, done.
Resolving deltas: 100% (31784/31784), done.
```

### 2. Робота з ремоутами.

Перевіряємо, що у копії репозиторію ЛР2 присутні гілки, які ми створювали при виконанні ЛР1:

```
student@virt-linux:~/TIRPZ/lab2$ cd SFML
student@virt-linux:~/TIRPZ/lab2/SFML$ git branch -a
* my-local-branch-3
  remotes/origin/HEAD -> origin/my-local-branch-3
  remotes/origin/master
  remotes/origin/my-local-branch-1
  remotes/origin/my-local-branch-2
  remotes/origin/my-local-branch-3
```

Перевіряємо куди "дивиться" наш поточний ремоут `origin`:

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git remote -v
origin	file:///home/student/TIRPZ/lab1/SFML (fetch)
origin	file:///home/student/TIRPZ/lab1/SFML (push)
```

Додаємо новий ремоут, використовуючи URI на інтернет-джерело репозиторію.

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git remote add upstream https://github.com/SFML/SFML.git
```

Список віддалених гілок:

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git remote -v
origin	file:///home/student/TIRPZ/lab1/SFML (fetch)
origin	file:///home/student/TIRPZ/lab1/SFML (push)
upstream	https://github.com/SFML/SFML.git (fetch)
upstream	https://github.com/SFML/SFML.git (push)
```

Створюємо нову гілку `lab2-branch`.

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git checkout -b lab2-branch
Switched to a new branch 'lab2-branch'
```

Робимо кілька комітів:

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git add .
student@virt-linux:~/TIRPZ/lab2/SFML$ git commit -m "n1.txt commit"
[lab2-branch a8d7148b] n1.txt commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 n1.txt
student@virt-linux:~/TIRPZ/lab2/SFML$ git add .
student@virt-linux:~/TIRPZ/lab2/SFML$ git status
On branch lab2-branch
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   n1.txt
	new file:   n2.txt

student@virt-linux:~/TIRPZ/lab2/SFML$ git commit -m "n1.txt modified n2.txt added"
[lab2-branch 572c8a16] n1.txt modified n2.txt added
 2 files changed, 1 insertion(+)
 create mode 100644 n2.txt
```

Пушимо гілку на ремоут `origin` (створений з ЛР1), не зв'язуючи гілки.

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git push origin lab2-branch
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 2 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 503 bytes | 71.00 KiB/s, done.
Total 6 (delta 2), reused 1 (delta 0)
To file:///home/student/TIRPZ/lab1/SFML
 * [new branch]        lab2-branch -> lab2-branch
```

Додаємо до гілки ще один коміт.

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git add .
student@virt-linux:~/TIRPZ/lab2/SFML$ git commit -m "n2.txt modified n3.txt added"
[lab2-branch f479b75d] n2.txt modified n3.txt added
 2 files changed, 1 insertion(+)
 create mode 100644 n3.txt
```

Пушимо зміни гілки на ремоут `origin`, зв'язуючи гілки.

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git push -u origin lab2-branch
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 290 bytes | 290.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
To file:///home/student/TIRPZ/lab1/SFML
   572c8a16..f479b75d  lab2-branch -> lab2-branch
Branch 'lab2-branch' set up to track remote branch 'lab2-branch' from 'origin'.
student@virt-linux:~/TIRPZ/lab2/SFML$ git push
Everything up-to-date
```

Додаємо до гілки ще один коміт.

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git add .
student@virt-linux:~/TIRPZ/lab2/SFML$ git commit -m "n3.txt modified"
[lab2-branch 0cf52cb8] n3.txt modified
 1 file changed, 1 insertion(+)
```

Пушимо зміни гілки на ремоут `origin` за допомогою команди `git push` завдяки тому, що ми зв'язали гілки.

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 280 bytes | 280.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
To file:///home/student/TIRPZ/lab1/SFML
   f479b75d..0cf52cb8  lab2-branch -> lab2-branch
```

Перевіряємо поточний стан гілок в репозиторії ЛР1, і бачимо що тут з'явилась нова локальна гілка `lab2-branch`, яку ми пушнули.

```
student@virt-linux:~/TIRPZ/lab1/SFML$ git branch -a
  lab2-branch
  master
  my-local-branch-1
  my-local-branch-2
* my-local-branch-3
```

### 3. Змерджити гілку, що була створена при виконанні ЛР1, в поточну гілку lab2-branch.

Мерджимо віддалену гілку `my-local-branch-3` командою `git merge`:

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git merge origin/my-local-branch-3
Merge made by the 'recursive' strategy.
 4.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
student@virt-linux:~/TIRPZ/lab2/SFML$ git log --graph
*   commit 4737d1c7aa92bd978c14eb7e1e69f80f171035a9 (HEAD -> lab2-branch)
|\  Merge: 06eff8c4 a8f9bdb5
| | Author: student <dimova.mariia@lll.kpi.ua>
| | Date:   Thu Dec 14 00:23:49 2023 +0200
| | 
| |     Merge remote-tracking branch 'origin/my-local-branch-3' into lab2-branch
| | 
```

### 4. Перенесення комітів.

Створюємо нову гілку `lab2-branch-2`.

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git checkout -b lab2-branch-2
Switched to a new branch 'lab2-branch-2'
```

Робимо в ній три коміти:

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git add .
student@virt-linux:~/TIRPZ/lab2/SFML$ git commit -m "cola1.txt added"
[lab2-branch-2 a73c7fc1] cola1.txt added
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 cola1.txt

student@virt-linux:~/TIRPZ/lab2/SFML$ git add .
student@virt-linux:~/TIRPZ/lab2/SFML$ git commit -m "cola2.txt added"
[lab2-branch-2 6be37c10] cola2.txt added
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 cola2.txt

student@virt-linux:~/TIRPZ/lab2/SFML$ git add .
student@virt-linux:~/TIRPZ/lab2/SFML$ git commit -m "cola3.txt added"
[lab2-branch-2 80ede238] cola3.txt added
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 cola3.txt
```

За допомогою команди `git log` дізнаємося хеш потрібного нам коміту (другого).

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git log
commit 80ede2385639d5241bb1217d8f817de6d614084d (HEAD -> lab2-branch-2)
Author: student <dimova.mariia@lll.kpi.ua>
Date:   Thu Dec 14 01:13:42 2023 +0200

    cola3.txt added

commit 6be37c10ea86a12cc43823d4594b0148f064de88
Author: student <dimova.mariia@lll.kpi.ua>
Date:   Thu Dec 14 01:13:08 2023 +0200

    cola2.txt added

commit a73c7fc1775179a7eae1dff6c89b8bceb170c794
Author: student <dimova.mariia@lll.kpi.ua>
Date:   Thu Dec 14 01:12:38 2023 +0200

    cola1.txt added

```

Переключаємось на гілку, у яку ми хочемо перенести коміт, у нашому випадку це `lab2-branch`. Та за допомогою команди `git cherry-pick` і хешу потрібного коміту, переносимо коміт.

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git checkout lab2-branch
Switched to branch 'lab2-branch'
Your branch is ahead of 'origin/lab2-branch' by 3 commits.
  (use "git push" to publish your local commits)
student@virt-linux:~/TIRPZ/lab2/SFML$ git cherry-pick 6be37c10ea86a12cc43823d4594b0148f064de88
[lab2-branch fd28abfd] cola2.txt added
 Date: Thu Dec 14 01:13:08 2023 +0200
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 cola2.txt
```

Демонстрація перенесення коміту:

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git log --pretty=oneline --graph -n 10 --branches
* fd28abfd6066bae18d030d4f8ba232906279682b (HEAD -> lab2-branch) cola2.txt added
*   4737d1c7aa92bd978c14eb7e1e69f80f171035a9 Merge remote-tracking branch 'origin/my-local-branch-3' into lab2-branch
|\  
| * a8f9bdb598eec222961cf35078ad57c6626a996a (origin/my-local-branch-3, origin/HEAD) 4.txt modified
* | 06eff8c49633a46e33e5ee8767cca1612c0d06fd n1.txt modified
* | 0cf52cb8493b53c6f59bcdbcdac61a8fd8a4d43a (origin/lab2-branch) n3.txt modified
* | f479b75d230ee9c83d7e8f5c689f4e1f019619c1 n2.txt modified n3.txt added
* | 572c8a1633b0e0a26f136d1b4c428cf9c6493e95 n1.txt modified n2.txt added
* | a8d7148b4f6389986b4a5a1c62a06924f2a06940 n1.txt commit
|/  
* 75122c410753005fe1a33455b8bd41e3bfb06d47 (my-local-branch-3) Modifying 4.txt
* bb166f75c3280a21bb9f13577923cb5ff407f1e2 (origin/my-local-branch-2) Modifying 3.txt

```

### 5. Визначити останнього спільного предка між двома будь-якими гілками.

Визначаємо останнього спільного предка між гілками 
`lab2-branch`  та `lab2-branch-2` за допомогою команди `git merge-base`. У результаті ми отримуємо хеш "базового" коміту, після якого гілки розійшлися.

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git merge-base lab2-branch lab2-branch-2
6feaf4657b2c09a205c1702ec7ec9232d833006f
```

### 6. Робота з ничкою.

Робимо трохи `unstaged` змін:
```
student@virt-linux:~/TIRPZ/lab2/SFML$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 4 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   n1.txt
	modified:   n3.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Зберігаємо зі зміни до нички командою `git stash`

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git stash
Saved working directory and index state WIP on lab2-branch: fd28abfd cola2.txt added
```

Як бачимо, ми отримали чисте робоче дерево:

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 4 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

```

Знову робимо трохи `unstaged` змін та зберігаємо їх у ничку.

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git stash
Saved working directory and index state WIP on lab2-branch: fd28abfd cola2.txt added
```

За допомогою команди `git stash list` переглядаємо вміст нички. Як бачимо, там знаходяться два захованих стани.

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git stash list
stash@{0}: WIP on lab2-branch: fd28abfd cola2.txt added
stash@{1}: WIP on lab2-branch: fd28abfd cola2.txt added

```

Дістаємо з нички перші збережені зміни за допомогою команди `git stash apply stash@{n}`. Як бачимо, до поточного робочого дерева застосовано саме перший збережений стан.

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git stash apply stash@{1}
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 4 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   n1.txt
	modified:   n3.txt

no changes added to commit (use "git add" and/or "git commit -a")

```

### 7. Робота з файлом `.gitignore`.

Створюємо файли та дивимось статус:

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 5 commits.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	gi1.txt
	gi2.kvfpm
	gi3.kvfpm

nothing added to commit but untracked files present (use "git add" to track)
```

Тепер змінимо файл .gitignore (він вже існував у проєкті) та додамо у нього шаблон `*.kvfpm`. Після цього знову дивимось статус:

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 5 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   .gitignore

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	gi1.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Як бачимо, файли з розширенням `.kvfpm` ігноруються та не відображаються у статусі. Тепер перевіримо його з файлами, що ігноруються:

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git status --ignored
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 5 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   .gitignore

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	gi1.txt

Ignored files:
  (use "git add -f <file>..." to include in what will be committed)
	gi2.kvfpm
	gi3.kvfpm

no changes added to commit (use "git add" and/or "git commit -a")
```

Файли відображаються. Тепер почистимо всі untracked файли:

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git clean -fdx
Removing gi1.txt
Removing gi2.kvfpm
Removing gi3.kvfpm
```

### 8.  Робота з `reflog`.

Видалимо гілку `lab2-branch` та переглянемо reflog командою `git reflog`:

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git branch -D lab2-branch
Deleted branch lab2-branch (was d2dd357c).
student@virt-linux:~/TIRPZ/lab2/SFML$ git reflog
6feaf465 (HEAD -> master, origin/master) HEAD@{0}: checkout: moving from lab2-branch to master
d2dd357c HEAD@{1}: commit: n1.txt and n3.txt
fd28abfd HEAD@{2}: reset: moving to HEAD
fd28abfd HEAD@{3}: reset: moving to HEAD
fd28abfd HEAD@{4}: reset: moving to HEAD
```

Тепер створимо нову гілку `lab2-ressurected` та переключимося на неї:

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git branch lab2-ressurected d2dd357c
student@virt-linux:~/TIRPZ/lab2/SFML$ git checkout lab2-ressurected 
M	.gitignore
Switched to branch 'lab2-ressurected'
```

Також можна переглянути лог:

```
student@virt-linux:~/TIRPZ/lab2/SFML$ git log --pretty=oneline --graph -n5
* d2dd357c5a5c649a30fc87ac3ed39d3e8d6e91db (HEAD -> lab2-ressurected) n1.txt and n3.txt
* fd28abfd6066bae18d030d4f8ba232906279682b cola2.txt added
*   4737d1c7aa92bd978c14eb7e1e69f80f171035a9 Merge remote-tracking branch 'origin/my-local-branch-3' into lab2-branch
|\  
| * a8f9bdb598eec222961cf35078ad57c6626a996a (origin/my-local-branch-3, origin/HEAD) 4.txt modified
* | 06eff8c49633a46e33e5ee8767cca1612c0d06fd n1.txt modified
```