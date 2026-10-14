# Réponses aux questions de réflexion

### 1. Before building anything: your personal weighting of weather vs. CO₂. 

Si je devais choisir personnellement, j'accorderais un poids prioritaire à un faible bilan carbone (en privilégiant les trajets proches ou accessibles en train)
tout en exigeant un seuil minimal de météo acceptable (pas de pluie continue), sans jamais ignorer complètement l'un des deux critères.
Pour moi, le climat agréable valide le départ, mais l'empreinte carbone tranche la destination finale parmi les options acceptables.

### 2. Why one batched API call is more reliable, not just faster, than 26 separate calls.

Avec 26 requêtes, on répète le processus 26 fois. Cette répétition multiplie par 26 les chances d'une coupure ou latence réseau, ce qui fait échouer la requête en cours
et interrompt le script. Avec 1 seule requête groupée, on exécute la requête une seule fois ce qui minimise le risque de perte de réseau. Un autre problème vient directement
de l'API qui peut limiter le nombre de requêtes consécutives pour éviter les attaques ou le spam. En fonction de l'API, elle risque donc de bloquer des requêtes.

### 3. What you'd do about the CO₂ emissions-factor number before publishing this for real.

Pour rendre ce chiffre exploitable par de vrais voyageurs, je remplacerais cette constante fixe par une API d'empreinte carbone mise à jour. 
Cela permettrait de calculer l'impact selon le mode de transport réel (train vs avion) plutôt que d'imposer un vol court-courrier, 
d'inclure le forçage radiatif en altitude, et de mentionner explicitement la source méthodologique sur le dashboard pour garantir la transparence des données.

### 4. What normalization within a list of 26 means for a KPI vs. a raw measurement.

La température réelle de la capitale médiocre ne changerait absolument pas (la mesure physique reste identique). 
En revanche, son score augmenterait.   
Puisque la normalisation étire les valeurs entre le minimum et le maximum du groupe, l'arrivée d'une ville encore plus froide et pluvieuse abaisserait la borne minimale. 
La capitale médiocre se retrouverait alors mécaniquement plus haut dans l'intervalle [0-1]. 

### 5. Your predicted winning capital, before running the script.

En privilégiant un climat très favorable tout en appliquant une pénalité sur les émissions CO2, Madrid devrait obtenir le meilleur score global car son ensoleillement élevé et ses températures douces compensent largement sa distance intermédiaire depuis Paris par rapport aux capitales nordiques ou très proches. 

### 6. Whether your prediction matched the real result, and why/why not.

La prédiction ne correspond pas au résultat réel affiché par le pipeline, où Rome arrive en tête du classement avec la formule 50/50.
Ce qui me surprend principalement c'est que bien que Madrid offre une météo nettement supérieure (température et ensoleillement), sa distance importante depuis Paris lui attribue un score CO2 très bas une fois normalisé sur l'échelle 0-1.

### 7. What signal on the live page would tell a visitor the pipeline had silently broken.

La seule information permettant au visiteur de détecter un arrêt du pipeline est la ligne Data last updated.
Si la date affichée a plus de 7 jours (la fréquence étant hebdomadaire), les données ne sont plus à jour.
Ce signal est insuffisant car il exige une vérification manuelle du visiteur. 
Pour corriger cela il faudrait peut être ajouter un bandeau ou un badge de statut plus visible.

### 8. Which file(s) you changed for the origin-city extension, and whether the "best" destination is absolute or relative to your starting point.

- **Fichiers modifiés :**
  - `scripts/fetch_and_score.py` : Remplacement des coordonnées de Paris par celles de Madrid (`40.4168, -3.7038`) et mise à jour de la variable utilisée dans le calcul de la distance (`ORIGIN_LAT`, `ORIGIN_LON`).
  - `docs/index.html` : Remplacement du texte de titre "from Paris" par "from Madrid".

