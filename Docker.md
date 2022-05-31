
# Docker pour le dev tous les jours, tout le temps

Spoilers : c'est bien !

===

## Problématiques

Les développeurs ont besoin d'un "environnement" de travail.

Cet environnement doit être :

- **Indépendant** de l'hôte, car un dev ne choisi pas toujours la machine sur laquelle il travaille ni sont O.S.
- **Isolé**, pour pouvoir travailler avec plusieurs outils et différentes versions sur différents projets.
- **Reproduisible**, pour que tout les membre de l'équipe ai le même.
- **Souple** mais **fiable** et **performant**, pour coller aux besoins du travail quotidiens sans être une contrainte.

---

Docker est là pour répondre à chacune de ces problématiques

===

## Théorie

> Il ne s'agit pas de virtualisation, mais de conteneurisation, une forme plus légère qui s'appuie sur certaines parties de la machine hôte pour son fonctionnement. Cette approche permet d'accroître la flexibilité et la portabilité d’exécution d'une application, laquelle va pouvoir tourner de façon fiable et prévisible sur une grande variété de machines hôtes, que ce soit sur la machine locale, un cloud privé ou public, une machine nue, etc...

TL ; DR

---

## Docker c'est

Une **architecture** multi services transformée en fichiers.

Chargée et manipulée à l'aide d'une super commande `docker-compose`.

---

## Vocabulaire

Un **service** : C'est une instance d'un programme (PHP, Nginx, PostgreSQL, Node, Crossbar...).

Une **image** : Une structure qui décrit un service et son environnement (O.S., dossiers, configuration...).

Un **container** : Un processus sur notre machine, basé sur une image.

---

En gros :

> Un **service** est décrit par une **image**, pour utiliser le **service** on créé un **container** à partir de l'**image**.

> Les **images** persistent tandis que les containers peuvent être remplacé / redémarré au besoin.

---

## Du coup pour le dev

Les fichiers décrivant l'architecture sont ajouté dans le projet. Le tout peut se lancer facilement sur tous les postes de l'équipe quel que soit leur hôte.

(**Indépendance** et **Reproductibilité**)

Les dépendances / versions des outils sont liés aux projets directement donc
on peut rajouter très simplement, sans impact sur l'hôte, un nouvel outil ou changer de version

(**Isolation**)

===

## L'architecture

*Comment on déclare et organise nos services.*

---

## docker-compose.yml

*One file to rule them all.*

C'est dans ce fichier que l'on déclare la liste des services et leurs paramétrages.

---

### Architecture "FSJS"

`docker-compose.yml`

```yaml
version: "3.7" # <- Ligne obligatoire (le numéro de version peut évoluer par contre)
services: # <- on va décrire la liste des services
    nodejs: # <- Je déclare un service "nodejs" #michelisable
        # Ce qui suit est la "configuration" de ce service
        build: ./docker/node

        volumes:
            - ".:/var/app"
        ports:
            - "3000:3000"
    bdd: # <- Je déclare un autre service "bdd" pour... ma base de données
        image: "postgres:12-alpine"
        environment:
            POSTGRES_PASSWORD: "postgres"
            POSTGRES_USER: "postgres"
```

---

### L'utilisation

Il y a **1** commande avec des sous commandes simple (comme pour `git`):

```bash
docker-compose up # Lance tous les services (créé et lance les containers)
docker-compose down # Coupe tous les services et supprime les containers
docker-compose logs nomservice # Affiche les logs du service
docker-compose exec nomservice sh # Ouvre un terminal dans le service
```

---

### Les services (nodejs / bdd)

Une entrée par service.

Le nom est libre il sert de référence pour la commande `docker-compose` et de nom machine pour les communications réseaux inter service.

*Donc si mon code dans mon service `nodejs` à besoin de se connecter au service `bdd` la connexion string ressemblera à `postgres://user@bdd/nomDeBase`*

===

## Les images

<pre>
Ex :
<code class="language-yaml hljs" data-line-numbers="3">...
bdd: # <- Je déclare un service "bdd" pour... ma base de données
    image: "postgres:12-alpine" # <- l'image à utiliser pour mon service
    environment:
        POSTGRES_PASSWORD: "postgres"
        POSTGRES_USER: "postgres"
</code></pre>

---

La communauté ou l'éditeur de chaque outil (NodeJS, PostGres, NGINX, Crossbar, Sentry)
fournit une image officielle à utiliser.

Par défaut, les images sont récupérées sur `https://hub.docker.com`. Leur documentation si trouve aussi.

Elles sont sous la forme `service:tag-option`, par ex : `postgres:12-alpine`

---

**service** : Le nom du service en question (postgres dans l'exemple)

**tag** : Généralement la version du service (ici la v12)

**option** : Sert souvent à définir quel est le "système de base" de l'image. `alpine` fait référence à une distribution Linux ultra light (~5 Mo).

La liste des `tag-option` pour un service est disponible dans la documentation de l'image.

---

### Le réseau

Chaque service peut voir les machines correspondantes aux autres service
(si elle n'ont pas été isolé via l'option `networks`).

On peut NAT (faire correspondre) un port d'un container avec un de l'hôte via l'option `ports`.

---

<pre>
Ex :
<code class="language-yaml hljs" data-line-numbers="7,8">...
nodejs:
    build: ./docker/node
    volumes:
        - ".:/var/app"
    ports: # <- Le routing des ports
        - "80:3000"
</code></pre>

*Les requêtes pour localhost:80 sont transférées sur le port 3000 du container*

---

### La configuration

*Ok maintenant que j'ai une image, comment je la fais coller à mes besoins ?*

Deux options s'offrent à moi.

---

Via les **variables d'environnements** :

<pre>
Ex :
<code class="language-yaml hljs" data-line-numbers="4-6">...
    bdd:
        image: "postgres:12-alpine"
        environment: # <- section des variables d'environnements
            POSTGRES_PASSWORD: "0"
            POSTGRES_USER: "prof"
</code></pre>

*Ici on définit le superuser du service PostGres et sont mot de passe*

---

On pourrait aussi utiliser l'option `env_file` et spécifier un fichier.

C'est particulièrement utile lorsque l'ont veut que plusieurs services partagent des variables d'environnements.

---

Via le **partage de fichier** :

Docker permet très facilement de partager un dossier (et ses fichiers) entre l'hôte et un container.

On parle de "monter" (dans le sens de la commande `mount` Unix) des **volumes**.

---

On peut par exemple  :

- Avoir notre IDE et écrire notre code dans l'hôte et partager les fichiers avec un container qui fait tourner node
- Enregistrer des fichiers de configuration (le fameux `pg_hba.conf` par exemple) dans notre projet et les charger directement
- Sauvegarder l'état d'une base de données indépendamment de la vie du container

---

<pre>
Ex :
<code class="language-yaml hljs" data-line-numbers="4-5">...
nodejs:
    build: ./docker/node
    volumes:
        - ".:/var/app"
    ports:
        - "3000:3000"
</code></pre>

*On monte le dossier courant (.) dans le dossier /var/app du container*

---

### Doc

Beaucoup possibilité dans la définition d'un service. Un point de référence, la doc :

<https://docs.docker.com/compose/compose-file/>

===

## Images personnalisées

En général les services applicatifs (ce qui contiendrons notre code) ont besoins d'un peu plus de personnalisation.

Pour ça on peut créer nos propres images.

---

### Dockerfile

Une image c'est un fichier `Dockerfile` qui a été **build**.

---

Pour utiliser une image personnalisé dans une architecture :

Soit on la **build** et on la **push** sur un registry comme hub.docker.com (fonctionnement pour la prod).

Soit on indique le fichier `Dockerfile` dans notre `docker-compose.yml`.

---

On va utiliser l'instruction `build` dans le docker-compose.yml pour indiquer **le dossier contenant** le `Dockerfile`

<pre>
Ex :
<code class="language-yaml hljs" data-line-numbers="3">...
nodejs:
    build: ./docker/node # <- Au lieu de donner une image j'indique un Dockerfile à build
    volumes:
        - ".:/var/app"
    ports:
        - "80:3000"
</code></pre>

---

<pre>
Exemple Dockerfile pour une app générique de dev Node
<code class="language-dockerfile hljs">
FROM node:lts-alpine

RUN mkdir -p /var/app &&\
    npm install -g nodemon

VOLUME /var/app
EXPOSE 3000

WORKDIR /var/app
CMD npm install && npm run dev
</code></pre>

---

On part **toujours** d'une image pré existante avec `FROM`.

<pre><code class="language-dockerfile hljs" data-line-numbers="2">
FROM node:lts-alpine

RUN mkdir -p /var/app &&\
    npm install -g nodemon

VOLUME /var/app
EXPOSE 3000

WORKDIR /var/app
CMD npm install && npm run dev
</code></pre>

---

On éxécute une série de commande avec des `RUN` pour installer des dépendances globales, créer des fichiers / dossiers...

<pre><code class="language-dockerfile hljs" data-line-numbers="4-5">
FROM node:lts-alpine

RUN mkdir -p /var/app &&\
    npm install -g nodemon

VOLUME /var/app
EXPOSE 3000

WORKDIR /var/app
CMD npm install && npm run dev
</code></pre>

---

On définit les points de montage avec `VOLUME` et les ports qui seront accessible avec `EXPOSE`.

<pre><code class="language-dockerfile hljs" data-line-numbers="7-8">
FROM node:lts-alpine

RUN mkdir -p /var/app &&\
    npm install -g nodemon

VOLUME /var/app
EXPOSE 3000

WORKDIR /var/app
CMD npm install && npm run dev
</code></pre>

---

On définit la commande qui sera éxécuté au lancement du container avec `CMD` et le dossier d'éxécution avec `WORKDIR`.

<pre><code class="language-dockerfile hljs" data-line-numbers="12-13">
FROM node:lts-alpine

RUN mkdir -p /var/app &&\
    npm install -g nodemon

VOLUME /var/app
EXPOSE 3000

WORKDIR /var/app
CMD npm install && npm run dev
</code></pre>

*Ces deux commandes sont surchargeasse avec `command` et `working_dir`, directement
dans le docker-compose.yml.*

---

### Doc

Il existe aussi d'autres instruction pour les fichiers Dockerfile et de la même façon -> RTFM.

<https://docs.docker.com/engine/reference/builder/>

===

## Et en prod ?

> Docker est de moins en moins utilisé en prod... mais de plus en plus en dev...

En faite sous le terme "Docker" se cache plusieurs outils :

- docker-compose
- Un builder d'image
- Un gestionnaire réseaux
- Un système de partage de dossiers
- Un système de création / lancement de containers
- ...

---

En prod on a surtout besoin de faire tourner des containers le reste est superflue...

Cependant les images "build" par Docker suive une norme générique et peuvent être utilisé avec d'autre
système de container !

Pour la prod on créera donc des images spécifique, qui seront éxécuté sous la forme de container par nos serveurs de prod.

Et comme Docker peut faire tourner ces images on peut, depuis notre machine, tester les conditions exactes de la production notre code.

===

### Liste des commandes utiles

Les commande `docker-compose` sont à exécuter dans le dossier du fichier `docker-compose.yml`.

```bash
docker-compose up # Lance toute l'architecture, interruptible avec Ctrl-c
docker-compose up --build # Idem en forçant le rebuild des images locale
docker-compose up --detach # Detache l'éxécution de la console courante
docker-compose up nodejs # Ne lance que le service nodejs
docker-compose down # Coupe et supprime tous les containers
docker-compose exec nodejs sh # Lance un term. dans le container nodejs
docker-compose logs -f nodejs # Affiche la sortie du container nodejs
```

---

### Liens utiles

- [Liste de samples](https://gitlab.audean.net/maxime/docker-samples/-/tree/master)
- [docker-compose.yml reference](https://docs.docker.com/compose/compose-file/)
- [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
