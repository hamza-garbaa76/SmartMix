# SmartMix — Générateur de playlist intelligent (L2)

SmartMix est une application web en **PHP 8.x** qui génère automatiquement une playlist à partir de critères choisis par l’utilisateur :
- **Styles musicaux** (multi-sélection)
- **Époques / décennies** (multi-sélection)
- **Durée totale cible** (curseur)

La génération se fait en “live” grâce à **deux sources de données** :
- **Internet Archive** (pistes souvent complètes)
- **iTunes Search API** (previews 30s, très rapide)

Le résultat affiche une liste de titres (avec lecteur audio quand disponible) et permet de **télécharger la playlist en CSV**.

---

## Fonctionnalités

### Interface (front)
- Sélection **multi-styles** via cases à cocher
- Sélection **multi-époques** (décennies) via cases à cocher
- Curseur pour choisir la **durée** (10 à 180 min)
- Bouton **Générer**
- Affichage des KPI : **durée cible**, **durée réelle**, **nombre de titres**
- Liste des titres : **Titre / Artiste / Année / Durée / Source**
- Lecteur audio HTML5 si `audio_url` est présent
- Bouton **Télécharger CSV** (activé après génération)

### Génération (back)
- Récupération de titres via **iTunes** (rapide) puis compléments via **Internet Archive** (plus variable)
- Construction d’une playlist visant à atteindre la durée cible (tolérance ~ ± 1 min)
- Mélange “cohérent” : alternance des styles pour éviter une série de titres du même style
- Sauvegarde serveur de la playlist générée (token) pour l’export CSV

---

## Structure du projet# SmartMix
projet d'un générateur de playlist intelligent
