# Rich text formatting

## Background and Objectives


### Composing posts with rich texts on the web application
As a User, I want to be able to compose posts with rich texts on the web application.
As a User, I want to be able to mention people in my rich text post
As a User, I want to be able to see the changes on a rich text post real time
As a User, I want to be able to add links to my rich text post
*List of changed endpoints:*
```
POST /api/2/posts
GET /api/2/posts/{postId}
POST /api/2/streams/{streamid}/posts
```
*List of changed files*  
> api/beekeeper/api/resources/postsv2.py  
> common/beekeeper/common/resources/posts.py  
> common/beekeeper/common/subdomains/stream/model.py  
> api/beekeeper/api/resources/base.py  
> common/beekeeper/common/mentions.py  
> common/beekeeper/common/utils/html_converter.py  
> api/beekeeper/api/resources/wsgi_errors.py

*Comment:*  
OVDE KOMENTAR

### See RTF posts formatted correctly on the web application
As a User, I want to be able to see the posts formatted correctly on the web application.
*List of changed endpoints:*
```
GET /api/2/posts
GET /api/2/streams/{streamid}/posts
GET /api/2/streams/{streamid}/labels/{labels}/posts
```
*List of changed files*  
> api/beekeeper/api/resources/postsv2.py  
> common/beekeeper/common/resources/posts.py

*Comment:*

###  Edit posts with rich text on the web application
As a User, I want to be able to edit posts with rich text on the web application.
*List of changed endpoints:*
```
PUT /api/2/posts/{postid}
```
*List of changed files*  
> api/beekeeper/api/resources/postsv2.py  
> common/beekeeper/common/resources/posts.py

*Comment:*

### See posts in rich-text formatting in web app Profile page 
As a User, I want to see posts in rich-text formatting in my web app Profile page
*List of changed endpoints:*
```
GET /profiles/{name}
```
*List of changed files*  
> api/beekeeper/api/resources/profilesv2.py  
> common/beekeeper/common/resources/profile.py

*Comment:*

### Translate the rich text content
As a User, I want to be able to translate the rich text content on all platforms.
*List of changed endpoints:*
```
GET /translations/post/{post_id}
```
*List of changed files*  
> api/beekeeper/api/resources/translationsv2.py  
> common/beekeeper/common/resources/inline_translations/translation_resource.py
*Comment:*

### Other endpoints
All below mentioned endpoints support rich text when accept header is set correctly and the feature flag enabled.
*List of changed endpoints:*
```
POST '/posts/{postid}/subscribe
DELETE '/posts/{postid}/subscribe
GET /posts/favorites
GET /posts/suggestions
POST /posts/{postid}/like
DELETE /posts/{postid}/like
POST /posts/{post_id}/move
POST /posts/{post_id}/vote/{option_id}
POST posts/{postid}/report
POST /posts/{postid}/favorite
DELETE /posts/{postid}/favoritePOST /posts/{postid}/keep
```
*List of changed files*  
> api/beekeeper/api/resources/postsv2.py  
> common/beekeeper/common/resources/posts.py  
> common/beekeeper/common/resources/digest_mail.py
*Comment:*

