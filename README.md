![movielens](https://github.com/user-attachments/assets/11cd3350-d6a0-437c-982a-ddf5e765b227)

# MovieLens Analytics with Spark & Cassandra in Zeppelin Notebook

This project explores the MovieLens 100k dataset using Apache Spark and Cassandra in Zeppelin Notebook. The objective was to process real-world structured data, store it in a distributed NoSQL database, and perform analytical queries using Spark SQL, all within a Big Data ecosystem.

---

## Tools & Technologies
- **Apache Spark 2 (PySpark)**
- **Cassandra NoSQL Database**
- **Zeppelin Notebook**
- **HDFS (Hadoop Distributed File System)**
- **HDP Sandbox (via VirtualBox)**

---

## Dataset Overview

The project uses the **MovieLens 100k** dataset which contains:
- `u.user` — 943 user profiles (age, gender, occupation, zip)
- `u.item` — 1,682 movie details (title, genre flags)
- `u.data` — 100,000 movie ratings (user, movie, rating, timestamp)

These files were:
- Downloaded and stored in **HDFS**
- Parsed with predefined **Spark schemas**
- Stored into **Cassandra tables** for persistence

---

## Results Summary

### Q1: Average Rating for Each Movie (Top 10)
We calculated the average rating for each movie by joining ratings_df_clean with titles_df using Spark SQL. The result was sorted by highest average rating and top 10 were displayed. 

![q1](https://github.com/user-attachments/assets/2be53ca1-c5a2-4a52-b67f-00cbc3928c8a)

While each movie in the result has a perfect average rating of 5.0, it’s important to note that these ratings were contributed by a very small number of users, typically between 1 and 3 ratings per movie.

This leads to a skewed result that is not statistically reliable. Movies with only a few ratings may have artificially inflated scores simply because they were rated by a limited audience. As such, these movies may not represent true audience favorites or critically acclaimed films.

To mitigate this, a better approach (applied in Q2) involves filtering out movies that have fewer than 50 ratings, ensuring a more representative list of high-quality films that have been rated by a broader sample of users.

### Q2: Top 10 Movies with Highest Average Ratings (≥ 50 ratings)
To ensure fairness, only movies with at least 50 user ratings were considered. We grouped by movie title, filtered using HAVING COUNT(*) >= 50, and then sorted by average rating. This ensured that highly-rated but rarely-rated movies did not skew the results.

#### Results:
![q2](https://github.com/user-attachments/assets/8aad1269-4ba6-47c7-95d8-c1a69fff55b2)

As mentioned, this output showcases the top 10 movies based on average rating, filtered to only include movies that received at least 50 ratings. By applying this threshold, the analysis avoids statistical noise caused by movies that were rated by only a few users.

The results include critically acclaimed and widely known titles such as Schindler’s List (1993), Casablanca (1942), and Star Wars (1977). These films received high ratings from a significant number of users—ranging from over 100 to nearly 600—indicating consistent viewer satisfaction across a broad audience.

By combining average rating with a minimum participation threshold, this query provides a much more reliable and representative view of the highest-rated movies in the dataset. It also highlights that animated short films like A Close Shave (1995) and The Wrong Trousers (1993) are also audience favorites, despite their shorter format.

### Q3: Favourite Genre of Active Users (≥ 50 ratings)

![q3](https://github.com/user-attachments/assets/55c1ba87-7d5a-4f05-a2e0-e49b4b25a60d)

This output identifies the most active users in the dataset—those who have rated at least 50 movies—and reveals their favourite movie genres based on rating frequency. For example, user 804 rated 105 comedy movies, while user 588 rated 95 drama movies, indicating strong preferences in their viewing habits.

To derive each user’s favourite genre:

+ Movie ratings were joined with genre flags from the movie metadata.
+ All genre columns were unpivoted using Spark’s stack() function to count how many times each genre was rated.
+ For each user, the genre with the highest count was selected as their favourite.

The majority of users shown prefer drama, followed by comedy, action, and thriller. This analysis helps uncover individual taste profiles among highly engaged users, which can be leveraged for personalized movie recommendations, trend analysis, or user segmentation.

### Q4: Users Below Age 20

![q4](https://github.com/user-attachments/assets/06d46cb3-c6f3-4f44-a116-6b97ce8e1975)

This output displays a list of users whose age is below 20, revealing a segment of younger users in the dataset. The majority of them are students, typically aged between 10 and 14, with a few entries showing none or other as their occupation. This suggests that the dataset includes children and teenagers who actively rated movies.

Analyzing this age group is useful for understanding content preferences among younger viewers, especially in education- or family-focused media studies. It also highlights the diversity of user demographics in the MovieLens dataset, supporting further segmentation for personalized recommendations based on age.

### Q5: Scientists Aged Between 30 and 40

![q5](https://github.com/user-attachments/assets/801b9f6c-b4de-4343-bf02-1fbc65314b68)

This output filters the dataset to show all users whose occupation is scientist and whose age falls between 30 and 40, inclusive. The result includes both male and female users across a diverse range of zip codes. Most users are in their early to late 30s, indicating a healthy representation of mid-career professionals in the dataset.

Targeting this demographic is valuable for understanding content preferences among academically inclined or STEM-focused users. It can also assist in designing genre-based recommendations or academic research into media consumption patterns based on occupation and age groups.

---

## Conclusion

This project demonstrates a complete end-to-end data analytics pipeline using Apache Spark, Cassandra, and Zeppelin within a HDP Sandbox environment. The MovieLens 100k dataset was ingested, cleaned, and stored in Cassandra, and Spark SQL was used to extract meaningful insights across user demographics, movie ratings, and genre preferences.

By answering five targeted questions, the project explored user activity, content quality, and audience segmentation. The results highlighted differences in viewing patterns across various age groups and occupations, and surfaced both popular and critically favored movies through a combination of statistical filtering and SQL-based aggregation.

Overall, the integration of distributed processing (Spark), scalable storage (Cassandra), and interactive notebooks (Zeppelin) provided a powerful and efficient workflow for large-scale structured data analysis. This assignment not only reinforced core data engineering concepts, but also demonstrated practical techniques for building recommendation engines, user profiling systems, and genre-based insights in real-world media datasets.

---

## How to Reproduce?

1. Start HDP Sandbox (with Spark + Cassandra services running)
2. Open Zeppelin at `http://sandbox-hdp.hortonworks.com:9995` (or your Zeppelin Notebook port)
3. Paste the notebook blocks into `%sh` and `%pyspark` cells
4. Create Cassandra keyspace & tables using `cqlsh` in PuTTY or terminal
5. Run all queries & export results as needed

---

## Thank you for reading!




