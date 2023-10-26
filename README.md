# Spark_Running_in_Docker_Containers

Apache SPARK Up and Running FAST with Docker: https://www.youtube.com/watch?v=Zr_FqYKC6Qc

## Build the the Docker images 

docker build -t spark-base:latest ./docker/base

docker build -t spark-master:latest ./docker/spark-master

docker build -t spark-worker:latest ./docker/spark-worker

docker build -t spark-submit:latest ./docker/spark-submit




## Examples

Here are a few Scala code snippets that you can run in the Spark shell to perform various operations:

### Create a Resilient Distributed Dataset (RDD):

```scala
val data = Array(1, 2, 3, 4, 5)
val rdd = sc.parallelize(data)
println("RDD Elements: " + rdd.collect().mkString(", "))
```

### Map and Reduce:

```scala
val squaredRDD = rdd.map(x => x * x)
val sum = squaredRDD.reduce((x, y) => x + y)
println("Squared RDD Elements: " + squaredRDD.collect().mkString(", "))
println("Sum of Squared Elements: " + sum)
```

### Filtering:

```scala
val evenRDD = rdd.filter(x => x % 2 == 0)
println("Even Elements: " + evenRDD.collect().mkString(", "))
```

### Read from a text file:

```scala
val textFileRDD = sc.textFile("path/to/textfile.txt")
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
