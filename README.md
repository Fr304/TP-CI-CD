# TP-CI-CD

## Exercice 1 - Premier contact

**Objectif** : mettre en place l’environnement de travail et exécuter son tout premier workflow GitHub Actions.

Pour commencer cet exercice, je vais installer Git sur ma machine avec les commandes suivantes :

```bash
sudo apt update
sudo apt install git -y
```
Ensuite, je configure mon identité Git avec mon nom et mon adresse mail :

```bash
git config --global user.name "Fr304"
git config --global user.email "mon-adresse-mail@example.com"
```
Ensuite, je récupère le dépôt GitHub que j’ai créé :

```bash
git clone https://github.com/Fr304/TP-CI-CD.git
cd TP-CI-CD
```
Ensuite, grâce à ces commandes, je vérifie que mon dépôt est bien téléchargé :

```bash
pwd
ls -la
git status
```
Exemple de résultat attendu avec git status :

```bash
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```
Ensuite, je crée un dossier spécial pour GitHub Actions :

```bash
mkdir -p .github/workflows
```

Dans ce dossier, je crée mon premier workflow :

```bash
nano .github/workflows/bonjour.yml
```

Ci-dessous le contenu de ce workflow :

```bash
name: Bonjour

on:
  push:
  workflow_dispatch:

jobs:
  dire-bonjour:
    runs-on: ubuntu-latest

    steps:
      - name: Afficher un message
        run: echo "Bonjour depuis GitHub Actions !"
```

Ci-dessous, la signification de chaque intitulé :

**name: Bonjour** : C’est le nom visible dans l’onglet Actions de GitHub.

**on: </br>
  push:** </br>
Le workflow se lance automatiquement à chaque fois que j’envoie du code avec git push.

**workflow_dispatch:** Cela permet aussi de lancer le workflow manuellement depuis GitHub ou avec la commande gh workflow run.

**jobs:** Un workflow contient un ou plusieurs jobs.

**dire-bonjour:** C’est le nom du job.

**runs-on: ubuntu-latest** : GitHub va lancer une machine Ubuntu temporaire pour exécuter le job.

**steps:** : Ce sont les étapes exécutées dans le job.

**run:** Exécute une commande shell Linux.

Ensuite, j’envoie mon workflow sur GitHub :

```bash
git status
git add .github/workflows/bonjour.yml
git commit -m "Ajout du premier workflow GitHub Actions"
git push origin main
```

Ci-dessous, l’explication de chaque commande :

**git status** Affiche l’état des fichiers du projet. </br>

**git add .github/workflows/bonjour.yml** : Prépare le fichier bonjour.yml pour le prochain commit. </br>

**git commit -m "Ajout du premier workflow GitHub Actions"** Enregistre cette modification avec un message de commit. </br>

**git push origin main** : Envoie le commit sur GitHub dans la branche main. </br>

Après le push, sur mon dépôt GitHub, je vais dans l’onglet Actions. Je vois le workflow nommé Bonjour.

En cliquant sur le job dire-bonjour, je peux consulter les logs et voir le message suivant :

Bonjour depuis GitHub Actions !

La coche verte indique que le workflow fonctionne sans problème.

<img width="1900" height="793" alt="image" src="https://github.com/user-attachments/assets/f1c450a2-784d-4a5f-95b4-a8499073f60a" />

## Exercice 2 - Anatomie d’un fichier de workflow

**Objectif** : Comprendre la structure d’un fichier YAML de workflow et savoir nommer chacune de ses parties.

Pour cette exercie, dans le répertoire "TP-CI-CD" 

```bash
ubuntu@ubuntu-devsecops:~/TP-CI-CD$ pwd
/home/ubuntu/TP-CI-CD
ubuntu@ubuntu-devsecops:~/TP-CI-CD$ git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
ubuntu@ubuntu-devsecops:~/TP-CI-CD$ 
```

Le fichier .github/workflows est bien présent : 

```bash
ubuntu@ubuntu-devsecops:~/TP-CI-CD$ ls -la .github/workflows
total 12
drwxrwxr-x 2 ubuntu ubuntu 4096 juin  11 12:22 .
drwxrwxr-x 3 ubuntu ubuntu 4096 juin  11 11:51 ..
-rw-rw-r-- 1 ubuntu ubuntu  196 juin  11 12:22 bonjour.yml
ubuntu@ubuntu-devsecops:~/TP-CI-CD$ 
```
Avec le contenu que j'ai spécifié dans le précédent exercice : 

```bash
ubuntu@ubuntu-devsecops:~/TP-CI-CD$ cat .github/workflows/bonjour.yml
name: Bonjour

on:
  push:
  workflow_dispatch:

jobs:
  dire-bonjour:
    runs-on: ubuntu-latest

    steps:
      - name: Afficher un message
        run: echo "Bonjour depuis GitHub Actions !"
ubuntu@ubuntu-devsecops:~/TP-CI-CD$ 
```
Je vais donc editer ce fichier et y renseigner le contenu suivant : 

```bash
name: Workflow d'initiation

on: push

jobs:
  saluer-le-monde:
    runs-on: ubuntu-latest

    steps:
      - name: Afficher un message de bienvenue
        run: echo "Bonjour depuis GitHub Actions !"

      - name: Afficher la date du jour
        run: date

      - name: Afficher l'utilisateur GitHub qui a lancé le workflow
        run: echo "Workflow lancé par ${{ github.actor }}"
```
