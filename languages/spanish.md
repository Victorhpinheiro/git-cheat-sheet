# git-cheat-sheet

Traducido del cheat sheet de Mosh

Original:
```
https://programmingwithmosh.com/wp-content/uploads/2020/09/Git-Cheat-Sheet.pdf
```

Otros Idiomas:
- [Portugués](../README.md)

# Creación de Snapshots

### Creación de un repositorio
```
git init
```

### Agregar archivos al area de preparación (Staging Area)
```
git add file1.js           # Agrega un solo archivo
git add file1.js file2.js  # Agrega multiples archivos
git add *.js               # Agrega con un patrón (todos los archivos con extensión ".js")
git add .                  # Agrega el directorio actual y todos los archivos dentro recursivamente
```

### Revisar el estado actual (Status)
```
git status            # Todos los status
git status -s         # Versión resumida
```

### Confirmar (Commit) los archivos del area de preparación
```
git commit -m "message"    # Commit con un mensaje de una línea
git commit                 # Abre el default editor para un mensaje largo
```

### Saltarse el área de preparación
```
git commit -am "message"
```

### Eliminando (Remove) archivos
```
git rm file1.js          # Remove del working directory y de la staging area
git rm --cached file.js  # Remove del staging area solamente
```

### Renombrar o mover archivos
```
git mv file1.js file1.txt
```

### Ver cambios del staging y unstaged
```
git diff              # Muestra los cambios que no estan en el staging
git diff --staged     # Muestra los cambios dentro del stage con el ultimo commit
git diff --cached     # Lo mismo que arriba
```

### Revisar la historia
```
git log              # toda la historia
git log --oneline    # Resumen
git log --reverse    # Lista de los commits de mas antiguo a mas nuevo
```

### Revisar un commit
```
git show 921a2ff       # Muestra un commit individual
git show HEAD          # Muestra el ultimo commit
git show HEAD~2        # Muestra un commit 2 pasos atrás del atual
git show HEAD:file.js  # Muestra la versión del archivo file.js en el commit mas actual
```

### Remover un archivo de la Staging Area
```
git restore --staged file.js
```

### Descartando cambios locales
```
git restore file.js             # Restaura un archivo
git restore file1.js file2.js   # Restaura varios archivos
git restore .                   # Descarta los cambios realizados en todos los archivos del directorio actual (excepto archivos untracked)
git clean -fd                   # Elimina todos los archivos untracked
```

### Restaurar una versión anterior de un archivo
```
git restore --source=HEAD~2 file.js
```

---

# Navegando la historia

### Revisar la historia
```
git log --stat   # Muestra la lista de archivos modificados
git log --patch  # Muestra los cambios (patches)
```


### Filtrando la historia
```
git log -3                        # Muestra los últimos 3 commits
git log --author=“Mosh”
git log --before=“2020-08-17”
git log --after=“one week ago”
git log --grep=“GUI”              # Commits con “GUI” en el mensaje
git log -S“GUI”                   # Commits con “GUI” en el patch
git log hash1..hash2              # Range de commits
git log file.txt                  # Commits que afectaron el archivo file.txt
```

### Formateo del log output
```
git log --pretty=format:”%an committed %H”
```


### Creacion de un alias
```
git config --global alias.lg “log --oneline"
```

### Revisar un commit
```
git show HEAD~2
git show HEAD~2:file1.txt   # Muestra la versión del archivo que estaba en ese commit
```

### Comparando Commits
```
git diff HEAD~2 HEAD             # Muestra los cambios entre dos commits
git diff HEAD~2 HEAD file.txt    # Cambios de file.txt solamente
```

### Checkeando un commit
```
git checkout dad47ed         # Checks out el commit dado
git checkout master          # Checks out la master branch
```

### Encontrar un commit
```
git bisect start
git bisect bad               # Marca el commit actual como un commit malo
git bisect good ca49180      # Marca el commit dado como un buen commit
git bisect reset             # Termina a bisect session
```

### Revisar Contribuyentes
```
git shortlog
```

### Revisar la historia de un archivo
```
git log file.txt             # Muestra los commits que cambiaron el file.txt
git log --stat file.txt      # Muestra estadísticas (el número de cambios) para el file.txt
git log --patch file.txt     # Muestra los patches (cambios) aplicados al file.txt
```

### Encontrar el autor de una linea
```
git blame file.txt    # Mostrar el autor de cada línea en el archivo .txt
```

### Tagging
```
git tag v1.0              # Tags el commit actual como v1.0
git tag v1.0 5e7a828      # Tags un commit antigo
git tag                   # Lista de todas las tags
git tag -d v1.0           # Elimina laa tag dada
```

---

# Branching & Merging

### Managing branches
```
git branch bugfix          # Crea una nueva branch llamada bugfix
git checkout bugfix        # Check out para la branch bugfix
git switch bugfix          # Mismo que arriba
git switch -C bugfix       # Crae y cambia la branch 
git branch -d bugfix       # Elimina la bugfix branch
```

### Comparando branches       
```
git log master..bugfix          # Lista de los commits en la bugfix branch no presentes en la master
git diff master..bugfix         # Mostrar el resumen de cambios
```

### Stashing
```
git stash push -m “New tax rules”       # Crea un nuevo stash
git stash list                          # Lista todos los stashes
git stash show stash@{1}                # Muestra un stash dado
git stash show 1                        # Atajo para stash@{1}
git stash apply 1                       # Aplica el stash dado en el working dir
git stash drop 1                        # Elimina un stash dado
git stash clear                         # Elimina todos los stashes
```

### Merging
```
git merge bugfix               # Merge un bugfix branch en la branch actual
git merge --no-ff bugfix       # Crea un merge commit incluso si el fast forward es posible
git merge --squash bugfix      # Hace um squash merge
git merge --abort              # Aborta el merge
```

### Revisar las merged branches
```
git branch --merged        # Muestra las merged branches
git branch --no-merged     # Muestra las unmerged branches
```

### Rebasing
```
git rebase master            # Cambia la base de la branch atual
```

### Cherry picking
```
git cherry-pick dad47ed  # Applica el commit dado en la branch atual
```

---

# Colaborando

### Clonando un repositorio
```
git clone url
```

### Sincronizando con los remotes
```
git fetch origin master     # Fetches master de origin
git fetch origin            # Fetches todos los objetos de origin
git fetch                   # Atajo para “git fetch origin”
git pull                    # Fetch + merge
git push origin master      # Pushes master para origin
git push                    # Atajo para “git push origin master”
```

### Compartir tags
```
git push origin v1.0             # Pushes tag v1.0 para origin
git push origin —delete v1.0
```

### Compartir branches
```
git branch -r                # Muestra remote tracking branches
git branch -vv               # Muestra local & remote tracking branches
git push -u origin bugfix    # Pushes bugfix para origin
git push -d origin bugfix    # Remove bugfix de origin
```

### Manejando remotes  
```
git remote                     # Muestra remote repos
git remote add upstream url    # Adiciona un nuevo remote llamado upstream
git remote rm upstream         # Remove upstream
```
---

# Reescribiendo la historia

### Deshaciendo commits
```
git reset --soft HEAD^        # Remueve el último commit, mantiene cambiado en el stage
git reset --mixed HEAD^       # Unstages los cambios também
git reset --hard HEAD^        # Descarta los cambios locales
```

### Revirtendo commits
```
git revert 72856ea                 # Revierte el commit dado
git revert HEAD~3..                # Reverte los últimos 3 commits
git revert --no-commit HEAD~3..
```

### Recuperando un commit perdido
```
git reflog                  # Muestra la historia del HEAD
git reflog show bugfix      # Muestra la historia del bugfix pointer
```

### Amending el último commit
```
git commit --amend
```

### Interactive rebasing
git rebase -i HEAD~5
