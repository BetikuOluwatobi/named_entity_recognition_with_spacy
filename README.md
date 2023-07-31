# Named Entity Recognition (NER) on Investing Subreddit Data with SpaCy and Sentiment Analysis with Flair

This project applies Named Entity Recognition (NER) using SpaCy on the Investing Subreddit data, and sentiment analysis using Flair to analyze customer sentiment on different company stocks.

## Getting Started

### Prerequisites

Ensure you have installed the necessary Python libraries: requests, pandas, spacy, and flair. Also, ensure you have access to Reddit API credentials.

### Data Collection

Data is pulled from the Investing subreddit using Reddit API which requires HTTP basic authentication. The extracted data includes post time, content, title, upvote ratio, score, and URL. The code snippet below shows how to make the API call:

```python
auth = requests.auth.HTTPBasicAuth(auth_tok['client_id'], auth_tok['secret'])
data = {'grant_type': 'password',
        'username': 'your_reddit_username',
        'password': auth_tok['password']}
headers = {'User-Agent': "app_name/0.0.1"}
access = requests.post("https://www.reddit.com/api/v1/access_token", auth=auth, data=data, headers=headers)
headers['Authorization'] = f"bearer {access.json()['access_token']}"
api = "https://oauth.reddit.com/"
res = requests.get(f"{api}/r/investing/new", headers=headers, params={'limit': '100'})
```

The returned data is stored in a Pandas DataFrame for further analysis.

### Named Entity Recognition

Entities are extracted from the text data using SpaCy's `en_core_web_sm` model. It identifies 'organization' entities in the post content.

### Sentiment Analysis

The Flair library is used for sentiment classification. It provides a pre-trained sentiment analysis model `en-sentiment`, which classifies the sentiment of each post as positive or negative. The sentiment scores are appended to the data frame.

## Conclusion

This project uses Named Entity Recognition and sentiment analysis to extract insights from subreddit posts about investing. The results provide a snapshot of current market sentiments towards different companies based on Reddit posts. The code and steps presented here can be adapted to analyze any subreddit or text corpus for similar insights.
