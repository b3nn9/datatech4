scala> val inputRDD = sc.textFile("file:///C:/opt/spark-2.2.1-bin-hadoop2.7/README.md")
~~~
inputRDD: org.apache.spark.rdd.RDD[String] = file:///C:/opt/spark-2.2.1-bin-hadoop2.7/README.md MapPartitionsRDD[17] at textFile at <console>:24
~~~
scala> val sparkRDD = inputRDD.filter(line => line.contains("spark"))
~~~
sparkRDD: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[18] at filter at <console>:25
~~~
scala> val apacheRDD = inputRDD.filter(line=>line.contains("apache"))
~~~
apacheRDD: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[19] at filter at <console>:25
~~~
scala> val unionRDD = sparkRDD.union(apacheRDD)
~~~
unionRDD: org.apache.spark.rdd.RDD[String] = UnionRDD[20] at union at <console>:27
~~~
scala> sparkRDD.count()
~~~
res11: Long = 13
~~~
scala> apacheRDD.count()
~~~
res12: Long = 10
~~~
scala> unionRDD.count()
~~~
res13: Long = 23
~~~
scala> inputRDD.take(3).foreach(println)
~~~
# Apache Spark

Spark is a fast and general cluster computing system for Big Data. It provides
~~~
scala> sparkRDD.take(3).foreach(println)
~~~
<http://spark.apache.org/>
guide, on the [project web page](http://spark.apache.org/documentation.html).
["Building Spark"](http://spark.apache.org/docs/latest/building-spark.html).
~~~
scala> apacheRDD.take(3).foreach(println)
~~~
<http://spark.apache.org/>
guide, on the [project web page](http://spark.apache.org/documentation.html).
Spark is built using [Apache Maven](http://maven.apache.org/).
~~~
scala> val input = sc.parallelize(List(1,2,3,4))
~~~
input: org.apache.spark.rdd.RDD[Int] = ParallelCollectionRDD[21] at parallelize at <console>:24
~~~
scala> val result = input.map(x=>x*x)
~~~
result: org.apache.spark.rdd.RDD[Int] = MapPartitionsRDD[22] at map at <console>:25
~~~
scala> println(result.collect().mkString(","))
~~~
1,4,9,16
~~~
scala> s"aa\tbb\tcc"
~~~
res18: String = aa      bb      cc
~~~
scala> List("aa", "bb", "cc").mkString("\t")
~~~
res19: String = aa      bb      cc
~~~
scala> val lines = sc.parallelize(List("hello spark","hi"))
~~~
lines: org.apache.spark.rdd.RDD[String] = ParallelCollectionRDD[23] at parallelize at <console>:24
~~~
scala> val words = lines.flatMap(line=>line.split(" "))
~~~
words: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[24] at flatMap at <console>:25
~~~
scala> words.first()
~~~
res20: String = hello
~~~
scala> val rdd1 = sc.parallelize(List("coffee","coffee","tea","milk"))
~~~
rdd1: org.apache.spark.rdd.RDD[String] = ParallelCollectionRDD[25] at parallelize at <console>:24
~~~
scala> val rdd2 = sc.parallelize(List("coffee","cola","water"))
~~~
rdd2: org.apache.spark.rdd.RDD[String] = ParallelCollectionRDD[26] at parallelize at <console>:24
~~~
scala> rdd1.distinct().foreach(println)
~~~
tea
coffee
milk
~~~
scala> rdd1.intersection(rdd2).foreach(println)
~~~
coffee
~~~
scala> rdd1.subtract(rdd2).foreach(println)
~~~
milk
tea
~~~
scala> rdd1.cartesian(rdd2).foreach(println)
~~~
(coffee,cola)
(coffee,coffee)
(coffee,water)
(coffee,coffee)
(coffee,water)
(coffee,cola)
(tea,coffee)
(tea,water)
(tea,cola)
(milk,water)
(milk,cola)
(milk,coffee)
~~~
scala> rdd1.sample(false,0.5).foreach(println)
~~~
coffee
tea
~~~
scala> val data = sc.parallelize(List(1,2,3,3))
~~~
data: org.apache.spark.rdd.RDD[Int] = ParallelCollectionRDD[42] at parallelize at <console>:24
~~~
scala> data.collect()
~~~
res27: Array[Int] = Array(1, 2, 3, 3)
~~~
scala> data.countByValue()
~~~
res28: scala.collection.Map[Int,Long] = Map(1 -> 1, 2 -> 1, 3 -> 2)
~~~
scala> data.top(2)
~~~
res29: Array[Int] = Array(3, 3)
~~~
scala> data.takeSample(false,1).take(1).foreach(println)
~~~
3
~~~
scala> data.reduce((x,y)=>x+y)
~~~
res31: Int = 9
~~~
scala> data.reduce(_+_)
~~~
res32: Int = 9
~~~
scala> data.aggregate((0,0))((x,y)=>(x._1+y,x._2+1),(x,y)=>(x._1+y._1,x._2+y._2))
~~~
res33: (Int, Int) = (9,4)
~~~
