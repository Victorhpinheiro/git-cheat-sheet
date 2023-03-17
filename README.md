# git-cheat-sheet

Traduzido do cheat sheet do Mosh

Original:
```
https://programmingwithmosh.com/wp-content/uploads/2020/09/Git-Cheat-Sheet.pdf
```

# Criando Snapshots

### Inializando um repositório
```
git init
```

### Staging Arquivos
```
git add file1.js           # Stages um arquivo único
git add file1.js file2.js  # Stages multiplo arquivos
git add *.js               # Stages com um padrão
git add .                  # Stages o diretório atual e todos os arquivos dentro recursivamente
```

### Vendo o status
```
git status            # Todos os status
git status -s         # Versão resumida
```

### Commiting os arquivos que estão no stage
```
git commit -m "message"    # Commit com uma messagem de uma linha
git commit                 # Abre o default editor para uma mensagem longa
```

### Pulando a staging area
```
git commit -am "message"
```

### Removendo arquivos
```
git rm file1.js          # Remove do working directory e da staging area
git rm --cached file.js  # Remove da staging area somente
```

### Renomear ou mover files
```
git mv file1.js file1.txt
```

### Ver as mudanças do staging e unstaged
```
git diff              # Mosta as mudanças que não estao no staging
git diff --staged     # Mostra mudanças dentro do stage com o ultimo commit
git diff --cached     # Mesmo que o de cima
```

### Vendo a historia
```
git log              # toda a história
git log --oneline    # Resumo
git log --reverse    # Lista os commits do mais antigo ao mais novo
```

### Vendo um commit
```
git show 921a2ff       # Mostra o commit individual
git show HEAD          # Mostra o ultimo commit
git show HEAD~2        # Mostra o commit 2 passos atrás do atual
git show HEAD:file.js  # Mostra a versão do arquivo file.js no commit mais atual
```

### Removendo arquivo da Staging area
```
git restore --staged file.js  # Copia a última versão do file.js para o index
```

### Descartando mudanças locais
```
git restore file.js             # Copia file.js da staging area para o working directory
git restore file1.js file2.js   # Restora varios arquivos do working directory
git restore .                   # Discarta todas as mudanças locaiss (exceto arquivos untracked)
git clean -fd                   # Remove todos os arquivos untracked
```

### Restaurando uma versão anterior de um arquivo
```
git restore --source=HEAD~2 file.js
```

---

# Navegando história

### Vendo a história
```
git log --stat   # Mostra a lista de arvivos modificados
git log --patch  # Mostra as mudanças (patches)
```


### Filtrando a história
```
git log -3                        # Mostra as últimas 3 commits
git log --author=“Mosh”
git log --before=“2020-08-17”
git log --after=“one week ago”
git log --grep=“GUI”              # Commits com “GUI” na mensagem
git log -S“GUI”                   # Commits com “GUI” no patches
git log hash1..hash2              # Range de commits
git log file.txt                  # Commits que afetaram o arquivo file.txt
```

### Formatando o log output
```
git log --pretty=format:”%an committed %H”
```


### Criando um alias
```
git config --global alias.lg “log --oneline"
```

### Vendo um commit
```
git show HEAD~2
git show HEAD~2:file1.txt   # Mostra a versão do arquivo que estava nesse commit
```

### Comparando Commits
```
git diff HEAD~2 HEAD             # Mostra as mudanças entre dois commits
git diff HEAD~2 HEAD file.txt    # Mudanças do file.txt somente
```

### Checkando um commit
```
git checkout dad47ed         # Checks out o commit dado
git checkout master          # Checks out a master branch
```

### Achando um commit
```
git bisect start
git bisect bad               # Marca o commit atual como um ruim commit
git bisect good ca49180      # Marca o commit dado como um bom commit
git bisect reset             # Termina a bisect session
```

### Checando contribuidores
```
git shortlog
```

### Vendo a historia de um arquivo
```
git log file.txt             # Mostra os commits que mudaram o file.txt
git log --stat file.txt      # Mostra estatísticas (O número de mudanças) para o file.txt
git log --patch file.txt     # Mostra os patches (mudanças) aplicadas ao file.txt
```

### Achando o author da lina
```
git blame file.txt    # Mostra o author de cada linha do file.txt
```

### Tagging
```
git tag v1.0              # Tags o commit atual como v1.0
git tag v1.0 5e7a828      # Tags um commit antigo commit
git tag                   # Lista todas as tags
git tag -d v1.0           # Deleta a tag dada
```

---

# Branching & Merging

### Managing branches
```
git branch bugfix          # Cria uma nova branch chamada bugfix
git checkout bugfix        # Muda para a branch bugfix
git switch bugfix          # Mesmo que o acima
git switch -C bugfix       # Cria e muda a branch
git branch -d bugfix       # Deleta a bugfix branch
```

### Comparando branches       
```
git log master..bugfix          # Lista os commits na bugfix branch não presentes na master
git diff master..bugfix         # Mostra o resumo de mudanças
```

### Stashing
```
git stash push -m “New tax rules”       # Cria um novo stash
git stash list                          # Lista todos os stashes
git stash show stash@{1}                # Mostra um stash dado
git stash show 1                        # Atalho para stash@{1}
git stash apply 1                       # Aplica o stash dado na working dir
git stash drop 1                        # Deleta um stash dado
git stash clear                         # Deleta todos os stashes
```

### Merging
```
git merge bugfix               # Merge a bugfix branch na branch atual
git merge --no-ff bugfix       # Cria um merge commit mesmo se o fast forward seja possível
git merge --squash bugfix      # Performa um squash merge
git merge --abort              # Aborta a merge
```

### Vendo as merged branches
```
git branch --merged        # Mostra as merged branches
git branch --no-merged     # Mostra as unmerged branches
```

### Rebasing
```
git rebase master            # Muda a base da branch atual
```

### Cherry picking
```
git cherry-pick dad47ed  # Applica o commit dado na branch atual
```

---

# Colaborando

### Clonando um repositório
```
git clone url
```

### Sincronizando com os remotes
```
git fetch origin master     # Fetches master da origin
git fetch origin            # Fetches todos os objetos da origin
git fetch                   # Atalho para “git fetch origin”
git pull                    # Fetch + merge
git push origin master      # Pushes master para origin
git push                    # Atalho para “git push origin master”
```

### Compartilhando tags
```
git push origin v1.0             # Pushes tag v1.0 para origin
git push origin —delete v1.0
```

### Compartilhando branches
```
git branch -r                # Mostra remote tracking branches
git branch -vv               # Mostra local & remote tracking branches
git push -u origin bugfix    # Pushes bugfix para origin
git push -d origin bugfix    # Remove bugfix da origin
```

### Gerenciando remotes  
```
git remote                     # Mostra remote repos
git remote add upstream url    # Adiciona um novo remote chamado upstream
git remote rm upstream         # Remove upstream
```
---

# Reescrevendo História

### Desfazendo commits
```
git reset --soft HEAD^        # Remove o último commit, mantém mudado no stage
git reset --mixed HEAD^       # Unstages as mudanças também
git reset --hard HEAD^        # Discarta as mudanças locais
```

### Revertendo commits
```
git revert 72856ea                 # Reverte o commit dado
git revert HEAD~3..                # Reverte os últimos 3 commits
git revert --no-commit HEAD~3..
```

### Recuperando um commit perdido
```
git reflog                  # Mostra a história do HEAD
git reflog show bugfix      # Mostra a história do bugfix pointer
```

### Amending o último commit
```
git commit --amend
```

### Interactive rebasing
git rebase -i HEAD~5
