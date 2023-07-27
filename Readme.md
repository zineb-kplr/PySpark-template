

1- Exécutez le docker-compose pour configurer Spark :
```
docker-compose up -d
```

2- Accédez au conteneur du worker Spark :
```
docker exec -it spark-worker /bin/bash
```

3- Installez le module py4j :
```
python3 -m pip install py4j
```

4- Lancez l'interpréteur Python :
```
python3
```

5- Importez les modules nécessaires et créez un SparkContext :

```
from pyspark import SparkContext
from pyspark.sql import SparkSession
# Créez un SparkContext
sc = SparkContext("local", "PySpark Playground")
spark = SparkSession(sc)
```
