# TP2 - GitHub Centralisé avec Hello World en Java

## Informations
- Langage : Java
- OS : Windows (Git Bash)
- Dépôt : https://github.com/steavenspr/tp2-github-centralise-steavens

---

## Objectifs

- Créer un dépôt GitHub distant
- Cloner un dépôt sur sa machine
- Créer et modifier un fichier source Java
- Enregistrer les versions avec Git
- Ajouter des tags de version
- Créer une branche
- Fusionner une branche dans la branche principale
- Mettre à jour le dépôt GitHub

---

## Etape 1 - Créer le dépôt sur GitHub

1. Aller sur github.com et se connecter
2. Cliquer sur "New repository"
3. Remplir les champs :
   - Nom : `tp2-github-centralise-nom-prenom`
   - Public ou Private selon consigne
   - Ne cocher aucune option (pas de README, pas de .gitignore, pas de licence)
4. Cliquer sur "Create repository"

---

## Etape 2 - Cloner le dépôt en local

```bash
git clone https://github.com/steavenspr/tp2-github-centralise-steavens.git
cd tp2-github-centralise-steavens
git status
git remote -v
```

Créer le .gitignore pour ignorer le dossier IntelliJ :

```bash
echo ".idea/" >> .gitignore
git status
```

---

## Etape 3 - Créer le programme Hello World

```bash
cat > Main.java << 'EOF'
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
EOF
```

```bash
git status
git diff
```

---

## Etape 4 - Premier commit et tag v1.0

```bash
git add .
git commit -m "v1.0 - creation du programme Hello World"
git tag v1.0
git log --oneline
```

Résultat attendu :
```
31f977c (HEAD -> main, tag: v1.0) v1.0 - creation du programme Hello World
```

---

## Etape 5 - Publier sur GitHub

```bash
git push -u origin main
git push origin v1.0
```

---

## Etape 6 - Version 1.1

```bash
cat > Main.java << 'EOF'
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World");
        System.out.println("Version 1.1");
    }
}
EOF
```

```bash
git add .
git commit -m "v1.1 - ajout d un deuxieme affichage"
git tag v1.1
git push
git push origin v1.1
```

---

## Etape 7 - Version 1.2

```bash
cat > Main.java << 'EOF'
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World");
        System.out.println("Version 1.1");
        System.out.println("Version 1.2");
    }
}
EOF
```

```bash
git add .
git commit -m "v1.2 - ajout d un troisieme affichage"
git tag v1.2
git push
git push origin v1.2
```

---

## Etape 8 - Créer la branche feature-affichage

```bash
git checkout -b feature-affichage
git branch
```

Résultat attendu :
```
* feature-affichage
  main
```

---

## Etape 9 - Modifier le programme dans la branche

```bash
cat > Main.java << 'EOF'
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World");
        System.out.println("Version 1.1");
        System.out.println("Version 1.2");
        System.out.println("Travail sur branche feature");
    }
}
EOF
```

```bash
git add .
git commit -m "feature - ajout d'un affichage sur la branche feature"
git push -u origin feature-affichage
git log --oneline
```

---

## Etape 10 - Revenir sur la branche principale

```bash
git checkout main
git branch
```

En revenant sur main, le fichier Main.java revient automatiquement à la version sans la ligne "Travail sur branche feature". Git gère seul les différentes versions selon la branche active.

---

## Etape 11 - Fusionner la branche feature dans main

```bash
git merge feature-affichage
git tag v2.0
git push
git push origin v2.0
git log --oneline
```

---

## Etape 12 - Vérifications finales

```bash
git branch
git tag
git log --oneline --decorate --graph --all
```

Résultat final :

Branches :
```
  feature-affichage
* main
```

Tags :
```
v1.0
v1.1
v1.2
v2.0
```

Historique :
```
* e024791 (HEAD -> main, tag: v2.0) feature - ajout d'un affichage sur la branche feature
* d476d74 (tag: v1.2)               v1.2 - ajout d un troisieme affichage
* 22c995e (tag: v1.1)               v1.1 - ajout du deuxieme affichage
* 31f977c (tag: v1.0)               v1.0 - creation du programme HELLO WORLD
```

---

## Récapitulatif des commandes utilisées

| Commande | Description |
|---|---|
| `git clone <url>` | Télécharger un dépôt GitHub en local |
| `git status` | Voir l'état des fichiers |
| `git diff` | Voir les modifications non enregistrées |
| `git add .` | Préparer tous les fichiers pour le commit |
| `git commit -m "message"` | Sauvegarder une version avec un message |
| `git tag v1.0` | Marquer une version |
| `git push` | Envoyer les commits sur GitHub |
| `git push origin v1.0` | Envoyer un tag sur GitHub |
| `git log --oneline` | Voir l'historique des commits |
| `git checkout -b feature` | Créer une branche et basculer dessus |
| `git checkout main` | Revenir sur la branche principale |
| `git branch` | Lister les branches |
| `git merge feature` | Fusionner une branche dans la branche actuelle |
| `git remote -v` | Vérifier le dépôt distant |

---

## Workflow Git de base

```
1. Modifier le code
2. git add .          -> préparer les fichiers
3. git commit -m      -> sauvegarder la version
4. git tag            -> marquer la version
5. git push           -> envoyer sur GitHub
```
