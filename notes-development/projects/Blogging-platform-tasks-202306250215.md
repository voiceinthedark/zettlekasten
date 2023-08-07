---
title: Blogging-platform-tasks
date: 25/06/2023
tags: project blogging-platform tasks
---

# **Blogging-platform-tasks** 202306250215 
> **48a886**

> Added to my [[projects-timeline]]
  
### Progress

**Total Task Count:** 95
**Finished Task Count:** 74
**Completion Percentage:** 77.89%

## Tasks

- [x] Setup database and database connections
- [ ] Registration system
  - [x] Create user registration functionality with validation
  - [x] Implement user authentication
  - [ ] Implement user roles
- [x] User Management
  - [x] Add User profile page
    - [x] Show user information
    - [x] Show users articles
    - [x] Show users latest comments
  - [x] Add user Followership
    - [x] Add user Notification when new posts are published
- [x] Main Page Management
  - [x] Create main page with sidebars and search field
  - [x] List posts by date published
  - [x] Implement pagination for posts
- [ ] Blog Post Management
  - [x] Create database schema table and set up relationships
  - [x] Implement CRUD for blog posts
    - [x] Add Create Post
    - [x] Add Delete Post
      - [ ] Add Delete Confirmation
    - [x] Add Edit/Update Post
    - [x] Add Show Post
  - [ ] Implement blog post sharing
  - [x] Add validation for blog post fields
  - [x] Implement pagination for posts list
- [x] Blog Post Editor
  - [x] Allow user to create edit and update posts in rich text editor
  - [x] Implement image uploads and handling within the post (markdown?)
  - [x] Add support for tags and categories to organize blog posts
  - [x] Add word count for post, and calculate minutes to read.
- [x] Frontend Design and layout
  - [x] Create a visually appealing design using Tailwindcss
  - [x] Create reusable components using tailwindcss
  - [x] Implement dynamic ui Design using Alpinejs (dropdowns, modals etc.)
- [ ] Commenting system
  - [x] Add a commenting system where users can comments and reply to existing comments
  - [x] Add comment threading and pagination
  - [ ] Implement validation and moderation for user comments
- [x] Dashboard and Profile
  - [x] Add dashboard for users to create new posts and manage their profile information
  - [x] Add Post Listing for login user posts
  - [x] Allow users to edit their profile details
  - [x] Provide statistics and analytics for users to track their blog post performance
- [x] Search functionality
  - [x] Implement a search feature to allow users to search for blog posts based on keywords
  - [x] Search based on tags
  - [x] Search based on categories
  - [x] Configure search indexing and integration with a search engine (e.g., Elasticsearch or Algolia)
- [x] Following system
  - [x] Create User_Followers table (many2many)
  - [x] Enable user follow and unfollow functionality
  - [x] Implement methods for followers and following retrieval.
  - [x] Display Following and followers on profile page
  - [x] Display following and followers on popup card for user
- [ ] Feed and activity system
  - [ ] Implement a feed or activity stream of posts, updates, or other content from the users a user is following
- [x] Likes and dislikes System
  - [x] Create a Likes table
  - [x] Enable Like/Dislike actions
  - [x] Retrieve like and dislike for a post
  - [x] Retrieve users who liked\disliked the post
  - [x] Display likes and dislikes on Post pages
  - [x] Provide a way for users to view the list of users who liked or disliked a post
  - [x] Perform a security check to ensure that users can only perform like or dislike actions once per post
- [x] Comments Like and Dislike System
  - [x] Create a Comments_Like table
  - [x] Enable Like/Dislike actions
  - [x] Retrieve like and dislike for a comment
  - [x] Retrieve users who liked\disliked the comment
  - [x] Display likes and dislikes on Comment pages
  - [x] Provide a way for users to view the list of users who liked or disliked a comment
  - [x] Perform a security check to ensure that users can only perform like or dislike actions once per comment
- [ ] Recommendation System
  - [ ] Add collaborative filtering
  - [x] Add content based filtering
- [ ] Messaging system
  - [x] Create Direct Messaging table
  - [x] Allow users to send messages
  - [x] UI where users can view and send messages
  - [x] Sort messages by date
  - [x] Sort message content by date
  - [x] Display message history
  - [ ] Implement notifications for new messages
  - [ ] Add mail notifications
  - [ ] Add in-app notification
  - [ ] Add real-time notification (websockets)
  - [ ] Implement a security check to ensure that only authorized users can send messages
- [ ] Security and Permissions
  - [ ] Implement role-based access control (RBAC) to restrict certain actions and features based on user roles
  - [x] Add CSRF protection and input validation to prevent security vulnerabilities
  - [x] Implement authorization checks for user actions, such as editing or deleting blog posts
- [ ] Testing 
  - [ ] Implement Unit testing and integration testing


[//begin]: # "Autogenerated link references for markdown compatibility"
[projects-timeline]: ../../notes/projects-timeline "Projects Timeline"
[//end]: # "Autogenerated link references"