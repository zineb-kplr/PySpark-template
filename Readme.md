1-Run the docker-compose to setup spark :
```
docker-compose up -d
```

2-Access to spark worker container : 
```
docker exec -it spark-worker /bin/bash
```

3-Install py4j module :
```
python3 -m pip install py4j
```
4-launch the Python interpreter:
```
python3
```
5-Import the necessary modules and create a SparkContext:

```
from pyspark import SparkContext
from pyspark.sql import SparkSession
# Create a SparkContext
sc = SparkContext("local", "PySpark Playground")
spark = SparkSession(sc)
```
