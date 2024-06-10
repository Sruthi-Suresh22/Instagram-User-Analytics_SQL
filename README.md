# 1. INSTAGRAM USER ANALYTICS

### Table of Contents
- [Project Description](project_description)
- [Dataset Details](dataset_details)
- [Task Details](task_details)
  - [(A)Marketing Analysis]((a)marketing_analysis)
  - [(B)Investor Metrics](investing_metrics)
- [Insights](insights)
   - [(A)Marketing Analysis]((a)marketing_analysis)
   - [(B)Investor Metrics]((b)investing_metrics)
- [Conclusion](conclusion)

### Project Description :

This project intends to conduct an extensive analysis of the user engagement process with one of the world's most popular social media platforms : Instagram. User analysis involves tracking how users engage with a digital product, such as a software application or a mobile app. The insights derived from this analysis can be used by various teams within the business. For example, the marketing team might use these insights to launch a new campaign, the product team might use them to decide on new features to build, and the development team might use them to improve the overall user experience.
As a data analyst working with the product team at Instagram, this project involves analyzing user interactions and engagement with the Instagram app to provide valuable insights that can help the business grow.

### Dataset Details :

#### There are total 7 csv files : users, photos, comments, likes, follows, photo_tags and tags.
- Table **users** consists of 100 records having the details of the Instagram users with the columns : `id`, `username`, `created_at`.
- Table **photos** consists of 257 records having the details of the photos posted by the Instagram users with the columns: `id`, `image_url`, `user_id`, `created_dat`.
- Table **comments** consists of 7488 records having the details of the comments posted by the Instagram users with the columns: `id`, `comment_text`, `user_id`, `photo_id`, `created_at`.
- Table **likes** consists of 8782 records having the details of the likes given by the Instagram users with the columns: `user_id`, `photo_id`, `created_at`.
- Table **follows** consists of 7623 records having the followers details with the columns: `follower_id`, `followee_id`, `created_at`.
- Table **photo_tags** consists of 501 records with the columns: `photo_id`, `tag_id`.
- Table **tags** consists of 21 records having the hashtag details with the columns: `id`, `tag_name`, `created_at`.

### Tasks Details: 

#### (A) Marketing Analysis:
1. **Loyal User Reward:** To identify the five oldest users on Instagram as the marketing team wants to reward the most loyal users, i.e., those who have been using the platform for the longest time.
2. **Inactive User Engagement:** To identify users who have never posted a single photo on Instagram as the team wants to encourage inactive users to start posting by sending them promotional emails.
3. **Contest Winner Declaration:** To determine the winner of the contest and provide their details to the team as the team have organized a contest where the user with the most likes on a single photo wins.
4. **Hashtag Research:** To identify the top five most commonly used hashtags on the platform as a partner brand wants to know the most popular hashtags to use in their posts to reach the most people.
5. **Ad Campaign Launch:** To determine the day of the week when most users register on Instagram as the team wants to know the best day of the week to launch ads.

#### (B) Investor Metrics:
1. **User Engagement:** To calculate the average number of posts per user on Instagram. Also, provide the total number of photos on Instagram divided by the total number of users as the Investors want to know if users are still active and posting on Instagram or if they are making fewer posts.
2. **Bots & Fake Accounts:** To identify users (potential bots) who have liked every single photo on the site, as this is not typically possible for a normal user as the Investors want to know if the platform is crowded with fake and dummy accounts.

### Insights:

#### (A) Marketing Analysis:
- Loyal User Reward:
  
Query:

```sql
SELECT id AS "Id", username AS "Top 5 Loyal Users", created_at AS "Joined Instagram at" 
FROM users 
ORDER BY created_at 
LIMIT 5;
```
Result: The top 5 Loyal Users i.e., the oldest users who will get the rewards are as follows:
 
| Id | Top 5 Loyal Users | Joined Instagram at |
|----|-------------------|---------------------|
| 80 | Darby_Herzog      | 2016-05-06 00:14:21 |
| 67 | Emilio_Bernier52  | 2016-05-06 13:04:30 |
| 63 | Elenor88          | 2016-05-08 01:30:41 |
| 95 | Nicole71          | 2016-05-09 17:30:22 |
| 38 | Jordyn.Jacobson2  | 2016-05-14 07:56:26 |

- Inactive User Engagement:

Query:

```sql
SELECT users.id AS "Id", users.username AS "List of Inactive Users" 
FROM users 
LEFT JOIN photos ON users.id = photos.user_id 
WHERE photos.user_id IS NULL;
```
Result: There are 26 users who have never posted a single photo on Instagram.

| Id | List of Inactive Users |
|----|------------------------|
| 5  | Aniya_Hackett          |
| 7  | Kasandra_Homenick      |
| 14 | Jaclyn81               |
| 21 | Rocio33                |
| 24 | Maxwell.Halvorson      |
| 25 | Tierra.Trantow         |
| 34 | Pearl7                 |
| 36 | Ollie_Ledner37         |
| 41 | Mckenna17              |
| 45 | David.Osinski47        |
| 49 | Morgan.Kassulke        |
| 53 | Linnea59               |
| 54 | Duane60                |
| 57 | Julien_Schmidt         |
| 66 | Mike.Auer39            |
| 68 | Franco_Keebler64       |
| 71 | Nia_Haag               |
| 74 | Hulda.Macejkovic       |
| 75 | Leslie67               |
| 76 | Janelle.Nikolaus81     |
| 80 | Darby_Herzog           |
| 81 | Esther.Zulauf61        |
| 83 | Bartholome.Bernhard    |
| 89 | Jessyca_West           |
| 90 | Esmeralda.Mraz57       |
| 91 | Bethany20              |

- Contest Winner Declaration:

Query:

```sql
SELECT users.username AS "Name of the Winner", users.id AS "Id" ,photos.image_url AS "Image URL", COUNT(*) AS Total_Likes
FROM photos 
JOIN users ON users.id = photos.user_id
JOIN likes ON likes.photo_id = photos.id
GROUP BY photos.id
ORDER BY Total_Likes DESC
LIMIT 1;
```
Result: The winner of the contest who is having most likes for a single photo is Zack_Kemmer93.

| Name of the Winner | Id | Image URL           | Total_Likes |
|--------------------|----|---------------------|-------------|
| Zack_Kemmer93      | 52 | https://jarret.name | 48          |

- Hashtag Research:

Query:

```sql
SELECT tags.id AS "Tag Id", tags.tag_name AS "Hashtag Name", COUNT(photo_tags.tag_id) AS Total_Count 
FROM tags JOIN photo_tags ON tags.id = photo_tags.tag_id 
GROUP BY tag_name 
ORDER BY Total_Count DESC 
LIMIT 5;
```
Result: The top five most commonly used hashtags on the platform are as follows:

| Tag Id | Hashtag Name | Total_Count |
|--------|--------------|-------------|
| 21     | smile        | 59          |
| 20     | beach        | 42          |
| 17     | party        | 39          |
| 13     | fun          | 38          |
| 18     | concert      | 24          |

- Ad Campaign Launch:

Query:

```sql
SELECT DAYNAME(created_at) AS "Day",COUNT(id) AS Number_of_users_registered
FROM users 
GROUP BY DAYNAME(created_at) 
ORDER BY Number_of_users_registered DESC;
```
Result: The best day of the week to launch ads will be Thursday & Sunday as inferred from the result.

| Day       | Number_of_users_registered |
|-----------|----------------------------|
| Thursday  | 16                         |
| Sunday    | 16                         |
| Friday    | 15                         |
| Tuesday   | 14                         |
| Monday    | 14                         |
| Wednesday | 13                         |
| Saturday  | 12                         |

#### (B) Investor Metrics:
- User Engagement:

Query:
```sql
SELECT COUNT(id) AS "Total No. of Photos on Instagram" FROM photos;
```
| Total No. of Photos on Instagram |
|----------------------------------|
| 257                              |

```sql
SELECT COUNT(id) AS "Total No. of Users on Instagram" FROM users;
```
| Total No. of Users on Instagram  |
|----------------------------------|
| 100                              |
```sql
SELECT COUNT(DISTINCT(user_id)) AS "Total No. of Active Users" FROM photos;
```
| Total No. of Active Users  |
|----------------------------|
| 74                         |
```sql
SELECT 
ROUND((SELECT COUNT(id) AS "Total No. of Photos on Instagram" FROM photos)/(SELECT COUNT(id) AS "Total No. of Users on Instagram" FROM users),2) 
AS "Total No. of Photos / Total No. of Users on Instagram";
```
| Total No. of Photos / Total No. of Users on Instagram  |
|--------------------------------------------------------|
| 2.57                                                   |
```sql
SELECT AVG(posts_per_user) AS Average_posts_per_user
FROM (SELECT COUNT(*) AS posts_per_user FROM photos GROUP BY user_id) 
AS user_posts_count;
```
| Average_posts_per_user  |
|-------------------------|
| 3.4730                  |

Result: There are 100 users out of which there are 74 Active users who have posted atleast once. Average user posts around 3 - 4 times as inferred from the data.

- Bots & Fake Accounts:

Query:

```sql
SELECT users.id AS "Id", users.username AS "Username", COUNT(DISTINCT(likes.photo_id)) AS "Overall Likes Count" 
FROM users JOIN likes ON users.id = likes.user_id 
GROUP BY users.id 
HAVING COUNT(DISTINCT(likes.photo_id)) = (SELECT COUNT(*) FROM photos);
```
Result: There are 13 users (potential bots) who have liked every single photo on the site, as this is not typically possible for a normal user which account for 13% of the total users and they are as follows:

| Id | Username           | Overall Likes Count |
|----|--------------------|---------------------|
| 5  | Aniya_Hackett      | 257                 |
| 14 | Jaclyn81           | 257                 |
| 21 | Rocio33            | 257                 |
| 24 | Maxwell.Halvorson  | 257                 |
| 36 | Ollie_Ledner37     | 257                 |
| 41 | Mckenna17          | 257                 |
| 54 | Duane60            | 257                 |
| 57 | Julien_Schmidt     | 257                 |
| 66 | Mike.Auer39        | 257                 |
| 71 | Nia_Haag           | 257                 |
| 75 | Leslie67           | 257                 |
| 76 | Janelle.Nikolaus81 | 257                 |
| 91 | Bethany20          | 257                 |

### Conclusion:
The insights drawn from Instagram User Analytics project focusing on the Marketing and Investor Metrics have helped in understanding and extracting valuable information such as the most loyal users, top 5 most used hashtags, the best day of the week to launch ads and to identify the bots and fake accounts etc., could possibly help in the potential development and progress of one of the most popular social media platform Instagram. This analysis could help in making data-driven decisions, whether the platform is growing or became stagnant in its growth etc., by extracting meaningful insights from the data using SQL and MySQL Workbench tool.

