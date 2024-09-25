## Sentiment Analysis of Election Candidates: Donald Trump and Kamala Harris

This project analyzes social media sentiments surrounding the elections of Donald Trump and Kamala Harris. Using Python libraries like `TextBlob` and `VADER SentimentIntensityAnalyzer`, the dataset is processed to classify public opinions about the candidates into three categories: positive, neutral, and negative.

## Key Features:
- **Tweet Scraping**: Uses `nscrapper` to collect tweets related to Trump and Harris.
- **Lexical Diversity**: Analyzes the variety of words used in the dataset.
- **Sentiment Analysis**: Applies `TextBlob` and `VADER` to classify sentiment on the candidates.
- **Sentiment Analysis**: Applies `TextBlob` and `VADER` to evaluate the sentiment of public comments about Trump and Harris.
- **Visualizations**: Generates pie charts to display the distribution of sentiments for each candidate and word clouds to highlight common words in the dataset.

The analysis provides a clearer picture of how each candidate was perceived during the election period, allowing for a comparison of their public reception. Visualizations like word clouds and pie charts enhance the insights by illustrating common keywords and overall sentiment trends. This project serves as a valuable tool for political analysts and researchers to study electoral sentiment patterns.
****************************************************************************************
## Key Steps:

1. **Sentiment Classification with TextBlob**:
   - Calculates sentiment polarity of the text (`positive`, `neutral`, `negative`).
   
   ```python
   from textblob import TextBlob
   merged_df['polarity'] = merged_df['text'].apply(lambda x: TextBlob(str(x)).sentiment.polarity)
   merged_df['sentiment'] = merged_df['polarity'].apply(lambda x: 'positive' if x > 0 else ('neutral' if x == 0 else 'negative'))
2 **Sentiment Classification with VADER**:

Classifies sentiment using the VADER model, particularly effective for social media text.
 ```python
Copy code
from nltk.sentiment.vader import SentimentIntensityAnalyzer
sia = SentimentIntensityAnalyzer()
merged_df['vader_polarity'] = merged_df['text'].apply(lambda x: sia.polarity_scores(str(x))['compound'])
merged_df['vader_sentiment'] = merged_df['vader_polarity'].apply(lambda x: 'positive' if x > 0.25 else ('neutral' if -0.25 <= x <= 0.25 else 'negative'))
 ```
![image](https://github.com/user-attachments/assets/785c102d-eb29-4104-8c1e-8f31d2c8fc1e)
![image](https://github.com/user-attachments/assets/dc5c8709-3ec2-4226-964e-8a1efd3f65de)

3. **Visualization - Pie Chart**:

Generates a pie chart showing the distribution of sentiment in the dataset.
 ```python
Copy code
sentiment = merged_df['sentiment'].value_counts()
sentiment_colors = ['red', (1.0, 0.75, 0.0), 'green']
sentiment.plot(kind='pie', title='Sentiment Analysis of the Post', colors=sentiment_colors, autopct='%1.1f%%', wedgeprops=dict(width=0.6))
 ```
![image](https://github.com/user-attachments/assets/4006de62-9193-46f2-abbc-b029bfeb789f)

4.**Visualization - Word Cloud**:

Generates a word cloud to represent the most frequent words in the dataset.
python
 ```
from wordcloud import WordCloud
import matplotlib.pyplot as plt
text = "".join(text for text in merged_df['text'].dropna())
wordcloud = WordCloud(background_color='black', width=100, height=100).generate(text)
plt.figure(figsize=(10, 8))
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis('off')
plt.show()
 ```
![image](https://github.com/user-attachments/assets/3c019395-3532-4639-89df-de28ba792f34)

**Conclusion**:
The project effectively demonstrates the use of both TextBlob and VADER for sentiment analysis, providing insightful visualizations of the results.
