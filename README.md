![movielens](https://github.com/user-attachments/assets/11cd3350-d6a0-437c-982a-ddf5e765b227)

# 🎬 MovieLens Analytics with Spark Cassandra in Zeppelin Notebook

This project explores the MovieLens 100k dataset using Apache Spark and Cassandra in Zeppelin Notebook. The objective was to process real-world structured data, store it in a distributed NoSQL database, and perform analytical queries using Spark SQL, all within a Big Data ecosystem.

---

## 🧰 Tools & Technologies
- **Apache Spark 2 (PySpark)**
- **Cassandra NoSQL Database**
- **Zeppelin Notebook**
- **HDFS (Hadoop Distributed File System)**
- **HDP Sandbox (via VirtualBox)**

---

## 📂 Dataset Overview

The project uses the **MovieLens 100k** dataset which contains:
- `u.user` — 943 user profiles (age, gender, occupation, zip)
- `u.item` — 1,682 movie details (title, genre flags)
- `u.data` — 100,000 movie ratings (user, movie, rating, timestamp)

These files were:
- Downloaded and stored in **HDFS**
- Parsed with predefined **Spark schemas**
- Stored into **Cassandra tables** for persistence

---

## 📊 Results Summary

### Q1: Average Rating for Each Movie (Top 10)
We calculated the average rating for each movie by joining ratings_df_clean with titles_df using Spark SQL. The result was sorted by highest average rating and top 10 were displayed. This helped identify the most critically appreciated movies based on viewer ratings.

### Q2: Top 10 Movies with Highest Average Ratings (≥ 50 ratings)
To ensure fairness, only movies with at least 50 user ratings were considered. We grouped by movie title, filtered using HAVING COUNT(*) >= 50, and then sorted by average rating. This ensured that highly-rated but rarely-rated movies did not skew the results.

### Q3: Favourite Genre of Active Users (≥ 50 ratings)
Users who rated at least 50 movies were extracted, then joined with genre information from titles_df. Genres were unpivoted using stack() and the most frequently rated genre per user was calculated. This helped identify viewing preferences of the most engaged users.

### Q4: Users Below Age 20
A simple Spark SQL filter on users_df using WHERE age < 20 displayed all users who were teenagers or children. This could be used to analyze the demographic distribution of young users in the dataset.

### Q5: Scientists Aged Between 30 and 40
Another filtered query on users_df identified all users whose occupation was scientist and whose age was between 30 and 40. This showed a specific subgroup of professionals for targeted analysis.

---

## ✅ Conclusion

This project demonstrates an end-to-end pipeline using Apache Spark and Cassandra in Zeppelin Notebook to analyze the MovieLens 100k dataset. All three key files (u.user, u.item, and u.data) were:

+ Uploaded into HDFS
+ Parsed using Spark
+ Saved into Cassandra tables

Spark SQL was then used for analytical queries, leveraging in-memory computation. The combination of distributed processing and NoSQL storage enabled efficient handling of real-world scale datasets. This notebook shows how to build scalable and insightful data analytics pipelines for structured datasets.

---

## How to Reproduce?

1. Start HDP Sandbox (with Spark + Cassandra services running)
2. Open Zeppelin at `http://sandbox-hdp.hortonworks.com:9995` (or your Zeppelin Notebook port)
3. Paste the notebook blocks into `%sh` and `%pyspark` cells
4. Create Cassandra keyspace & tables using `cqlsh` in PuTTY or terminal
5. Run all queries & export results as needed

---




