
## Basic Idea
 ### About database
 handle Instagram posts image urls and other post metadata. Created a table called `mutual_follows` to find the intersection between followers. Added a trigger `update_mutual_follows_trigger` to update the mutuals mapping on an upsert in the following/follower list. 

 ### About Scraper
implemented user metadata scraping, got user posts and metadata for better interests extraction since there may be cases where posts are more descriptive about a user's interest(like art and traveling).



## Setup

### Prerequisites

- Python 3.8+
- PostgreSQL database
- Instagram account credentials
- OpenAI API key

### Installation

1. Clone this repository:

```bash
git clone https://github.com/tawishicodes/six_scrapping-
cd six_scrapping-


```

2. Install required packages:

```bash
pip install -r requirements.txt
```

3. Set up environment variables in `.env` file:

```
INSTAGRAM_USERNAME=your_instagram_username
INSTAGRAM_PASSWORD=your_instagram_password

DB_USER=your_db_user
DB_PASSWORD=your_db_password
DB_HOST=localhost
DB_PORT=5432
DB_NAME=instagram

OPENAI_KEY=your_openai_api_key
```

4. Set up the database:

```bash
psql -U your_db_user -d instagram -f database/create_db.sql
```

## Available Scripts

### 1. One-Shot Analysis

Merged the functionalities of scrapers, interest classifier in one script.

```bash
python one_shot.py
```

- You'll be prompted for all required information

### 2. Post Scraper

Scrapes recent posts, their captions, likes and other metadata from Instagram profiles.

```bash
python post_scraper.py
```

- You'll be prompted to enter Instagram usernames (comma-separated)
- Enter the number of posts to scrape
- Choose whether to save data to the database

### 3. Follow Scraper

Scrapes followers and following lists from Instagram profiles. Please set this number to small amount or it will take a lot of time

```bash
python follow_scraper.py
```

- You'll be prompted to enter Instagram usernames (comma-separated)
- Enter the number of followers/following to scrape (or "all")
- Optionally use a proxy server to avoid rate limiting

### 4. Interest Analysis

Analyzes posts and following lists to predict user interests using OpenAI's GPT model.

```bash
python interest.py <username>
```


### 5. Batch Interest Analysis

Analyzes a user's interests in batches to handle large following lists.

```bash
python batch_interest.py <username>
```


- You'll be prompted to enter a batch size (default: 20)

### 6. Mutual Followers Analysis

Finds mutual followers between two Instagram users.

```bash
python get_mutual_followers.py <username1> <username2>
```

## Data Flow

1. Scrape posts with metadata, followers, and following data from Instagram
2. Store data in PostgreSQL database
3. Analyze images and captions using AI to determine interests
4. Process following list data to refine interest predictions
5. Output predicted interests


