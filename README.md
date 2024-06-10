# 1. INSTAGRAM USER ANALYTICS

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

- Inactive User Engagement:

Query:

```sql
SELECT users.id AS "Id", users.username AS "List of Inactive Users" 
FROM users 
LEFT JOIN photos ON users.id = photos.user_id 
WHERE photos.user_id IS NULL;
```
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
- Hashtag Research:

Query:

```sql
SELECT tags.id AS "Tag Id", tags.tag_name AS "Hashtag Name", COUNT(photo_tags.tag_id) AS Total_Count 
FROM tags JOIN photo_tags ON tags.id = photo_tags.tag_id 
GROUP BY tag_name 
ORDER BY Total_Count DESC 
LIMIT 5;
```
- Ad Campaign Launch:

Query:

```sql
SELECT DAYNAME(created_at) AS "Day",COUNT(id) AS Number_of_users_registered
FROM users 
GROUP BY DAYNAME(created_at) 
ORDER BY Number_of_users_registered DESC;
```
#### (B) Investor Metrics:
- User Engagement:

Query:
```sql
SELECT COUNT(id) AS "Total No. of Photos on Instagram" FROM photos;
```
```sql
SELECT COUNT(id) AS "Total No. of Users on Instagram" FROM users;
```
```sql
SELECT COUNT(DISTINCT(user_id)) AS "Total No. of Active Users" FROM photos;
```
```sql
SELECT 
ROUND((SELECT COUNT(id) AS "Total No. of Photos on Instagram" FROM photos)/(SELECT COUNT(id) AS "Total No. of Users on Instagram" FROM users),2) 
AS "Total No. of Photos / Total No. of Users on Instagram";
```
```sql
SELECT AVG(posts_per_user) AS Average_posts_per_user
FROM (SELECT COUNT(*) AS posts_per_user FROM photos GROUP BY user_id) 
AS user_posts_count;
```
- Bots & Fake Accounts:

Query:

```sql
SELECT users.id AS "Id", users.username AS "Username", COUNT(DISTINCT(likes.photo_id)) AS "Overall Likes Count" 
FROM users JOIN likes ON users.id = likes.user_id 
GROUP BY users.id 
HAVING COUNT(DISTINCT(likes.photo_id)) = (SELECT COUNT(*) FROM photos);
```
