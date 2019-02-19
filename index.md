# PRIMEROS PASOS
git init  -- crear repositorio local
git status -- Que se modifico, que archivos estan listos, en que lugar trabajamos
git add . -- Archivos que queremos enviar
git commit -m "primer commit"  -- registro historico de los archivos

git remote add origin <url repositorio remoto>
git remote -v
git commit -am "asdad"
git push -u origin master

# GUIA

### recuperar archivo o revertir cambios
git checkout -- .
git checkout -- README.md

### configuración
git config --global user.name <name>
git config --global user.email <email>
git config --global -e

### log
git log
git log --oneline -- forma reducida
git log --oneline --decorate --all --graph -- (decorate y graph con ramas se ve mejor)
git log 

### alias
git config --global -e  (ver archivo con las configuraciones)
git config --global -l  (ver archivo con las configuraciones - modo lectura)
git config --global alias.lg "log --oneline --decorate --all --graph"
git config --global alias.s "status -s -b"
git config --global alias.a "git add . && git status"
git config --global alias.aa "git add . && git add -u . && git status"
git config --global alias.ac "git add . && git commit"

### eliminar alias
git config --global --unset alias.a

### quitar error
git config core.autocrlf true (eliminar error en el git add -A)

### Formas de añadir
git add . -- todos
git add index.html -- archivo unitario
git add *.png -- archivos extension
git add css/ -- archivos dentro de una carpeta
git add -A -- agrega todos los archivos modificados
git add "*.txt" -- agrega todos los txt de TODO el proyecto que hayamos modificado
git add *.txt -- Agrega todos los txt en el directorio actual
git add --all -- Agrega todos los archivos modificados
git add <lista de archivos>
git add pdfs/*.pdf -- Agrega los archivos con extension pdf dentro de la carpeta pdfs

### excluir
git reset *.xml
git reset HEAD README.md
git reset --soft HEAD^ (dejar último commit a la escucha)
(HEAD es ultimo commit)
git reset --soft 31e77e0 (volver a un commit anterior)
git reset --mixed b409281 (volver atras y dejar en editados)
git reset --hard b409281 (borramos todos los cambios y lo dejamos en este punto)

### recuperar archivos
git reflog (log de todos los commit, reset, etc)
git reset --hard b409281 (id del commit al que queremos volver)

### commit
git commit
	-m (comentario)
	-am (añadir al estage y añadir comentario)
	--amend -m "Actualizamos el README" (cambiar último comentario)

### cambiar nombre de archivo
git mv destruir-mundo.txt.txt salvar-mundo.txt
(al terminar realizar commit)

### eliminar archivo
git rm salvar-mundo.txt

### status
git status
	-s -- silent
	-b -- rama

### ver diferencias
git diff
	--staged (ver diferencias incluyendo el escenario)

### actualizar 
git add -u

### al salir del modo editar
:q (salir)
:wq (escribir y salir)

### cambiar nombre y eliminar fuera de git
(renombrar)
git add -u
git add -A 
git commit -m "Renombrando la historia de superman"
(eliminar)
git add -u
git commit -m "Eliminamos la historia de batman"

## Ramas: Es una línea de tiempo de commits
### Merge: Uniones. Formas de unir.
	- Fast-forward: cuando no hay cambios en la rama principal
	- Automaticas: Cuando hay modificaciones en la rama principal pero 	no afectan unas a otras.
	- Manual: modo conflicto.

### crear rama
git branch rama-villanos

### ver ramas 
git branch (en verde la rama en la que te encuentres)
git branch -a (remotas)
### moverte a rama
git checkout rama-villanos

### crear rama y moverte a ella
git checkout -b rama-villano

### ver diferencias
git diff rama-villanos master

### unir ramas en modo Fast-forward
(estamos en la rama-villanos)
git checkout master
git merge rama-villanos

### borrar rama
git branch -d rama-villanos
git branch -D <name>
git push origin :rama-misiones (borrar remoto)
git remote prune origin (cuando da error al borrar en remoto)

### unir ramas en modo Automaticamente
(estando en master)
git merge rama-villanos

### union manual con conflictos
(en master)
git merge rama-conflicto
(quitamos el HEAD == y >>)

## TAGS - ETIQUETAS -- son una referencia a un commit especifico
### crear tag
git tag superRelease
git tag -a v1.0.0 -m "Versión 1.0.0" (Con anotación y comentario)
git tag -a v0.1.0 345d7de -m "Versión alfa" (tag en un commit)

### ver tags
git tag
git show v1.0.0

### borrar tags 
git tag -d superRelease

### subir tag a repositorio remoto
git push --tags

## STASH -- Caja donde almacenar todos los cambios temporales que aún no queremos aunar a la rama master
### salvar directorio o crear stash
git stash
git stash save
git stash save "Agregamos a loki" (stash con mensajes que apareceran en el list)

### ver working process (WIP) o stashs
git stash list
git stash list --stat (más información de las entradas del stash)
git show stash (información detallada de los cambios por lineas)
git show stash@{1}

### recuperar cambios del Stash
git stash pop (restaura el último stash y lo elimina)
git stash apply (Restaura el último registro en el stash)
git stash apply stash@{1} (recuperar stash indicando que stash)
git stash save --keep-index (Guarda todo menos los archivos en el stage)
git stash save --include-untracked (Incluye todos los archivos, junto a los que git no le da seguimiento)

### recuperar cambios del Stash con conflicto
git stash pop (nos dará el conflicto)
(salvamos los cambios en los archivos)
git stash drop

### eliminar stash
git stash drop (elimina el primer stash, posición 0)
git stash@{1} drop

### borra todas las entradas en el stash
git stash clear

## REBASE -- Añade los cambios de la rama seleccionada a un area temporal, mueve la rama por delante del ultimo commit de la rama master y añade nuevamente los cambios a su rama.
git checkout rama-misiones (nos movemos a la rama deseada)
git rebase master
git rebase -i HEAD~3 (poner los commits indicados en un area temporal y despues añadirlos de nuevo en el orden almacenado)
### rebase squash -- Chocar
git rebase -i HEAD~4

### rebase reword -- Utilizar rebase para modificar comentarios
git rebase -i HEAD~1
(cambiar pick por reword)
git checkout master

### rebase edit
git checkout -- nombreArchivo (devuelve el archivo a su estado anterior)
git rebase -i HEAD~2
(sustituimos pick por edit)
git reset HEAD^ (un paso atras, antes del último commit)
git add README.md
git commit -m "Actualizaciones al README"
git commit -am "Agregamos a Deadshot"
git rebase --continue

## GITHUB
### añadir repositorio
git remote add <nombre origin> <url .git>

### ver versión remote (nos saldra el nombre origin)
git remote -v 

### subir al repositorio
git push -u origin master (la -u sirve para asginar el repositorio por defecto)

### clonar repositorio
git clone <url repositorio>
git clone <url git remote> demo-10

### Diferencia entre fetch y pull
* pull, intenta descargar los cambios y automáticamente realizar un merge
git pull 
* fetch, intenta descargar los cambios sin realizar un merge
git fetch
(despues del git fetch)
git pull (si despues de hacer el git fetch, hacemos git pull, y no hay errores, quiere decir que no había conflictos de código)
git push

## Fork, clone, Colaboraciones
1. Fork. Tomar repositorio original y clonarlo a un lugar donde tenemos total acceso.
2. Clone. 
3. Colaboraciones. 

 git remote add upstream <url git remote>

### Trabajar en grupo
git checkout -b rama-villanos
git add .
git commit -m "Agregamos el archivo de villanos"
git push origin rama-villanos
(pull request desde github)
git branch -D rama-villanos

### explicación versiones
v1.0.0 
Mayor.menor.parche

V1.0.0

### Release vs TAGs
1. El Release nos permite compartir archivos binarios y podemos proveer una información adicional del uso del Release

## ISSUES
### commit para la issues
git commit -am "Agregamos a Nick fixes #4" (fixes, closes, resolve)

## Milestones - Son grupos de issues, caracteristicas o una fecha importante dentro de un periodo de tiempo
Ejemplo, Milestones Beta Launch, Milestones Octubre...

