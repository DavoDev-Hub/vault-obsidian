## Revisar version y help
Revisar la version de git
```bash
git --version
```

Ver la ayuda de git
```bash
git help
```

La documentacion de la web pero en la consola
```bash
git help commit
```
para salir del help :q

## Registrar
```bash
git config --global user.name "DavoDev-Hub"
git config --global user.email "juanpajmz13@gmail.com"
```

Si queremos confirmar que todo esto se hizo bien
```bash
git config --global -e
```

## Primer repositorio
- Iniciar nuestro repositorio
```bash
git init
```

- Esto se recomienda, para que cada vez que se inicialice un repositorio tenga el nombre de la rama que queremos
```bash
git config --global init.defaultBranch <name>
```

- Nunca borrar el repositorio .git:
*drwxr-xr-x 7 davo davo  4096 Aug 20 16:17 .git*

Dar informacion sobre los commits y la rama que estas trabajando
```bash
git status
```

Para darles seguimiento a los archivos que queremos agregar al commit
```bash
git add index.html
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   index.html
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store
	css/
	fonts/
	images/
```

Esto es muy tedioso, hacerlo uno por uno, asi que debemos de hacer:
```bash
git add *
```

Si metimos al comit un archivo que no queriamos entonces debemos de hacer
```bash
git reset <nombre_del archivo>
```

Ya para hacer el commit, poner un nombre claro. Esto se hace para hacer el registro de los archivos a los cuales hicimos git add
```bash
git commit -m "First commit" 
```

SE HACE COMMIT CUANDO HACEMOS UNA FUNCIONALIDAD IMPORTANTE

## Respaldos, recuperar commit
Reconstruir el proyecto al ultimo commit
```bash
git checkout --.
```

## Cambiar nombre de la rama Master a Main
Saber que rama estamos trabajando
Siempre trabajar en ramas
```bash
git branch
# *master
```

cambiar el nombre de la rama
```bash
git branch -m master main
# *main
```

Configuracion global para inicializar main en vez de branch
```bash
git config --global init.defaultBranch main
```

Si el archivo ya le estamos dando seguimiento
```bash
git commit -am "Readme actualizado"
```

Para ver los logs del repositorio
```bash
git log
#commit d832219b5df92bd499818a40c5a2f2081d4b7ed7 (HEAD -> main)
#Author: DavoDev-Hub <juanpajmz13@gmail.com>
#Date:   Wed Aug 20 16:48:51 2025 -0600
#   Readme added
```

## Formas de agregar archivos al commit
- Agregar todos los html al commit (desde la carpeta en la que se encuentra el archivo)
```bash
git add *.html
git add js/*.js
```
- Si creamos un archvio vacio, git no le da seguimiento, pero si dentro del directorio ponemos un archivo .gitkeep
```bash
.gitkeep
git add carpeta/.gitkeep
```
- Para tomar todo lo de una carpeta
```bash
git add css/
git commit -m "css added"
```

- Agregar todo:
```bash
git add .
```

## Crear Alias para comandos
```bash
git status --short
#M index.html
```

Para hacer este short efectivo:
```bash
git config --global alias.s "status --short"
```

```bash
git log --oneline
```









