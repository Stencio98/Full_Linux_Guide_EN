# GIT DELETE BRANCH
* the following script is made to easyly delete branch in local and remote git repository
```
#!/bin/bash

# Verifica che sia stato passato il nome del ramo
if [ -z "$1" ]; then
    echo "Utilizzo: $0 nome-ramo"
    exit 1
fi

BRANCH="$1"

echo "Eliminazione del ramo: $BRANCH"

# Elimina il ramo locale
git branch -d "$BRANCH" || exit 1

# Elimina il ramo remoto
git push origin --delete "$BRANCH" || exit 1

# Aggiorna i riferimenti ai rami remoti
git fetch --prune

echo "Ramo $BRANCH eliminato correttamente."
```
* the script is saved in home/user folder like .bashrc, to run it easyly it's better build an alias that can be lanuched in git folder
```
alias deletebranch='sh /....home/user/delete_branch.sh'
```
