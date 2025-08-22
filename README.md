        Extraction de données - Loire Atlantique
       (Chirurgiens-Dentistes via Web Scraping)

OBJECTIF
--------
L’objectif de ce projet est de collecter automatiquement
les coordonnées des chirurgiens-dentistes du département
Loire-Atlantique (44) à partir du site :
http://annuairesante.ameli.fr

PACKAGES UTILISÉS
-----------------
- requests : récupération du contenu HTML
- BeautifulSoup4 : parsing et extraction des balises HTML
- pandas : structuration et sauvegarde des données

ÉTAPES DU SCRAPING
------------------
1. Chargement de la page principale
   - URL : http://annuairesante.ameli.fr/trouver-un-professionnel-de-sante/chirurgiens-dentistes/44-loire-atlantique
   - Extraction des trois listes de communes (balises <ul> des classes "first", "second", "third").

2. Extraction des URLs des communes
   - Construction de 3 listes d’URLs : L1, L2, L3.

3. Collecte des praticiens par commune
   - Pour chaque URL de commune, récupération des liens de fiches praticiens.
   - Stockage des liens dans une liste "ll" (217 praticiens trouvés dans la première liste).

4. Extraction des informations praticien
   Pour chaque fiche praticien, les informations suivantes sont extraites :
   - Nom et prénom
   - Structure (société)
   - Bâtiment (si présent)
   - Adresse complète
   - Complément d’adresse (si présent)
   - Commune

   Une fonction "adress()" a été créée pour nettoyer et segmenter
   les adresses selon leur format (2 à 5 éléments).

5. Structuration des données
   - Création d’un DataFrame pandas avec les colonnes :
     ['Nom Prénom','BATIMENT','SOCIETE','ADRESSE','Coplement ADR','COMMUNE']
   - Assemblage des résultats des trois listes de communes (df_1, df_2, df_3).

6. Export final
   - Fusion des DataFrames en un seul : DATA
   - Sauvegarde au format CSV :
     Donnees_extraites.csv

RÉSULTAT
--------
Un fichier CSV contenant la liste complète des chirurgiens-dentistes
de Loire-Atlantique avec leurs coordonnées, prêt à être utilisé
pour l’analyse ou tout traitement ultérieur.
