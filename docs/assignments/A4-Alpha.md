---
title: Assignment 4 Alpha
layout: doc
---

# Assignment 4 Alpha

## ADTs

### <b>Concept: </b> Relationshipping  [User]
<b>Purpose: </b> Allow users to create their own relationships  
<b>Principle: </b> After creating a relationship and assigning creator and targets, looking up that pair will yield the relationship.  
<b>State: </b>  
relationTypes: creator -> relationship  
relatedUsers: relationship -> target   
<b>Actions: </b>  
* createRelationship(creator: User, relationship: String): relates creator to new relationship in relationTypes
* relate(creator: User, target: User, relationship: String): relates selected relationship under creator to target and removes instances of that target from other relationships (for the same creator)  
* deleteRelationship(creator: User, relationship: String): removes a relationship from relationTypes  
* getRelationship(creator: User, target: String): returns relationships that relates creator to target

### <b>Concept: </b> Privacy Controlling [Thing]  
<b>Purpose: </b> Control what users can see  
<b>Principle: </b> After creating a privacy attribute for an thing and assigning a vlue, one can check and find that atrribute and value using the thing  
<b>State: </b>  
privacyAttribute: thing -> String
privacyValue: privacyAttribute -> String  
<b>Actions: </b>  
* createAttribute(thing: Thing, attribute: String): relates attribute with thing in attributes 
* assignAttribute(thing: Thing, attribute: String, value: String): relates value with attribute related to thing 
* satisfies(thing: Thing, {checkAttribute: String, checkValue: String}*): returns True if checkAttribute is not related to thing or if checkValue is related to checkAttribute related to thing, else False.
* deleteAttribute(thing: Thing, attribute: String): unrelates attribute with thing in privacyAttribute  

### <b>Concept: </b> Posting [Content]
<b>Purpose: </b> Allow users to create content for others to see  
<b>Principle: </b> After adding a piece of content it can be found using its creator  
<b>State: </b>  
post: set Posts
content: post -> <b>one</b> Content  
creator: post -> <b>one</b> User  
<b>Actions: </b>  
* createPost(content: Content, user: User): creates an id, adds it to the set of posts, and relates it to content and its user
* updatePost(post: Post, content: Content): changes content associated with post to content  
* deletePost(post: Post): removes post from post and content
* getPosts(user: User): returns all posts related to user  
* getCreator(post: Post): returns creator related to post

### <b>Concept: </b> Collaborating [Object, User]
<b>Purpose: </b> Allows users besides the creator to edit objects  
<b>Principle: </b> After being added to the list of collaborators for an object, one can find that collaborator in the list by using the object  
<b>State: </b>     
collaborators: Object -> user  
<b>Actions: </b>  
* addColab(user: User, object: Object): relates user to object in collaborators  
* removeColab(user: User, object: Object): removes relation between user and object in collaborators  
* checkColab(user: User, object: Object): returns if the user is a collaborator on an object  

### <b>Concept: </b> Inviting [Thing, User]
<b>Purpose: </b> Allows users to send invites to other users to accept or decline  
<b>Principle: </b> After sending an invite for a Thing to target, target can be found using Thing  
<b>State: </b>  
invites: user -> Thing  
<b>Actions: </b>  
* inviteUser(user: User, thing: Thing): relates user to Thing in invites  
* deleteInvite(user: User, thing: Thing): unrelates user to Thing in invites  
* checkInvites(user: User): returns all relations to user in invites  

### <b>Concept: </b> Content Communitying [Object]
<b>Purpose: </b> Create communities where content can be assigned
<b>Principle: </b> After a community is created and an object is added, that object can be found using the community 
<b>State: </b>  
community: set Community
posts: community -> Object  
<b>Actions: </b>  
* createCommunity(community: Community): adds community to set
* addObject(community: Community, object: Object): relates community and object
* removeObject(community: Community, object: Object): unrelates community and object
* getPosts(community: Community): returns all objects related to a community

### <b>Concept: </b> Replying [Object]
<b>Purpose: </b> Content can be created as a response to other content  
<b>Principle: </b> After adding an object and selecting an object to reply to, the new object can be found using the other object  
<b>State: </b>  
reply: set Reply 
replies: Object -> reply  
<b>Actions: </b>  
* addReply(reply: Object): adds reply to the set of objects  
* removeReply(reply: Object): deletes reply from the set of objects  
* assignReply(object: Object, reply:Reply): relates reply with object in replies  
* removeReply(object: Object, reply:Reply): unrelates reply with object in replies   

### Generics:
User: user from authing
Content: Different content types coming from unlisted content creation concepts  
Object: Post, Reply  
Thing: Object, Content Community

### Graph:
![Diagram](images/A4/A4graph.jpg)

## Backend Repository
https://github.com/e-harbaugh/6.1040-backend
## Deployed Service
https://6-1040-backend-omega.vercel.app/