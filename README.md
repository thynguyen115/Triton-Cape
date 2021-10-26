# Triton-CAPE
Unit 8: Group Milestone - README - CAPE app
===

:::info
**Below is an example** of what your **Group Project README** should include and how it should be structured for the **Unit 8 Group Milestone Submission**.
:::

#

## Table of Contents
1. [Overview](#Overview)
1. [Product Spec](#Product-Spec)
1. [Wireframes](#Wireframes)

## Overview
### Description
Our App provides student the information about all the past courses in UCSD, including the instructor evaluations and course evaluations. The users can search for the information with the course number and instructor's name easily.  

### App Evaluation
- **Category:** Education
- **Mobile:** The computer version for this app has been created by UCSD. Hence, we are looking forward to making a mobile version for this app. 
- **Story:** Analyze how students from past quarters evaluated their Professors and TAs; Give students some insights about how the classes were conducted; Allow students to decide whether or not they should take the class with a particular instructor, etc.
- **Market:** UCSD students are the major group that will use this app. Instructors, on the otherhand, can also take a look at this app to understand more about the students' experience and adjust their teaching style accordingly
- **Habit:** This app can be use whenever students/instructors feel needed. However, most people will use this app when the class schedule is out, and/or when students register new classes.
- **Scope:** This app is defined very clearly. It helps the users to get help information about evaluations of all courses at UCSD.

## Product Spec
### 1. User Stories (Required and Optional)

**Required Must-have Stories**
* Users see app icons on the home and launch screen
* Users can login / logout to save their personal info & favorite CAPEs [i.e. Twitter, unit 3]
* Users can search for the information of courses by instructor's name or course number
* Users can see the instructor's name and his/her CAPE summary

**Optional Nice-to-have Stories**
* Users can "favorite" a CAPE post [i.e. Twitter, unit 4]
* Users can leave new comments (new evaluation) [i.e. Twitter, unit 4]

### 2. Screen Archetypes

* Login 
* Register - User signs up or logs into their account
   * Upon Download/Reopening of the application, the user is prompted to log in to gain access to their profile information to be properly matched with another person. 
   * ...
* Profile Screen 
   * Allows user to upload a photo and fill the information that they want to share
* CAPE Selection Screen.
   * Allows users to pick their desired class / course ID / instructor

### 3. Navigation

**Tab Navigation** (Tab to Screen)

* Profile
* Home page

Optional:

**Flow Navigation** (Screen to Screen)
* Forced Log-in -> Account creation if no log in is available
* Home search -> Jumps to course selection page
* Choose Course -> Course Detail page 
* profile -> profile page 

## Wireframes
![](https://i.imgur.com/egpDpyY.png)

## [BONUS] Interacive Prototype
<img src='https://i.imgur.com/6INVQaP.gif' title='Video Walkthrough' width='250' alt='Video Walkthrough' />

### [BONUS] Digital Wireframes & Mockups
![](https://i.imgur.com/egpDpyY.png)

## Schema 
### Models
#### Post

   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | objectId      | String   | unique id for the user post (default field) |
   | author        | Pointer to User | post author |
   | rating        | Number   | rating that the user gives |
   | review        | String   | review by author |
   | reviewCount   | Number   | number of reviews that has been posted to a course |
   | ratingsCount  | Number   | number of ratings for the course |
   | createdAt     | DateTime | date when post is created (default field) |
   | updatedAt     | DateTime | date when post is last updated (default field) |
### Networking
#### List of network requests by screen
   - Home Feed Screen
      - (Read/GET) Query all posts where user is author
         ```swift
         let query = PFQuery(className:"Post")
         query.whereKey("author", equalTo: currentUser)
         query.order(byDescending: "createdAt")
         query.findObjectsInBackground { (posts: [PFObject]?, error: Error?) in
            if let error = error { 
               print(error.localizedDescription)
            } else if let posts = posts {
               print("Successfully retrieved \(posts.count) posts.")
           // TODO: Do something with posts...
            }
         }
         ```
      - (Create/POST) Create a new rating on a post
      - (Delete) Delete existing rating
      - (Create/POST) Create a new review on a post
      - (Delete) Delete existing review
   - Create Post Screen
      - (Create/POST) Create a new Post object
   - Profile Screen
      - (Read/GET) Query logged in user object
      - (Update/PUT) Update user profile info
