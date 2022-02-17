# Disable Like Count Feature Flag

### Remove like count in Posts and Comments
**List of changed endpoints:**
```
POST /posts/{postid}/like
DELETE /posts/{postid}/like
GET /streams/{streamid}/posts (on page loading)
POST /comments/{id}/like
DELETE /comments/{id}/like
```
**List of changed files**  
> common/beekeeper/common/resources/posts.py  
> common/beekeeper/common/resources/comments.py  

**Comment:**
Return 0 like everywhere as count like.

### Remove “People who like this” popup on Web
**List of changed endpoints:**
```
GET /posts/{postid}/likes
```
**List of changed files**  
> api/beekeeper/api/resources/postsv2.py  

**Comment:**
Return empty list.

### Remove Like count in the User Profile
**List of changed endpoints:**
```
GET /profiles/{name}
```
**List of changed files**  
> common/beekeeper/common/resources/profile.py  

**Comment:**
Like count information on the User Profile in web application would be equal zero. 
Return 0 like everywhere as count like.

### Remove notification
```
POST /posts/{postid}/like
DELETE /posts/{postid}/like
POST /comments/{id}/like
DELETE /comments/{id}/like
```
**List of changed files**  
> common/beekeeper/common/resources/posts.py  
> common/beekeeper/common/resources/comments.py  

**Comment:**
Notification sent skipped.

### Slideshow  
Slideshow in directly connection with Posts and Comments. No changes.