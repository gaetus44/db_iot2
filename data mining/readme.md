# Projet Datamining - Gestion des Bases de Données

Ce projet s’inscrit dans le cadre du module **Datamining**. Il vise à exploiter des données issues de diverses sources pour en extraire des informations pertinentes, à l’aide de techniques de fouille de données, de bases de données relationnelles et d’analyses croisées.

## Architecture
L’ensemble des bases de données est hébergé sur un seul serveur sur une machine virtuelle.
![architecture db](architecture.png)

### Bases de Données et Schémas
1. **Database activites**
   - Contenu : cette database contient toutes les tables anonymisées de dbtransac, dbservices, dbbank1 et dbbank2
   - Schéma : ![Database Service](table%20bd.png)
2. **Database decision_temp**
   - Contenu : cette table contient les décisions après analyse
   - Schéma : ![Database Service](table%20bd%20decicion_temp.png)
3. **Database decision**
   - Contenu : cette table contient les décisions validée
   - Schéma : ![Database Service](table%20bd%20decision.png)

### Scripts python pour le stockage d'image en db
#### Upload 
```python
import mysql.connector

# 🔧 Paramètres de connexion à ta base
db = mysql.connector.connect(
    host="XXX.XXX.XXX.XXX",
    user="XXXXXXX",
    password="XXXXXXXXXX",
    database="XXXXXXXXXXXX"
)

cursor = db.cursor()

# 📂 Fichier image à insérer
image_path = "table db transac.png"

# 📥 Lecture de l'image en binaire
with open(image_path, 'rb') as file:
    image_data = file.read()

# 📝 Requête INSERT dans la table existante
sql = """
    INSERT INTO temporary_decision (id, image, description, user_id)
    VALUES (%s, %s, %s, %s)
"""
values = (1, image_data, "Ceci est une image stockée", 42)

cursor.execute(sql, values)
db.commit()

print("✅ Image insérée avec succès.")

cursor.close()
db.close()

```
#### Download
```python
import mysql.connector

# 🔧 Connexion à la base
db = mysql.connector.connect(
    host="XXX.XXX.XXX.XXX",
    user="XXXXXXX",
    password="XXXXXXXXXX",
    database="XXXXXXXXXXXX"
)

cursor = db.cursor()

# 📥 ID de l'image à récupérer
image_id = 1

# 🔍 Requête SELECT
sql = "SELECT image FROM temporary_decision WHERE id = %s"
cursor.execute(sql, (image_id,))
result = cursor.fetchone()

if result and result[0]:
    # 📁 Sauvegarde sur disque
    with open("image_extraite.jpg", "wb") as file:
        file.write(result[0])
    print("✅ Image extraite avec succès sous le nom : image_extraite.jpg")
else:
    print("❌ Aucune image trouvée avec l'ID :", image_id)

cursor.close()
db.close()
```
Grâce à ce code python, les images seront stockées en hexa dans la db.
### Scripts SQL de Création des Bases de Données
Les scripts de création des bases de données sont disponibles dans le répertoire principal :
- `commande sql db activites`
- `commande sql decision`
- `commande sql decision_temp`



