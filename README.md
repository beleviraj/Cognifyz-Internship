# Cognifyz Technologies Task Solutions

## LEVEL 1

### TASK 1

#### 1. Top Four Most Common Cuisines
```python
from collections import Counter
cuisines_list=df['Cuisines'].str.split(', ').explode().dropna()
cuisines_count=Counter(cuisines_list)
top_cuisines=cuisines_count.most_common(3)
top_cuisines
```

#### 2. Restaurants that Serve Each of the Top Cuisines
```python
total_restaurants = len(df)
percentage_top_cuisines = [(cuisine,(count / total_restaurants)*100) for cuisine, count in top_cuisines]
print(percentage_top_cuisines)
```

### TASK 2

#### 1. Identify the City with the Highest Number of Restaurants
```python
top_city = df['City'].value_counts().idxmax()
top_city
```

#### 2. Count of Restaurants in the Top City
```python
top_city_count = df['City'].value_counts().max()
top_city_count
```

### TASK 3

#### 1. Price Range Distribution
```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.histplot(df['Price_Range'], bins=10, kde=True)
plt.title('Price Range Distribution')
plt.show()
```

#### 2. Percentage of Restaurants in Each Price Range Category
```python
price_range_percentage = df['Price_Range'].value_counts(normalize=True) * 100
price_range_percentage
```

### TASK 4

#### 1. Online Delivery Availability
```python
delivery_percentage = df['Online_Delivery'].value_counts(normalize=True) * 100
delivery_percentage
```

#### 2. Compare Ratings of Restaurants with and Without Online Delivery
```python
df.groupby('Online_Delivery')['Rating'].mean()
```

## LEVEL 3

### TASK 1

#### 1. Analysis of Customer Reviews Sentiment
```python
from textblob import TextBlob

def analyze_sentiment(text):
    return TextBlob(str(text)).sentiment.polarity

df['Sentiment'] = df['Review_Text'].apply(analyze_sentiment)
df[['Restaurant_Name', 'Sentiment']].head()
```

#### 2. Visualization of Review Sentiments
```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.histplot(df['Sentiment'], bins=20, kde=True)
plt.title('Sentiment Distribution')
plt.show()
```

### TASK 2

#### 1. Identify Restaurants with the Highest and Lowest Number of Votes
```python
top_voted_restaurant = df.loc[df['Votes'].idxmax(), ['Restaurant_Name', 'Votes']]
low_voted_restaurant = df.loc[df['Votes'].idxmin(), ['Restaurant_Name', 'Votes']]
(top_voted_restaurant, low_voted_restaurant)
```

#### 2. Correlation Between Number of Votes and Ratings
```python
correlation = df[['Votes', 'Rating']].corr()
correlation
```

### TASK 3

#### 1. Relationship Between Price Range, Online Delivery, and Table Booking
```python
import seaborn as sns
sns.boxplot(x='Price_Range', y='Rating', hue='Online_Delivery', data=df)
plt.title('Price Range vs Rating (Online Delivery)')
plt.show()
```

```python
sns.boxplot(x='Price_Range', y='Rating', hue='Table_Booking', data=df)
plt.title('Price Range vs Rating (Table Booking)')
plt.show()
```

## Conclusion
This project analyzes restaurant data to extract insights such as popular cuisines, top cities, price ranges, customer sentiment, and online service impact. The insights can help businesses improve services based on data-driven decisions.
