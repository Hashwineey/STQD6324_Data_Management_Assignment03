# MovieLens 100K Dataset Analysis using Apache Spark & Cassandra

This project demonstrates big data processing using Apache Spark and Cassandra. It covers data ingestion, transformation, storage, and analysis of the [MovieLens 100K dataset](https://grouplens.org/datasets/movielens/100k/), a commonly used benchmark in recommendation systems and data mining research.

---

## Dataset Files

- `u.user`: User demographic information
- `u.item`: Movie metadata
- `u.data`: User ratings of movies

---

## Technologies Used

- **Apache Spark 2** (PySpark)
- **Cassandra 3**
- **Python 3**
- **Jupyter Notebook / Zeppelin**
- **Docker / VirtualBox (initial setup, replaced with on-prem Spark)**

---

## Project Workflow

1. **Data Loading & Parsing**
   - Read and parse `u.user`, `u.item`, and `u.data` files into Spark RDDs/DataFrames
2. **Schema Transformation**
   - Clean and transform raw data
3. **Cassandra Integration**
   - Write and read Spark DataFrames to/from Cassandra
4. **Query Execution**
   - Perform analytical queries using Spark SQL and Cassandra CQL

---

## ❓ Analysis Questions

1. How many users rated movies released in 1995?
2. What is the most-watched genre by female users?
3. What is the average rating of 'Toy Story (1995)' across all users?
4. Which age group gives the highest average movie rating?
5. How many movies have never been rated?

---

## Sample Output

> Example queries and results will be displayed here after execution.

---

## Insights & Challenges

- Learned how to handle multi-source file integration using Spark.
- Understood Cassandra’s columnar storage and its integration with Spark.
- Faced DNS issues in Docker and migrated setup to university machine.

---

## References

- [MovieLens Dataset](https://grouplens.org/datasets/movielens/)
- [Apache Spark Docs](https://spark.apache.org/docs/latest/)
- [Cassandra Docs](https://cassandra.apache.org/doc/latest/)

---

## Author

- Hashwineey Tamilselvan | MSc Data Science



