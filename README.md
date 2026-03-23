# Yelp Restaurant Review Sentiment & Topic Analyzer

A Python-based tool that fetches restaurant reviews from the Yelp Fusion API and performs emotion/sentiment analysis using the NRC Emotion Lexicon.

## Overview

This project allows you to:

1. **Search restaurants** near any location using the Yelp Fusion API
2. **Fetch reviews** for each restaurant found
3. **Analyze emotions** in the review text across 8 dimensions: Fear, Trust, Negative, Positive, Joy, Disgust, Anticipation, Sadness, and Surprise
4. **Compare sentiment** across multiple restaurants in a structured DataFrame

## How It Works

- The Yelp API is queried for restaurants near a given address
- For each restaurant, review snippets are retrieved via the `/v3/businesses/{id}/reviews` endpoint
- Each review is analyzed word-by-word against the [NRC Emotion Lexicon](https://saifmohammad.com/WebPages/NRC-Emotion-Lexicon.htm), which maps words to emotions
- Emotion scores are normalized by total word count, producing a comparative emotion profile per restaurant

## Example Output

```
restaurant   fear  trust  negative  positive  joy  disgust  anticip  sadness  surprise
Flat Top     0.00  0.03   0.01      0.03      0.01 0.00     0.01     0.01     0.00
Thai Market  0.00  0.06   0.00      0.07      0.06 0.00     0.02     0.00     0.00
KALBI        0.00  0.10   0.01      0.10      0.09 0.00     0.05     0.00     0.04
```

## Setup

### Prerequisites

- Python 3.x
- A [Yelp Fusion API Key](https://www.yelp.com/developers/documentation/v3)
- NRC Emotion Lexicon data file

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/Yelp-Restaurant-Review-Sentiment-Topic-Analyzer.git
   cd Yelp-Restaurant-Review-Sentiment-Topic-Analyzer
   ```

2. Install dependencies:
   ```bash
   pip install requests pandas
   ```

3. Create a `.env` file in the project root with your Yelp API credentials:
   ```
   CLIENT_ID=your_client_id
   API_KEY=your_api_key
   ```

## Usage

Open the Jupyter notebook and use the main function:

```python
# Analyze restaurants near any address
results = analyze_nearby_restaurants("Columbia University, New York, NY", number=15)
```

This returns a pandas DataFrame with emotion scores for each restaurant, making it easy to sort, filter, and visualize results.

## Key Functions

| Function | Description |
|---|---|
| `get_restaurants(api_key, location, number)` | Fetches nearby restaurants from Yelp |
| `get_business_review(api_key, business_id)` | Retrieves review text for a specific business |
| `get_reviews(location, number)` | Combines restaurant search and review fetching |
| `emotion_analyzer(text)` | Analyzes a text string for 8 emotion dimensions |
| `comparative_emotion_analyzer(text_tuples)` | Produces a DataFrame comparing emotions across multiple texts |
| `analyze_nearby_restaurants(address, number)` | End-to-end pipeline: location in, emotion DataFrame out |

## Technologies

- **Yelp Fusion API** - Restaurant search and review data
- **NRC Emotion Lexicon** - Word-level emotion classification
- **pandas** - Data analysis and tabular output
- **Jupyter Notebook** - Interactive development environment
