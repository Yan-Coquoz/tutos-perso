# Windows 10  en UTF-8

## Postgresql

tuto d'installation de Postgresql [ICI](https://medium.com/@aeadedoyin/getting-started-with-postgresql-on-windows-201906131300-ee75f066df78)
version 10 de PG.
mettre cette ligne a la place de celle du site pour l'installation.

````bash
choco install postgresql13 --params '/Password:mot_de_passe' -y
````

et faire attention dans la configuration pour `les variables d'envionnement`. Bien mettre la `13` et pas `10` selon la version actuel de postgresql.

## UTF-8

- lancer cmd.exe en admin.
- faire `intl.cpl`

une fenêtre s'ouvre.

---

- Dans l'onglet `administation`
- faire `Modifier les paramètres régionaux...`

une nouvelle fenêtre

---

- selectionner la langue et le pays.
- et l'option Bêta : Utiliser le format Unicode UTF-8 pour une prise en charge des langues à l'échelle mondiale
- `OK`

Un redémarrage est obligatoire!

- Pour que la BDD soit aussi en UTF-8 il faut simplement la réinstaller.

````sql
psql -U trombiuser -d trombi
trombi=> \i data/create_db.sql
````

Pas besoin de créé un nouveau ROLE ou une nouvelle DATABASE.
