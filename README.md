 
#        EXTRACTION ET ANALYSE DE DONNEES
 
 
Auteur : Mohamed YOULA   

----------------------------------------------------- 
OBJECTIF
-----------------------------------------------------
Ce projet a pour but de :
1. Extraire automatiquement les coordonnées des chirurgiens-dentistes 
   de Loire-Atlantique (44) à partir du site ameli.fr
2. Enrichir ces données avec la population des communes
3. Réaliser une analyse statistique sur la répartition
   des praticiens et le rapport population/praticien.

-----------------------------------------------------
DONNEES UTILISEES
-----------------------------------------------------
1. Donnees_extraites.csv  → Données issues du scraping :
   - Nom, Prénom
   - Adresse
   - Commune
2. Loire_atlantique.csv   → Données de population
   par commune

-----------------------------------------------------
PACKAGES UTILISES
-----------------------------------------------------
- requests
- beautifulsoup4
- pandas
- unidecode
- seaborn
- matplotlib


# ETAPE 1 : WEB SCRAPING

1. Chargement de la page principale :
   http://annuairesante.ameli.fr/trouver-un-professionnel-de-sante/chirurgiens-dentistes/44-loire-atlantique

2. Extraction des trois listes de communes (balises des classes "first", "second", "third").

3. Collecte des praticiens par commune :
   - Récupération des liens des fiches praticiens
   - 217 praticiens trouvés pour la première liste (exemple)

4. Extraction des informations praticien :
   - Nom et prénom
   - Structure (société)
   - Bâtiment (si présent)
   - Adresse complète
   - Complément d’adresse
   - Commune

5. Structuration des données :
   - DataFrame pandas avec colonnes :
     ['Nom Prénom','BATIMENT','SOCIETE','ADRESSE','Coplement ADR','COMMUNE']

6. Export final :
   - Fichier CSV : Donnees_extraites.csv

# ETAPE 2 : TANSFORMATION ET PREPARATION DE DONNEES

1. Nettoyage des noms de communes pour uniformiser l’écriture
   (SAINT → ST, suppression des accents, etc.)
2. Ajout d’une colonne "PTOT" = population totale
   → Jointure entre praticiens et fichier Loire_atlantique.csv
3. Correction des valeurs manquantes
   → Remplissage manuel de quelques communes absentes


# ETAPE 3 : ANALYSES DE DONNEES

1) Distribution du nombre de praticiens par commune
   - Calcul du nombre de praticiens uniques
   - Histogrammes + boxplots
   - Détection et suppression des outliers (méthode IQR)
   - Résultat : ~3 praticiens par commune en moyenne
     (hors valeurs aberrantes).

2) Distribution population/praticien
   - Ajout colonne "Population_par_praticien"
   - Calcul = Population totale / Nb praticiens
   - Détection des outliers
   - Résultat : ~1 486 habitants par praticien en moyenne
     (hors valeurs aberrantes)
   - Min : 272 habitants/praticien
   - Max : 3 359 habitants/praticien

3) Analyse des outliers
   - Communes avec beaucoup de praticiens (Nantes,
     Saint-Nazaire, Rezé, Saint-Herblain, etc.)
   - Communes avec ratio habitants/praticien très élevé
     (souvent grandes villes).


# RESULTATS

- Une base de données enrichie croisant praticiens et 
  population communale
- Identification des communes avec forte densité
  de praticiens
- Rapport population/praticien ≈ 1 500 habitants/praticien
  dans les communes standards

# FICHIERS GENERES

- Donnees_extraites.csv  (praticiens et adresses)
- Loire_atlantique.csv   (population communale)
- Graphiques (histogrammes et boxplots)

