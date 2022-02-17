# Disable Like Count Feature Flag

### List of changed endpoints
Remove like count in Post and Comments - list of changed endpoints:
```
POST /posts/{postid}/like
DELETE /posts/{postid}/like
GET /streams/{streamid}/posts (on page loading)
POST /comments/{id}/like
DELETE /comments/{id}/like
```
Remove “People who like this” popup on Web  - list of changed endpoints:
```
GET /posts/{postid}/likes
```
Remove Like count in the User Profile - list of changed endpoints:
```
GET /profiles/{name}
```
Remove notification - list of changed endpoints:
```
POST /posts/{postid}/like
DELETE /posts/{postid}/like
POST /comments/{id}/like
DELETE /comments/{id}/like
```
 