Design Instagram

Objective: Discuss and design schema for Instagram.

Requirement Analysis:
1. Analyse various entities.
2. Identify relationships between entities.
3. Define attributes for each entity.
4. Discuss keys and constraints for each entity.
5. Create a schema diagram.
6. Tackle two important areas:
  - User Management (User, Profile)
  - Post Management (Post, Comment, Like)


Step 1: Identifying Entities

1. User
  - Represents a user of the Instagram application.
2. Post
  - Represents a post made by a user.
  - Assumption: A post can be of any type (image, video, etc.).
3. Like
  - Represents a like made by a user on a post.
4. Comment
  - Represents a comment made on a post by a user.
5. Profile
  - Represents the profile information of a user.

Step 2: Writing attributes for each entity

1. User
  - userId (INT) (Primary Key)
  - userName (VARCHAR)
  - email (VARCHAR)
  - firstName (VARCHAR)
  - lastName (VARCHAR)
  - DOB (DATE)
  - accountCreatedAt (DATETIME)

Things to discuss:
  - `UNIQUE` constraint on userName and email.
  - Age can be a derived attribute from DOB.
  - Discussing datatypes such has VARCHAR, INT, DATE, DATETIME.

2. Post
  - postId (INT) (Primary Key)
  - userId (INT) (Foreign Key referencing User - Used to enforce referential integrity)
  - postDate (DATETIME)
  - postCaption (VARCHAR)
  - tags (VARCHAR)

Things to discuss:
  - tags is a multivalued attribute, can be stored as a separate table.
  - postCaption can be NULL if the post is an image without a caption.
  - Choosing userId as a foreign key to link posts to users. This enforces that a post must belong to a user and hence maintains referential integrity.

3. Like
  - likeId (INT) (Primary Key)
  - postId (INT) (Foreign Key referencing Post)
  - userId (INT) (Foreign Key referencing User)
  - likeDate (DATETIME)

Things to discuss:
  - Choosing postId and userId as foreign keys to link likes to posts and users respectively.

4. Comment
  - commentId (INT) (Primary Key)
  - postId (INT) (Foreign Key referencing Post)
  - userId (INT) (Foreign Key referencing User)
  - parentCommentId (INT) (Foreign Key referencing Comment - Used for nested comments)
  - commentText (VARCHAR)
  - commentDate (DATETIME)

Things to discuss:
  - parentCommentId allows for nested comments. Can be used to handle `replies` to a particular comment.
  - commentText can be NULL if the comment is a reaction (like an emoji).
  - Choosing postId and userId as foreign keys to link comments to posts and users respectively. This enforces that a comment must belong to a post and a user, maintaining referential integrity.

5. Profile
  - userId (INT) (Primary Key, Foreign Key referencing User)
  - profileBio (VARCHAR)
  - followersCount (INT)
  - followingCount (INT)
  - postCount (INT)

Things to discuss:
  - userId as a foreign key to link profile to user. This enforces that a profile must belong to a user. Since, this is unique to a user, it can also be a primary key.
  - profileBio can be NULL if the user has not set a bio.

Step 3: Identifying Relationships among entities

User relationships:
1. User to Post
  - A user can have multiple posts, but a post belongs to one user.
  - Relationship: One-to-Many

2. User to Like
  - A user can like multiple posts, but a like belongs to one user.
  - Relationship: One-to-Many

3. User to Comment
  - A user can comment on multiple posts, but a comment belongs to one user.
  - Relationship: One-to-Many
  - A user can also reply to multiple comments, but a comment belongs to one user.
  - Relationship: One-to-Many

4. User to Profile
  - A user has one profile, and a profile belongs to one user.
  - Relationship: One-to-One

5. User to User 
  - A user can follow multiple users, and a user can be followed by multiple users.
  - Relationship: Many-to-Many
  - This relationship can be represented using a separate table `User_Follow` with attributes:
    - followerId (INT) (Foreign Key referencing User)
    - followedId (INT) (Foreign Key referencing User)


Post relationships:
1. Post to Like
  - A post can have multiple likes, but a like belongs to one post.
  - Relationship: One-to-Many

2. Post to Comment
  - A post can have multiple comments, but a comment belongs to one post.
  - Relationship: One-to-Many

3. Post to Tag
  - A post can have multiple tags, and a tag can belong to multiple posts.
  - Relationship: Many-to-Many
  - This relationship can be represented using a separate table `Post_Tag` with attributes:
    - postId (INT) (Foreign Key referencing Post)
    - tag (VARCHAR)

