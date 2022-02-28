# Hide Like Counter
## Background and Objectives
Beekeeper's core functionality - the Streams - comes with an ability to “Like” a post or a comment. Some of Beekeeper's customers find the idea of “liking” not in line with their company ideology.
In order to acknowledge customer needs, switching off the “Like count” feature along with referencing features is enabled: 
- Content publisher and other users must not be able to see who and how many people liked their piece of content. 
- Allow customers to decide to disable Like count and referencing features such as Like count in the User profile, number of Likes in Slideshows, push notifications for liked content etc. 
- Make it a setting configurable in the Meta dashboard, and activated by Beekeeper Customer Success Managers, on customer request.

### Feature flag
Feature flag **hide_post_and_comment_like_count** is created for this functionality.
When enabled, likes are counted but not displayed.

### Remove like count in Posts and Post Comments
*List of changed endpoints:*
```
POST /posts/{postid}/like
DELETE /posts/{postid}/like
GET /streams/{streamid}/posts (on page loading)
POST /comments/{id}/like
DELETE /comments/{id}/like
```
*List of changed files*  
> common/beekeeper/common/resources/posts.py  
> common/beekeeper/common/resources/comments.py  

*Comment:*
Return 0 for the like count if the feature flag is enabled.

### Remove “People who like this” popup on Web
*List of changed endpoints:*
```
GET /posts/{postid}/likes
```
*List of changed files*  
> api/beekeeper/api/resources/postsv2.py  

*Comment:*
Return empty list of users who liked, if the feature flag is enabled.

### Remove Like count in the User Profile
*List of changed endpoints:*
```
GET /profiles/{name}
```
*List of changed files*  
> common/beekeeper/common/resources/profile.py  

*Comment:*
Like count information on the User Profile in web application would be equal zero. 
Return 0 for the like count if the feature flag is enabled.

### Disable notifications for like actions
```
POST /posts/{postid}/like
DELETE /posts/{postid}/like
POST /comments/{id}/like
DELETE /comments/{id}/like
```
*List of changed files*  
> common/beekeeper/common/resources/posts.py  
> common/beekeeper/common/resources/comments.py  

*Comment:*
Notification sending on like is skipped if the feature flag is enabled.

### Remove Like count information from slideshows  
Slideshow uses the endpoints mentioned above. No changes needed aside from already made.
