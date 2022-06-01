# Commandes du terminal de Bash

- `cd`

la commande `cd` pour *change directory*.
Permet de se déplacer entre les dossiers.

````bash
cd nomDuDossier
// sortir du dossier
cd ..
````

il est possible d'utiliser la touche `tab` pour aller plus vite lors de frappe de la commande, il faut un minimum des 2 premières lettre du dossier.

````bash
cd no + tab
# tab affichera le reste soit: mDuDossier
````

- `pwd`

Cette commande permet d'afficher le chemin complet du dossier dans lequel vous êtes.

Si le chemin est très grand, il sera tronqué, on peut y remedier grâce à une option.

````bash
pwd -P
````

- `ls`
  
affiche les dossiers et les fichiers présent.

- `man`
  
`man + NomDeLaCommande` affiche la doc de la commande.

````bash
man ls
````

- `mkdir`
  
(Make Directory) création d'un dossier.

````bash
mkdir monDossier
````

- `rmdir`
  
(Remouve Directory) supprime le dossier, celui-ci doit être vide.
En ajoutant l'option `-r` supprime tout.

````bash
rmdir monDossier
# option
rmdir -r monDossier
````

- `touch`
création d'un fichier.

````bash
touch monFichier
````

- `rm`

supprime le fichier.

````bash
rm monFichier
````

- `mv`
Déplace un fichier, ou le renomme.

````bash
mv monfichier [destination]
# renommé
mv monfichier myFile
````

- `option`
Permet de voir la doc de la commande.

````bash
ls -option
````

- `code`
permet d'ouvrir VsCode avec l'option de `.` on l'ouvre à partir du dossier courrant.

````bash
code
# option
code .
````

- `ctrl + l`
  permet de nettoyer l'écran du terminal.
