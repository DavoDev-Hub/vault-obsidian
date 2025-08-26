- No trabajar mucho con stash
WIP + WORK IN PROGRESS
## Stash
Ejemplo: 
- Supon un gran proyecto al que se le asignaron varios archivos, pero tu jefe dice que ya quiere desplegar el archivo, pero ese no esta listo
- Aqui se usa el stash, que es como una caja donde se almacenan los cambios no listos para lanzar la aplicacion con lo que funciona y despues ir agregando el stash sin conflictos
```bash
git stash
#Saved working directory and index state WIP on master: 5440fe5 Resolviendo conflictos
❯ git s  
#On branch master
#nothing to commit, working tree clean
```

- Ver referencias del stash:
```bash
git stash list
```

- Recuperar el trabajo del stash:
```bash
 git stash pop
# ❯ git stash pop

# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#  (use "git restore <file>..." to discard changes in working directory)
#	modified:   misiones.md

# no changes added to commit (use "git add" and/or "git commit -a")
# Dropped refs/stash@{0} (945ce245bdb6657df0636eb6cbfd59755e3f0c49)
# 07-demo-stash git:master*  
❯ git commit -am "Misiones.md: Actualizada"
#[master 7d020e2] Misiones.md: Actualizada
# 1 file changed, 1 insertion(+)
```

## Borrar stash basura
```bash
git stash clear
# Borras todos los stash, puedes recuperarlo con reflog
```

## Borrar un stash especifico
```bash
git stash drop stash@{0}
```

- Los stashes no proporcionan mucha infromacion, pero podriamos guardarlos con nombres especificos
```bash
git stash show stash@{2}
❯ git stash save "Agregamos a loki en villanos"
Saved working directory and index state On master: Agregamos a loki en villanos
stash@{0}: On master: Agregamos a loki en villanos
stash@{1}: WIP on master: 16c55eb Conflictos con el stash resueltos
stash@{2}: WIP on master: 16c55eb Conflictos con el stash resueltos
stash@{3}: WIP on master: 16c55eb Conflictos con el stash resueltos
```

## GIT REBASE

## Actualizando una rama **
```bash
git rebase master
```

## Rebase - Squash

```bash
* 43e250b - (18 seconds ago) Actualizamos misiones completadas - DavoDev-Hub (HEAD -> master)
* 38bb8f6 - (8 years ago) Actualizamos dos misiones completadas al momento - Strider
```

poner una s y una p a las que quieras unir
```bash
❯ git rebase -i HEAD~4 
[detached HEAD 539eaf8] Actualizamos dos misiones completadas al momento
 Author: Strider <fernando.herrera85@gmail.com>
 Date: Fri Jun 23 15:44:41 2017 -0600
 1 file changed, 4 insertions(+)
Successfully rebased and updated refs/heads/master.
```

## Reword
```bash
git rebase -i HEAD~4
#pick 300c014 Misiones nuevas agregadas
#pick 158ba9e Se agrego a la liga: Volcán Negro
#pick 0a4d7c0 Misiones-Completadas.md agregado
#r f3cea73 Misiones completadas actualizadas
```
* 0a4d7c0 - (8 years ago) Misiones-Completadas.md agregado - Strider
* 158ba9e - (8 years ago) Se agrego a la liga: Volcán Negro - Strider
Si ya fueron pusheados los commits, es mejor dejarlo asi

## Rebase - edit

Quitar el readme del commit
```bash
❯ git s
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md
	modified:   misiones.md
	modified:   villanos.md

no changes added to commit (use "git add" and/or "git commit -a")
08-demo-rebase git:master*  
❯ git checkout -- README.md 
```
Digamos que ya hicimos el commit:
Pero queremos crear commits independientes por cada archivo modificado
```
08-demo-rebase git:master*  
❯ git add .
08-demo-rebase git:master*  
❯ git commit -m "commits"
[master b9088fe] commits
 2 files changed, 3 insertions(+), 1 deletion(-)
```

```bash
pick 0a4d7c0 Misiones-Completadas.md agregado
pick f3cea73 Misiones completadas actualizadas
e b9088fe commits
```

aqui dice que estamos en medio de un rebase iteractivo
```
 git status
interactive rebase in progress; onto 158ba9e
Last commands done (3 commands done):
   pick f3cea73 Misiones completadas actualizadas
   edit b9088fe commits
  (see more in file .git/rebase-merge/done)
No commands remaining.
You are currently editing a commit while rebasing branch 'master' on '158ba9e'.
  (use "git commit --amend" to amend the current commit)
  (use "git rebase --continue" once you are satisfied with your changes)

nothing to commit, working tree clean
```

Aqui ya estariamos donde estan los dos archivos modificados, listo para hacer doble commit separado:
```
❯ git reset HEAD^
Unstaged changes after reset:
M	misiones.md
M	villanos.md
```

```
08-demo-rebase git:master*  
❯ git add villanos.md
```

```
❯ git status
interactive rebase in progress; onto 158ba9e
Last commands done (3 commands done):
   pick f3cea73 Misiones completadas actualizadas
   edit b9088fe commits
  (see more in file .git/rebase-merge/done)
No commands remaining.
You are currently editing a commit while rebasing branch 'master' on '158ba9e'.
  (use "git commit --amend" to amend the current commit)
  (use "git rebase --continue" once you are satisfied with your changes)
```

```
❯ git reset HEAD^
Unstaged changes after reset:
M	misiones.md
M	villanos.md
```

```
08-demo-rebase git:master*  
❯ git s
interactive rebase in progress; onto 158ba9e
Last commands done (3 commands done):
   pick f3cea73 Misiones completadas actualizadas
   edit b9088fe commits
  (see more in file .git/rebase-merge/done)
No commands remaining.
You are currently splitting a commit while rebasing branch 'master' on '158ba9e'.
  (Once your working directory is clean, run "git rebase --continue")
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   villanos.md
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   misiones.md
```

```
08-demo-rebase git:master*  
❯ git commit -m "Agregamos a deadshot"
[detached HEAD c21a835] Agregamos a deadshot
 1 file changed, 1 insertion(+)

08-demo-rebase git:master*  
❯ git commit -am "Misiones actualizadas"
[detached HEAD 0485b07] Misiones actualizadas
 1 file changed, 2 insertions(+), 1 deletion(-)
```

```
❯ git rebase --continue
Successfully rebased and updated refs/heads/master.
```

```
* 0485b07 - (5 minutes ago) Misiones actualizadas - DavoDev-Hub (HEAD -> master)
* c21a835 - (5 minutes ago) Agregamos a deadshot - DavoDev-Hub
```

