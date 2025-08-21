## Primeros comandos de push a github 
```bash
echo "liga-justicia" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https...
git push -u origin main
```

## Subir las tags
```bash
git tag
```

## Realease tags
Son importantes para considerar cambios maduros (irse a github -> tags )

## GIT PULL
git pull, sirve para traer los datos que se encuentran en el origen seteado por defecto

```bash
git pull origin main
# se puede especificar la rama
```

## Git remote -v 
Mirar el path donde se encuentra el repositorio
```bash
git remote -v
```

## Warning- Pulling without reconcile strategy
Para solo traer cambios fast forward
```bash
git config --global pull.ff only
```
global:
```bash
git config --global pull.rebase true
```
## Clonar un repositorio
```bash
git clone https://github.com/DavoDev-Hub/gitcourse   
```
## Subir cambios locales al remoto
```bash
git add .
git commit -m "Cambios"
git push
```
#### Errores comunes cuando actualizas desde github y desde el local el mismo archivo
```bash
❯ git pull
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 956 bytes | 956.00 KiB/s, done.
From https://github.com/DavoDev-Hub/gitcourse
   a15e9c6..a054e63  main       -> origin/main
fatal: Not possible to fast-forward, aborting.
```
Para solucionar esto
```
git config pull.rebase true
```
y ahora nos encontraremos en un punto de rebase
entranos y modificamos el archvio que causa conflicto,, aceptamos si queremos alguno de los dos cambios y hacemos add . y commit
y ya por ultimo 
git rebase --continue

