

1- Exécutez le docker-compose pour configurer Spark :
```
docker-compose up -d
```

2- Accédez au conteneur du worker Spark :
```
docker exec -it spark-worker /bin/bash
```
![image](https://github.com/zineb-kplr/PySpark-template/assets/123749462/c51f673b-0cb8-4e69-8e9e-6732c3daf815)

3- Installez le module py4j :
```
python3 -m pip install py4j
```
![image](https://github.com/zineb-kplr/PySpark-template/assets/123749462/4b15fe78-0964-42e3-8542-25ccac1e880a)

4- Lancez l'interpréteur Python :
```
python3
```
![image](https://github.com/zineb-kplr/PySpark-template/assets/123749462/9e34a696-6cfc-4112-a627-2d746b363868)

5- Importez les modules nécessaires et créez un SparkContext :

```
from pyspark import SparkContext, SparkConf
from pyspark.sql import SparkSession
# Créez un SparkContext
sc = SparkContext("local", "PySpark Playground")
spark = SparkSession(sc)
```
6-Créons un RDD à partir de zéro et affichons son contenu :
```
# Votre liste de données dataList
dataList = [("KRYPTON", 36), ("XENON", 54), ("OSMIUM", 76)]

# Créez le RDD à partir de la liste de données
rdd = sc.parallelize(dataList)
# Afficher les éléments du RDD :
rdd.collect()
```
- Qu'avez-vous remarqué ?
- Laquelle des instructions a pris le plus de temps ?
- Pourquoi selon vous ?
- Pour une liste d'opérations possibles sur les RDD, veuillez consulter le lien suivant :
https://spark.apache.org/docs/latest/rdd-programming-guide.html#transformations
https://spark.apache.org/docs/latest/rdd-programming-guide.html#actions

7-Jouons un peu avec notre RDD :

```python
rdd.take(2)
rdd.first()
rdd.count()
```

8-Créons ensuite un deuxième RDD et joignons les deux pour en obtenir un troisième :

```python
dataList2 = [("CHROMIUM", 25), ("CESIUM", 55), ("BARIUM", 56)]
rdd2 = spark.sparkContext.parallelize(dataList2)
rdd3 = rdd.union(rdd2)
rdd3.collect()
```

- Qu'observez-vous dans la sortie ?
- Que pensez-vous de l'immutabilité ?
9-Tentons de trier notre RDD union :

```python
rdd4 = rdd3.sortBy(lambda a: a[1])
rdd4.collect()
```

10-Essayez les commandes suivantes :

```python
rdd4.toDebugString()
rdd3.toDebugString()
```

- Qu'en pensez-vous de la sortie ?
- Quelles sont vos hypothèses ?
- Pourquoi fait-il référence à Java et Scala selon vous ?

- Créons maintenant un dataframe à partir d'un fichier CSV et affichons son contenu :

- Le fichier doit être téléchargé et chargé sur HDFS.
**Ressources utiles :**

- API de référence de SPARK DATAFRAME

- PYSPARK PAR L'EXEMPLE

11-Remplacez putyourfirstnamehere par le dossier personnel que vous avez créé lors du chargement des données sur HDFS :

```python
df = spark.read.option("header", True).format("csv").load("hdfs:///user/root/putyourfirstnamehere/data/zipcodes.csv")
df.show()
```
12-Comptons maintenant les entrées dans notre fichier :

```python
df.count()
```

- Qu'avez-vous remarqué ?
- Quelle instruction a pris le plus de temps ?
- Pourquoi selon vous ?

13-Jouons avec le Dataframe :

```python
df.filter(df.city == "New York").show(df.count(), False)
df.filter(df.state == "MA").count()
df.groupBy("state").count().show()
df.groupBy("state","city").count().show(100)
df.groupBy("state","city").count().orderBy("state", "city").where().show(100)
df.groupBy("state","city").count().alias("zipcount").orderBy("state", "city").where("count > 50").orderBy("count").show(10)
```
