Para hacer un cambio tenemos que hacer un fork, despues de ahi podemos hacer nuestros commits y push, para enseguida hacer un pull request al proyecto principal.

# FORK
## Actualizando fork - practica
Actualizar el fork para tener la ultima version que se esta trabajando puede resultar muy util, este paso se puede hacer desde github, no hay problema, despues hacer un pull
Si queremos hacer ambos desde la consola:
```bash
git remote -v
git remote add upstream <https://>
git remote -v
git pull 
# no sucedera nada porque es mi repo perosnal
git pull upstream master
git commit -am "upstream actualizado"
git rebase --continue
git pull
git push
```


# INTRODUCCION A LOS FLUJOS DE TRABAJO
## Feature Branch - Flujo de trabajo mediante pull request
NO TRABAJAR EN LA RAMA MAIN!
Creamos otra rama:
```bash
git checkout -b rama-villanos
```

como subir la nueva rama:
```bash
git push --set-upstream origin rama-villanos
```
cuando dejes de trabajar la rama, basicamente la borras de github pero quedara en git, por eso solo hacemos un:
```
git branch -d rama-villanos -f
```

# Feature Branch - Revisando el trabajo de otros compañeros
Traer la rama de mi compañero para revisar la rama de mi compañero
```bash
❯ git pull --all
Already up to date.
❯ git branch
* main
❯ git branch --all
* main
  remotes/origin/main
  remotes/origin/rama-misiones
  remotes/origin/rama-villanos
❯ git checkout rama-misiones
branch 'rama-misiones' set up to track 'origin/rama-misiones'.
Switched to a new branch 'rama-misiones'
```

### Mucha basura
```bash
 git branch
  main
* rama-misiones
❯ git branch -a
  main
* rama-misiones
  remotes/origin/main
  remotes/origin/rama-misiones
  remotes/origin/rama-villanos
PC ~\Desktop\avengers-master rama-misiones ≡ 
❯ 
```

como purgar esto, ya que asi siempre nos dara error:
```bash
❯ git push origin :rama-misiones
error: unable to delete 'rama-misiones': remote ref does not exist
error: failed to push some refs to 'https://github.com/DavoDev-Hub/avengers-curso.git'
PC ~\Desktop\avengers-master main ≡  949ms 
❯ 
```
Esto actualiza bien las ramas:
```bash
❯ git remote prune origin
Pruning origin
URL: https://github.com/DavoDev-Hub/avengers-curso.git
 * [pruned] origin/rama-misiones
 * [pruned] origin/rama-villanos
PC ~\Desktop\avengers-master main ≡  509ms 
❯ 
```

# RAMA DE PRODUCCION
Como mantener una rama de manera perpetua creando una tag, los tags perduran si se borra la rama

Si borraron la rama de github y de git, se puede recuperar de la siguiente manera (con la tag): 
```
git checkout v0.0.1
git s
git checkout -b rama-kitkat
git lg
git push
git push --set-upstream origin rama-kitkat
git checkout main
```

