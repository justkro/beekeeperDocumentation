# Rich text formatting

## Background and Objectives
The purpose of this feature is to enable usage of rich formating for the posts and streams.

## Feature flag
New feature flag **rich_text_in_posts** is to be created which will controll enrolment of this functionality. 

## Functionality
A new field `html` is added to requests/responses containing the rich version of post. `text` is kept unchanged because of backward compatibity.
A new content types are added `application/vnd.io.beekeeper.post+json;version=2` for single post and `Content-Type: application/vnd.io.beekeeper.posts+json;version=2
` multiple of posts. These should be used in `Content-Type` and `Accept` headers in adition to feature flag being enabled for rich text to be used.

### Composing posts with rich texts on the web application
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
Changes in these endpoints are related to composing posts with rich text and mention people in rich text post.
Compose post not supported on mobile applications. Only supports rich text in the web application.  
Added class ```AuthenticatedPostResource```. 
In ```is_mobile_without_rich_text``` function for mobile version newer than 7.24 add support for displaying rich text.
```get_post_content``` function processes exceptions and checks appropriate request headers. 
If html field is available, function calls ```get_mentioned_users_in_rich_text```, ```convert_emojis``` and ```html_to_plain```.
It is important that these 3 functions are called in the specified order.  
```html_to_plain``` function converts html to plain text to support legacy applications. 
Conversion was done based on the instructions from [html formatting](https://docs.google.com/document/d/1NLqT_AH4LFckNPTEgXLO6tbgTgxGDEsaAMujrNs2xxM/edit#heading=h.j14kso86812h).  
For better understanding HTMLConverter class please first read [documentation](https://docs.python.org/3/library/html.parser.html)  
```is_html``` for recording the fact if the content was generated from a rich text editor.


### See RTF posts formatted correctly on the web application
*List of changed endpoints:*
```
GET /api/2/posts
GET /api/2/streams/{streamid}/posts
GET /api/2/streams/{streamid}/labels/{labels}/posts
```
*List of changed files*  
> api/beekeeper/api/resources/postsv2.py  
> common/beekeeper/common/resources/posts.py
> common/beekeeper/common/utils/html_converter.py  
> common/beekeeper/common/subdomains/stream/model.py

*Comment:*  
Return response with html field. If post doesn't have html field, function ```text_to_html``` converts plain to rich text. 

###  Edit posts with rich text on the web application
*List of changed endpoints:*
```
PUT /api/2/posts/{postid}
```
*List of changed files*  
> api/beekeeper/api/resources/postsv2.py  
> common/beekeeper/common/resources/posts.py

*Comment:*  
Update post, added support for rich-text, add html field in response.

### See posts in rich-text formatting in web app Profile page 

*List of changed endpoints:*
```
GET /profiles/{name}
```
*List of changed files*  
> api/beekeeper/api/resources/profilesv2.py  
> common/beekeeper/common/resources/profile.py

*Comment:*  
Return html field on web app profile page if feature flag enabled.

### Translate the rich text content
*List of changed endpoints:*
```
GET /translations/post/{post_id}
```
*List of changed files*  
> api/beekeeper/api/resources/translationsv2.py  
> common/beekeeper/common/resources/inline_translations/translation_resource.py  

*Comment:*  
Translate rich text. Add html variable in list for translation.

### Other endpoints

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
All mentioned endpoints support rich text when accept header is set correctly and the feature flag enabled.
