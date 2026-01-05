# SmartMix — Instructions d’exécution (Pelican / Panel)

Ce README explique **comment installer et exécuter** SmartMix sur ton hébergement (Pelican/Pterodactyl) **sans SSH**, uniquement via le panel.

---

## Pré-requis

- Serveur web déjà fonctionnel (Nginx + PHP-FPM) — dans ton cas c’est OK.
- PHP 8.x (tu es en 8.4).
- Accès au **File Manager** du panel.
- Le dossier racine du site est : **`webroot/`**

---

## 1) Déployer les fichiers (structure obligatoire)

Dans le **File Manager**, vérifie / crée cette arborescence :

webroot/
index.php
api/
generate.php
download.php
lib/
ia.php
itunes.php
playlist_store.php
data/
cache/
playlists/


###  À faire dans le panel
1. Ouvre **File Manager**
2. Va dans `webroot/`
3. Crée les dossiers s’ils n’existent pas :
   - `webroot/api/`
   - `webroot/lib/`
   - `webroot/data/cache/`
   - `webroot/data/playlists/`
4. Colle/Upload les fichiers PHP dans les bons dossiers (exactement comme ci-dessus)

> Important : `data/cache/` et `data/playlists/` doivent être **écrivables** par PHP.  
> Sur Pelican/Ptero c’est généralement OK si les dossiers existent.

---

## 2) Démarrer le serveur (Panel)

Dans l’onglet **Console** du panel :

- Clique **Start** (ou redémarre si déjà lancé).
- Attends le message indiquant que Nginx/PHP-FPM est démarré.

---

## 3) Tester que le site tourne

Ouvre dans ton navigateur :

- Page principale :  
  `http://node.wavescloud.fr:40171/`

Tu dois voir l’interface SmartMix.

---

## 4) Tester l’API (diagnostic rapide)

### Génération JSON

 Si tout marche, tu obtiens un JSON avec :
- `token`
- `target_sec`
- `total_sec`
- `tracks[]`

### Export CSV
Copie le `token` du JSON et ouvre :


 Ton navigateur doit télécharger un fichier `.csv`.

---

## 5) Résolution de problèmes

### A) Page blanche / erreur 500
1. Va dans **Console** du panel
2. Recharge la page
3. Regarde les logs : la ligne d’erreur PHP indique le fichier et la ligne.

Erreurs fréquentes :
- **Parse error** : tu as collé du code avec un `<?php` en trop dans un fichier.
- **Permission denied** : `webroot/data/cache` ou `webroot/data/playlists` n’existent pas ou ne sont pas écrivable.

### B) “Télécharger CSV” ne marche pas
- Vérifie que `webroot/api/download.php` existe
- Vérifie que `webroot/data/playlists/` existe
- Le bouton CSV ne s’active qu’après une génération réussie (token présent)

### C) Génération très lente
La génération dépend de services externes :
- iTunes est rapide
- Internet Archive peut être lent (variable)

Conseils :
- coche **2–4 styles max**
- coche **1–3 décennies max**
- relance une génération (les caches IA peuvent accélérer)

---

## 6) Où modifier quoi ?

- UI / design / cases à cocher : `webroot/index.php`
- Algorithme de génération : `webroot/api/generate.php`
- Source Internet Archive : `webroot/lib/ia.php`
- Source iTunes : `webroot/lib/itunes.php`
- Stockage token playlist : `webroot/lib/playlist_store.php`
- Export CSV : `webroot/api/download.php`

---

## Vérification finale (checklist)
- [ ] `webroot/index.php` existe
- [ ] `webroot/api/generate.php` répond en JSON
- [ ] `webroot/api/download.php?token=...` télécharge un CSV
- [ ] `webroot/data/cache/` existe
- [ ] `webroot/data/playlists/` existe
- [ ] Le serveur est démarré via le panel
## 7) Compiler le raopport 

Le PDF peut ne pas être prévisualisable directement sur GitHub mais le fichier peut être téléchargé et compilé à partir des sources LaTex, du code rapport du dossier 'rapport'.
