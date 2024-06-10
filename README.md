# 1. INSTAGRAM USER ANALYTICS

### Project Description :

This project intends to conduct an extensive analysis of the user engagement process with one of the world's most popular social media platforms : Instagram. User analysis involves tracking how users engage with a digital product, such as a software application or a mobile app. The insights derived from this analysis can be used by various teams within the business. For example, the marketing team might use these insights to launch a new campaign, the product team might use them to decide on new features to build, and the development team might use them to improve the overall user experience.
As a data analyst working with the product team at Instagram, this project involves analyzing user interactions and engagement with the Instagram app to provide valuable insights that can help the business grow.

### Dataset Details :

#### There are total 7 csv files : users, photos, comments, likes, follows, photo_tags and tags.
- Table users consists of 100 records having the details of the Instagram users with the columns : id, username, created_at.
- Table photos consists of 257 records having the details of the photos posted by the Instagram users with the columns: id, image_url, user_id, created_dat.
- Table comments consists of 7488 records having the details of the comments posted by the Instagram users with the columns: id, comment_text, user_id, photo_id, created_at.
- Table likes consists of 8782 records having the details of the likes given by the Instagram users with the columns: user_id, photo_id, created_at.
- Table follows consists of 7623 records having the followers details with the columns: follower_id, followee_id, created_at.
- Table photo_tags consists of 501 records with the columns: photo_id, tag_id.
- Table tags consists of 21 records having the hashtag details with the columns: id, tag_name, created_at.

### Tasks Details: 

#### (A) Marketing Analysis:
1. Loyal User Reward: To identify the five oldest users on Instagram as the marketing team wants to reward the most loyal users, i.e., those who have been using the platform for the longest time.
2. Inactive User Engagement: To identify users who have never posted a single photo on Instagram as the team wants to encourage inactive users to start posting by sending them promotional emails.
3. Contest Winner Declaration: To determine the winner of the contest and provide their details to the team as the team have organized a contest where the user with the most likes on a single photo wins.
4. Hashtag Research: To identify the top five most commonly used hashtags on the platform as a partner brand wants to know the most popular hashtags to use in their posts to reach the most people.
5. Ad Campaign Launch: To determine the day of the week when most users register on Instagram as the team wants to know the best day of the week to launch ads.

#### (B) Investor Metrics:
1. **User Engagement:** To calculate the average number of posts per user on Instagram. Also, provide the total number of photos on Instagram divided by the total number of users as the Investors want to know if users are still active and posting on Instagram or if they are making fewer posts.
2. Bots & Fake Accounts: To identify users (potential bots) who have liked every single photo on the site, as this is not typically possible for a normal user as the Investors want to know if the platform is crowded with fake and dummy accounts.

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
![A1](https://github.com/Sruthi-Suresh22/SQL_Projects/assets/162356465/ff931e5c-f774-46f1-be5d-f4622902dea4)



