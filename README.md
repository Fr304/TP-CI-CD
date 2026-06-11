# TP-CI-CD

## Exercice 1 - Premier contact
### Objectif : Mettre en place l’environnement de travail et exécuter son tout premier workflow.

Pour commencer cet exercice, je vais installer Git sur ma machine, pour cela, je vais utiliser les commandes suivantes :

```bash
sudo apt update
sudo apt install git -y
```

Ensuite j'ai configuré mon identité nom + adresse mail et ensuite je vais récupérer le dépôt que j'ai créé :

```bash
git clone https://github.com/allaouifrd-png/TP-CI-CD.git
cd TP-CI-CD
```

Ensuite, grâce à ces commandes, je vais vérifier que mon dépôt est bien téléchargé

```bash
pwd
```

```bash
ls -la
```

```bash
git status
```

```bash
ubuntu@ubuntu-devsecops:~/TP-CI-CD$ git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

Ensuite, je vais créer un dossier spécial GitHub Actions

```bash
mkdir -p .github/workflows
```

Dans ce dossier, je vais créer mon premier Workflow :

```bash
nano .github/workflows/bonjour.yml
```

Ci-dessous le contenu de ce workflow : 

```bash
name: Bonjour

on: push

jobs:
  dire-bonjour:
    runs-on: ubuntu-latest

    steps:
      - name: Afficher un message
        run: echo "Bonjour depuis GitHub Actions !"
```

Ci-dessous, la signification de chaque intitulé : 

**name: Bonjour :** c’est le nom visible dans l’onglet Actions de GitHub. </br>
**on: push :** le workflow se lance à chaque fois que j'envoie du code avec git push. </br>
**jobs:** : un workflow contient un ou plusieurs jobs. </br>
**dire-bonjour:** : c’est le nom du job. </br>
**runs-on: ubuntu-latest :** GitHub va lancer une machine Ubuntu temporaire pour exécuter le job. </br>
**steps:** : ce sont les étapes exécutées dans le job. </br>
**run:** : exécute une commande shell Linux. </br>

Ensuite, je vais envoyer mon Workflow sur Github : 

```bash
git status
git add .github/workflows/bonjour.yml
git commit -m "Ajout du premier workflow GitHub Actions"
git push origin main
```

Ci-dessous, l'explication de chaque commande : 

**git status :** affiche l’état des fichiers du projet </br>
**git add .github/workflows/bonjour.yml :** prépare le fichier bonjour.yml pour le prochain commit </br>
**git commit -m "Ajout du premier workflow GitHub Actions" :** enregistre cette modification avec un message </br>
**git push origin main :**  envoie le commit sur GitHub dans la branche main </br>

Après le push, sur mon repo Git, je vois le Workflow nommé Bonjour précédemment créé et en cliquant sur le job dire-bonjour dans les logs je vois "**Bonjour depuis GitHub Actions**"

La coche verte indique que le Workflow fonctionne sans problème 
