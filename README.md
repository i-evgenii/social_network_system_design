# System design: a social network for travelers
This page contains homework for the System Design course.

### Business requirements:
- publication of travel posts with photographs, a short description and reference to a specific travel location;
- rating and comments on posts of other travelers;
- subscribe to other travelers to monitor their activity;
- search for popular places to travel and view posts from these places in the form of TOP places by country and city;
- communication with other travelers in private messages;
- viewing feeds of other travelers.

### Functional requirements:
- Authentication, roles (administrator/moderator, company, individual user);
- Creation of posts (text and media);
- Creating comments, reactions (emoticons);
- Blocking comments on your posts;
- Create connections between users (to track posts);
- Ability to send private messages;
- Post feed on the main profile page;
- Search and filter vacation spots.

### Non-functional requirements:
- CIS audience;
- DAU 10,000,000;
- Possibility of automatic horizontal scaling;
- Site usage averages 1 time per day by 1 user;
- On average, there are 10 posts in a user’s feed.

## Basic calculations
- RPS (main user page) = 10 000 000 * 1 / 86 400 ~= 115
- RPS (loading posts) = 10 000 000 * 10 / 86 400 ~= 1150