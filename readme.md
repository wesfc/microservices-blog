# Study Case - Microservices & React
This study case focus on how to Microservices works and communicates with each others.
The communication occurs in the following way:

1 - All Posts and Comments emits an event to Event-Bus (PostCreated|CommentCreated|CommentUpdated).

2 - Event-Bus receives the events and transmit them to all microservices on route /events.

3 - Each application is able to handle events, but the main application that will handle them is Query Service.

4 - QueryService handle events and joins data from Post + respective post comments in a data structure to be consumed by UI Client.

## Microservices running

### UI Client
Simple UI using React framework. Creates and show posts and their respectives comments.

### Posts
Service responsible to handle posts.

Events emmited by this service: **PostCreated**

**PostCreated:** When a post is created on Blog.

### Comments
Service responsible to handle comments - Create and Update comments.

The comments of this application has three states: **pending | approved | rejected** (when comment includes the word 'orange').

Events emmited by this service: **CommentCreated | CommentModerated | CommentUpdated**

**CommentCreated:** When a comment is added in a Post.

**CommentModerated:** Received from Moderation Microservice when comment is approved or rejected.

**CommentUpdated:** Event with current status (approved|rejected) sent to be updated on Query Service.

### Event-Bus
Service to simulate an Event Broker - Receives events through HTTP and emit them for all microservices.

### Moderation
Service responsible to moderate all comments - 'orange' is now allowed word, rejects all comments that includes the prohibited word.


### Query Service
Service responsible to handle Posts and Comments and persist them in memory in easy way to be consumed by Client Service.