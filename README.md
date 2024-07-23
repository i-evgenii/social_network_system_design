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
- Authentication;
- Creation of posts (text and media);
- Adding comments to your own and other people's posts
- Ability to send private messages;
- Post feed on the main profile page;
- Search and filter vacation spots.

### Non-functional requirements:
- CIS audience;
- DAU 10,000,000;
- Possibility of automatic horizontal scaling;
- Site usage averages 1 time per day by 1 user;
- On average, there are 10 posts in a user’s feed;
- Availability 99.95;
- A seasonal load (summer, New Year, long weekends).

### Basic calculations
- RPS (viewing main user page) = 10 000 000 * 1 / 86 400 ~= 115
- RPS (viewing other user posts) = 10 000 000 * 10 / 86 400 ~= 1150
- RPS (creating posts) = 10 000 000 * 0.1 / 86 400 ~= 12
- Traffic = 1277 * 100Kb = 128Mb/s
- Connections = 10 000 000 * 0.1 = 1 000 000

### Storage calculations
- Projected chats data volume per year ~= 12 * 2Kb * 86400 * 365 ~= 760Gb
- Projected chats number of iops ~= 3Mb/s / 4Kb ~= 750
- Disks_for_capacity = 760 Gb / 512 Gb  ~= 2
- Disks_for_throughput = 3 Mb/s / 500 Mb/s = 0.006
- Disks_for_iops = 750 / 1000 = 0.75
- Disks = max(ceil(2), ceil(0.006), ceil(0.75)) = 2

- Projected comments data volume per year ~= 12 * 6Kb * 86400 * 365 ~= 2.3Tb
- Projected comments number of iops ~= 9Mb/s / 4Kb ~= 2300
- Disks_for_capacity = 2.3 Tb / 2 Tb  ~= 2
- Disks_for_throughput = 9 Mb/s / 500 Mb/s ~= 0.01
- Disks_for_iops = 2300 / 1000 = 2.3
- Disks = max(ceil(2), ceil(0.01), ceil(2.3)) = 3

- Projected media data volume per year ~= 12 * 80Kb * 86400 * 365 ~= 30Tb
- Projected media number of iops ~= 120Mb/s / 4Kb ~= 30000
- Disks_for_capacity = 30 Tb / 2 Tb  ~= 15
- Disks_for_throughput = 120 Mb/s / 500 Mb/s ~= 0.24
- Disks_for_iops = 30000 / 1000 = 30
- Disks = max(ceil(15), ceil(0.24), ceil(30)) = 30

- Projected messages data volume per year ~= 12 * 2Kb * 86400 * 365 ~= 1.5Tb
- Projected messages number of iops ~= 6Mb/s / 4Kb ~= 1500
- Disks_for_capacity = 1.5 Tb / 512 Gb  ~= 3
- Disks_for_throughput = 6 Mb/s / 500 Mb/s ~= 0.01
- Disks_for_iops = 1500 / 1000 = 1.5
- Disks = max(ceil(3), ceil(0.01), ceil(1.5)) = 3

- Projected posts data volume per year ~= 12 * 6Kb * 86400 * 365 ~= 2.3Tb
- Projected posts number of iops ~= 9Mb/s / 4Kb ~= 2300
- Disks_for_capacity = 2.3 Tb / 2 Tb  ~= 2
- Disks_for_throughput = 9 Mb/s / 500 Mb/s ~= 0.01
- Disks_for_iops = 2300 / 1000 = 2.3
- Disks = max(ceil(2), ceil(0.01), ceil(2.3)) = 3

- Projected users data volume per year ~= 12 * 2Kb * 86400 * 365 ~= 760Gb
- Projected users number of iops ~= 3Mb/s / 4Kb ~= 750
- Disks_for_capacity = 760 Gb / 512 Gb  ~= 2
- Disks_for_throughput = 3 Mb/s / 500 Mb/s = 0.006
- Disks_for_iops = 750 / 1000 = 0.75
- Disks = max(ceil(2), ceil(0.006), ceil(0.75)) = 2

### Hosts calculations
- Replication factor = 2
- Replication = master-slave/sync
- Sharding = key based by user_id
- 5 SSD per 8Tb (2x factor)
- 5 shards with 1 SSD per 8Tb (2x factor)