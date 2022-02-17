# Disable Like Count Feature Flag

###Remove like count in Posts and Comments - list of changed endpoints:
```
POST /posts/{postid}/like
DELETE /posts/{postid}/like
GET /streams/{streamid}/posts (on page loading)
POST /comments/{id}/like
DELETE /comments/{id}/like
```
### Remove “People who like this” popup on Web  - list of changed endpoints:
```
GET /posts/{postid}/likes
```
### Remove Like count in the User Profile
**List of changed endpoints:**
```
GET /profiles/{name}
```
**List of changed files**  
> common/beekeeper/common/resources/profile.py  

**Comment:**
Like count information on the User Profile in web application would be equal zero. 
Function return 0 like everywhere as count like.

### Remove notification - list of changed endpoints:
```
POST /posts/{postid}/like
DELETE /posts/{postid}/like
POST /comments/{id}/like
DELETE /comments/{id}/like
```

### Comment for the *Slideshow*  
Slideshow in directly connection with Posts and Comments.