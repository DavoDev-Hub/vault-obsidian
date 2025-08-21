Las ramas son como una version diferente de proyecto, es un desprendimineto para experimentar.
Una linea del tiempo completamente aparte
#### MERGE
Son las uniones de commits entre ramas

## MERGE : Fast-Forward
- Cambiar de rama y o crear rama
```bash
git branch rama-villanos
git branch
# *master
# rama-villanos
git checkout rama-villanos 
# Switched to branch 'rama-villanos'
```

- Unir ramas
	- Estar en la rama que espera los cambios
```bash
git merge rama-villanos 
# Updating 62c8a10..f998cfe
# Fast-forward
# villanos.md | 6 ++++++
# 1 file changed, 6 insertions(+)
# create mode 100644 villanos.md
```

- Borrar ramas que ya no ocupamos (conveniente cuando terminamos de trabjaar con una rama)
```bash
git branch -d rama-villanos
# git branch -d rama-villanos -f
```

## Merge : Union automatica
- Crear las ramas de una manera mas eficiente
```bash
❯ git checkout -b rama-villanos
Switched to a new branch 'rama-villanos'
```
-Git logra unificar los cambios de manera automatica sin alterar archivos
```bash
git merge rama-villanos 
#Merge made by the 'ort' strategy.
# villanos.md | 2 ++
# 1 file changed, 2 insertions(+)
```
```
   6372807 - (10 minutes ago) Merge branch 'rama-villanos'!!! - DavoDev-Hub (HEAD -> master)
|\  
| * c202cf4 - (14 minutes ago) Notas en villanos - DavoDev-Hub (rama-villanos)
| * 450ef9e - (15 minutes ago) Agregamnos a Doomsday - DavoDev-Hub
* | 266d5de - (12 minutes ago) Borramos a Daredevil - DavoDev-Hub
|/ 
```

## Merge : Uniones con conflicto
- Se origina cuando dos devs hacen cambios en el mismo lugar del codigo
	- aqui modificamos un archivo en dos ramas distintas, si queremos hacer un merge dara un error
```bash
❯ git merge rama-conflicto 
Auto-merging misiones.md
CONFLICT (content): Merge conflict in misiones.md
Automatic merge failed; fix conflicts and then commit the result.
```
Basicamente quiere saber git cual archivo es el bueno, o cual cambio aceptar
```
# misiones.md <- archivo con conflicto
# Misiones
1. Acabar con el plan de Lex Luthor
2. Crear la liga de la justicia
<<<<<<< HEAD
3. Buscar nuevos miembros que luchen por la justicia
4. Buscar comida para ellos.
=======
5. Buscar nuevos miembros que sean super heroes
>>>>>>> rama-conflicto
```
Basicamente podemos modificar el archivo manual para dejar solo una modificacion
```
1. Acabar con el plan de Lex Luthor
2. Crear la liga de la justicia
3. Buscar nuevos miembros que luchen por la justicia
4. Buscar comida para ellos.
```

```bash
❯ git s
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)
Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both modified:   misiones.md
no changes added to commit (use "git add" and/or "git commit -a")
06-demo git:master  
❯     
```

```bash 
❯ git commit -am "Union con rama-conflicto"
[master a30dd58] Union con rama-conflicto     
```

## Tags - Etiquetas
Hace referencia a un commit y a todo el punto del proyecto en especifico
- Digamos que este punto ya esta listo
```bash
 a30dd58 - (5 minutes ago) Union con rama-conflicto - DavoDev-Hub (HEAD -> master)
```
- Para crear un tag 
```bash
git tag super-release
```
- queda asi y siempre se quedara, el tag sirve para muchas cosas, moverse en el tiempo, checkouts, etc
```bash 
a30dd58 - (7 minutes ago) Union con rama-conflicto - DavoDev-Hub (HEAD -> master, tag: super-release)
```

- Con:
```
 git tag
```
Vemos las tags que creamos
- Para borrar tags:
```bash
❯ git tag -d super-release 
Deleted tag 'super-release' (was a30dd58)
```

- Es mejor ponerle una version semantica correcta (al ultimo commit obivamente)
```bash
git tag -a v1.0.0 -m "Version 1.0.0 lista"
```

- v1 -> Version mayor
- .0 -> funcionalidad, no version mayor
- .0 -> Bug fix

- Como crear tags en otros puntos:
```
git tag -a v0.1.0 f998cfe -m "Version Alpha de nuestra app"
```
- Ver mas informacion de los tags
```
06-demo git:master  
❯ git show v0.1.0 
```

