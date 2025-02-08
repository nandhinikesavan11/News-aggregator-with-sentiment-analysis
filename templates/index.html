from flask import Flask, render_template, request
import feedparser
from datetime import datetime
from nltk import download
from nltk.sentiment.vader import SentimentIntensityAnalyzer
from nltk.tokenize import sent_tokenize

# Download necessary NLTK data files
download('vader_lexicon')
download('punkt')

# Initialize Flask app
app = Flask(__name__)

# Initialize sentiment analyzer
sentiment_analyzer = SentimentIntensityAnalyzer()

# RSS Feeds for various categories
RSS_FEEDS = {
    "world": "http://feeds.bbci.co.uk/news/world/rss.xml",
    "politics": "http://feeds.bbci.co.uk/news/politics/rss.xml",
    "entertainment": "http://feeds.bbci.co.uk/news/entertainment_and_arts/rss.xml",
    "sports": "http://feeds.bbci.co.uk/sport/rss.xml",
    "technology": "http://feeds.bbci.co.uk/news/technology/rss.xml",
    "fashion": "https://www.vogue.com/rss",
    "stories": "http://feeds.bbci.co.uk/news/stories/rss.xml",
}

# Helper function to fetch and parse RSS feeds with pagination
def fetch_news(category, page=1, per_page=50):
    feed = feedparser.parse(RSS_FEEDS[category])
    news_items = feed.entries  # Get all items from the RSS feed
    # Sort news by published date in descending order (latest first)
    news_items.sort(key=lambda x: x.get("published_parsed"), reverse=True)
    
    # Paginate the news items
    start_index = (page - 1) * per_page
    end_index = start_index + per_page
    return news_items[start_index:end_index], len(news_items)  # Return news items for this page and total count

# Helper function to summarize news content
def summarize_content(content, summary_length=3):
    sentences = sent_tokenize(content)
    return ' '.join(sentences[:summary_length])

# Helper function to determine the sentiment of the news
def analyze_sentiment(content):
    score = sentiment_analyzer.polarity_scores(content)
    if score["compound"] >= 0.05:
        return "Positive"
    elif score["compound"] <= -0.05:
        return "Negative"
    else:
        return "Neutral"

# Route for the homepage with pagination
@app.route("/", methods=["GET", "POST"])
def index():
    selected_category = request.form.get("category", "world")
    selected_sentiment = request.form.get("sentiment", "all")
    current_page = int(request.args.get("page", 1))  # Default to page 1 if not specified

    # Fetch and sort news based on category and page
    news_items, total_items = fetch_news(selected_category, current_page)
    total_pages = (total_items // 50) + (1 if total_items % 50 != 0 else 0)  # Calculate total pages

    formatted_news = []

    # Format news items with summary, publication date, and sentiment
    for item in news_items:
        summary = summarize_content(item.description)
        published_time = datetime(*item.published_parsed[:6]).strftime("%Y-%m-%d %H:%M:%S") if item.published_parsed else "Unknown"
        sentiment = analyze_sentiment(summary)

        formatted_news.append({
            "title": item.title,
            "link": item.link,
            "summary": summary,
            "published": published_time,
            "sentiment": sentiment
        })

    # Filter news items based on selected sentiment, if applicable
    if selected_sentiment != "all":
        formatted_news = [item for item in formatted_news if item["sentiment"] == selected_sentiment]

    return render_template("index.html", news=formatted_news, categories=RSS_FEEDS.keys(), category=selected_category, sentiment=selected_sentiment, current_page=current_page, total_pages=total_pages)

if __name__ == "__main__":
    app.run(debug=True)