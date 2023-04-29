# Functional Requirements

- User can create and publish a post
- User can follow or unfollow other users
- User can like ,share or comment the posts from user's timeline
- User can view the posts from his followers/friends
- Served to consumers via mobile/webapp
- Feed will contain images/videos and text
- Video streaming is out of scope


# Non-Functional Requirements

- Service need to available 
- 200ms to generate feed & 200ms to load the static contents
- System should be reliable


# System View 
- ViewService 
- PostService
- LikeService
- FollowService
- CommentService
- NewsFeedService
- FeedGenerationService
- SearchService
- AccountService

![system view](../../problems/images/newsfeed.png)













# APIs



## Generate news feed

- generateFeed(user_id, timestamp, batchsize,batchrange[])
## User Auth

# Search Users/Accounts
- searchAccount(user_name, user_id)
- searchPhot(user_id,keywords)


## User view/upload/get Photos

- viewPhoto(photo_id,user_id)
- viewPhotos(photo_ids)
- postPhoto(user_id,photo, location, time, title, tags[])

## Users like/comment/share photos

- likePhoto(photo_id,user_id)
- postComment(photo_id, timestamp, user_is, comment)
## Users should be able t follow/unfollow users

- follow(follow_id, followee_id, timestamp)
- unfollow(follow_id, followee_id, timestamp)


# Data Model



## User view/upload/get Photos

- PhotoTable 
  - photoId(primarykey int64) 
  - userId(int64)
  - desc(varchar)
  - imagestore(varchar)
  - timeStamp(dateTime)
- UserTable
- LikeTable
  - PrimaryKey(userId+photoId)  
  - TimeStamp


- CommentTable
  - PrimaryKey(userId+photoId+timestamp)
  - comment(Varchar256)
