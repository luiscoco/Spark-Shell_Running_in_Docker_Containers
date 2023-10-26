# Spark_Running_in_Docker_Containers

Apache SPARK Up and Running FAST with Docker: https://www.youtube.com/watch?v=Zr_FqYKC6Qc

## Run Docker Desktop

![image](https://github.com/luiscoco/Spark-Shell_Running_in_Docker_Containers/assets/32194879/1dae31df-6aaf-496d-bbdb-e695ee16bafb)

## Pull Spark Docker images 

![image](https://github.com/luiscoco/Spark-Shell_Running_in_Docker_Containers/assets/32194879/54a45dc6-383d-47a9-996b-18ac12bed59c)

## Run the Spark Docker container

Type this command to run the Spark docker container

```
docker run -it spark /opt/spark/bin/spark-shell
```

![image](https://github.com/luiscoco/Spark-Shell_Running_in_Docker_Containers/assets/32194879/3e41806f-2f7d-47f0-a99b-c9d69e1a1cff)

## Examples

Here are a few Scala code snippets that you can run in the Spark shell to perform various operations:

### Create a Resilient Distributed Dataset (RDD):

```scala
val data = Array(1, 2, 3, 4, 5)
val rdd = sc.parallelize(data)
println("RDD Elements: " + rdd.collect().mkString(", "))
```

![image](https://github.com/luiscoco/Spark-Shell_Running_in_Docker_Containers/assets/32194879/5d884dde-67c8-44f8-b355-5ab2477e1e1f)

### Map and Reduce:

```scala
val squaredRDD = rdd.map(x => x * x)
val sum = squaredRDD.reduce((x, y) => x + y)
println("Squared RDD Elements: " + squaredRDD.collect().mkString(", "))
println("Sum of Squared Elements: " + sum)
```

![image](https://github.com/luiscoco/Spark-Shell_Running_in_Docker_Containers/assets/32194879/6f3922ef-de14-484b-87e7-b7d0b500d714)

### Filtering:

```scala
val evenRDD = rdd.filter(x => x % 2 == 0)
println("Even Elements: " + evenRDD.collect().mkString(", "))
```

![image](https://github.com/luiscoco/Spark-Shell_Running_in_Docker_Containers/assets/32194879/c1776e73-4e25-4ae4-a397-b0fd36517cc6)

### Read from a text file:

```scala
val textFileRDD = sc.textFile("C:/Users/LEnriquez/3D Objects/Downloads/testFile.txt")
println("Text File Content: " + textFileRDD.collect().mkString("\n"))
```

### Word Count:

```scala
val words = textFileRDD.flatMap(line => line.split(" "))
val wordCounts = words.map(word => (word, 1)).reduceByKey(_ + _)
println("Word Counts: " + wordCounts.collect().mkString(", "))
```

### Joining RDDs:

```scala
val rdd1 = sc.parallelize(Array((1, "Alice"), (2, "Bob")))
val rdd2 = sc.parallelize(Array((1, 25), (2, 30)))
val joinedRDD = rdd1.join(rdd2)
println("Joined RDD: " + joinedRDD.collect().mkString(", "))
```

![image](https://github.com/luiscoco/Spark-Shell_Running_in_Docker_Containers/assets/32194879/6dbcad18-925c-451c-82be-f36abfde3b38)

### Persisting RDD:

```scala
squaredRDD.persist()
println("Squared RDD Elements (after persist): " + squaredRDD.collect().mkString(", "))
```

### Custom Function:

```scala
def multiplyByTwo(x: Int): Int = x * 2
val result = rdd.map(multiplyByTwo)
println("Result after custom function: " + result.collect().mkString(", "))
```
