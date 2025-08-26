## 1) Setup inicial (primera vez en cada compu)
```bash
git clone <URL-del-repo>
cd <repo>

git fetch origin
git branch -r                  # ver ramas remotas

# crear la rama local que sigue a la remota del issue
git switch --track origin/2-gv-foto
# (para el otro issue, la primera vez)
# git switch --track origin/4-creacion-y-ajuste-de-modelos

git branch -vv                 # confirmar seguimiento
```
## 2) Ciclo de trabajo diario en tu rama del issue
```bash
# traer lo último del remoto
git fetch origin
git pull --rebase              # actualizar tu rama (2-gv-foto) desde origin/2-gv-foto

# integrar cambios recientes de main en tu rama (opción rebase)
git rebase origin/main

# trabajar y commitear
git status
git add -A
git commit -m "WIP: avance en /user/foto (refs #2)"

# subir tu trabajo
git push                       # si hiciste rebase antes:
# git push --force-with-lease

```

## 3) Cambiar entre ramas de issues
```bash
# si ya la creaste antes en esta compu:
git switch 2-gv-foto
git switch 4-creacion-y-ajuste-de-modelos

# si es la primera vez en esta compu:
git switch --track origin/4-creacion-y-ajuste-de-modelos
```
## 4) Trabajar desde otra computadora
```bash
git clone <URL-del-repo>
cd <repo>
git fetch origin
git switch --track origin/2-gv-foto
git pull --rebase
# trabajar normal...
```
## 5) Mantener tu rama al día y evitar conflictos
```bash
# al empezar y antes de pushear:
git fetch origin
git rebase origin/main         # o merge si así lo piden
# si rebaseaste y ya habías pusheado antes:
git push --force-with-lease
```
## 6) Antes de abrir el Pull Request
```bash
# limpia historial (squash) dejando 1–3 commits significativos
git fetch origin
git rebase -i origin/main      # pick/squash y reescribe mensajes

# sube la historia limpia
git push --force-with-lease
```

## 7) Después de que el PR se fusione a main
```bash
git switch main
git pull

# borrar la rama local y remota del issue (si ya la cerraron)
git branch -D 2-gv-foto
git push origin --delete 2-gv-foto
```
## 8) Extras útiles
```bash
git log --oneline --graph --decorate --all
git stash push -m "WIP local"  # guardar trabajo sin commitear
git stash pop                  # recuperar
git diff                       # ver cambios
git restore --staged .         # quitar del index si te equivocaste
```
