## Ver los cambios de los archvios
- Saber que cambio hicimos en el archivo
```bash
git diff
```
- Saber los cambios del stage
```bash
git diff --staged
```

## Actualizar mensaje del commit y revertir commits
```bash
git commit --amend -m "Instalaciones actualizadas" 
```

## Poner modificaciones al commit anterior
El head puede ser remplazado por el hash de un commit
```bash
git reset --soft HEAD^
```

## Viajes en el tiempo
- Agregar un commit a un commit especifico
 ```bash
  git reset --soft ffb3276
  ```
- Volver a un commit y olvidar los commits anteriores
```bash
git reset --mixed 46d96ac
```
- Tener cuidado, es destructivo, te vuelve al commit que quieras
```bash
git reset --hard a932047
```
- Pero si se puede recuperar con 
```bash
# Primero ver todo lo sucedido
git reflog
# Tomamos el hash del commit que queremos recuperar y viajar en el tiempo
git reset --hard e4c593e
```

## Cambiar el nombre y eliminar archivos mediante git
- Cambiar nombre:
```bash
git mv destruir-mundo.md salvar-mundo.md
```
- Eliminar archivos
```bash
git rm salvar-mundo.md
```
- Si queremos revertir esto
```bash
git reset --hard
git checkout --.
```

## Cambiar el nombre y eliminar archivos fuera de git


## Ignorar archivos que no deseamos
.gitignore
