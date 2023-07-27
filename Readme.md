

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
