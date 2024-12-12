# Automated Data Analysis

## Dataset: E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\goodreads.csv

### Summary

- Shape: (10000, 23)
- Columns: {'book_id': 'int64', 'goodreads_book_id': 'int64', 'best_book_id': 'int64', 'work_id': 'int64', 'books_count': 'int64', 'isbn': 'object', 'isbn13': 'float64', 'authors': 'object', 'original_publication_year': 'float64', 'original_title': 'object', 'title': 'object', 'language_code': 'object', 'average_rating': 'float64', 'ratings_count': 'int64', 'work_ratings_count': 'int64', 'work_text_reviews_count': 'int64', 'ratings_1': 'int64', 'ratings_2': 'int64', 'ratings_3': 'int64', 'ratings_4': 'int64', 'ratings_5': 'int64', 'image_url': 'object', 'small_image_url': 'object'}
- Missing values: {'book_id': 0, 'goodreads_book_id': 0, 'best_book_id': 0, 'work_id': 0, 'books_count': 0, 'isbn': 700, 'isbn13': 585, 'authors': 0, 'original_publication_year': 21, 'original_title': 585, 'title': 0, 'language_code': 1084, 'average_rating': 0, 'ratings_count': 0, 'work_ratings_count': 0, 'work_text_reviews_count': 0, 'ratings_1': 0, 'ratings_2': 0, 'ratings_3': 0, 'ratings_4': 0, 'ratings_5': 0, 'image_url': 0, 'small_image_url': 0}

### Insights

Based on the provided dataset from Goodreads, we can analyze several aspects to derive insights about books, their ratings, authors, and publication years. Below, I suggest some analyses along with Python code snippets for implementation.

### Suggested Analyses and Insights

1. **Distribution of Average Ratings**:
   Understand how the average ratings are distributed among books.

   ```python
   import pandas as pd
   import matplotlib.pyplot as plt
   import seaborn as sns

   # Load the dataset
   df = pd.read_csv(r'E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\goodreads.csv')

   # Plot the distribution of average ratings
   plt.figure(figsize=(10, 5))
   sns.histplot(df['average_rating'], bins=30, kde=True)
   plt.title('Distribution of Average Ratings')
   plt.xlabel('Average Rating')
   plt.ylabel('Frequency')
   plt.show()
   ```

2. **Top Authors by Average Ratings**:
   Identify who the highest-rated authors are based on average ratings of their books.

   ```python
   # Group by authors and calculate the mean average rating
   top_authors = df.groupby('authors')['average_rating'].mean().sort_values(ascending=False).head(10)

   # Plotting
   top_authors.plot(kind='bar', figsize=(10, 5), title='Top 10 Authors by Average Ratings')
   plt.ylabel('Average Rating')
   plt.xlabel('Authors')
   plt.xticks(rotation=45)
   plt.show()
   ```

3. **Books Published Over Time**:
   Analyze the trend of books published over different years.

   ```python
   # Convert original_publication_year to int (drop NaNs)
   publication_years = df['original_publication_year'].dropna().astype(int)

   # Count the number of books published each year
   publication_count = publication_years.value_counts().sort_index()

   # Plotting
   plt.figure(figsize=(12, 6))
   publication_count.plot(kind='line')
   plt.title('Number of Books Published Over the Years')
   plt.xlabel('Publication Year')
   plt.ylabel('Number of Books')
   plt.grid()
   plt.show()
   ```

4. **Language Distribution**:
   Assess the distribution of languages in the dataset.

   ```python
   # Count of books available in each language
   language_distribution = df['language_code'].value_counts()

   # Plotting
   plt.figure(figsize=(10, 5))
   sns.barplot(x=language_distribution.index, y=language_distribution.values)
   plt.title('Distribution of Languages')
   plt.xlabel('Language Code')
   plt.ylabel('Number of Books')
   plt.xticks(rotation=45)
   plt.show()
   ```

5. **Correlation between Ratings and Reviews**:
   Analyze how the number of ratings and text reviews correlate with average ratings.

   ```python
   # Compute the correlation matrix
   correlation = df[['average_rating', 'ratings_count', 'work_text_reviews_count']].corr()

   # Heatmap
   plt.figure(figsize=(8, 6))
   sns.heatmap(correlation, annot=True, cmap='coolwarm')
   plt.title('Correlation Heatmap')
   plt.show()
   ```

6. **Top Rated Books**:
   Identify the top 10 rated books in the dataset.

   ```python
   # Get the top 10 books by average rating
   top_rated_books = df.nlargest(10, 'average_rating')[['title', 'authors', 'average_rating']]

   print(top_rated_books)
   ```

7. **Analysis of ISBN Data**:
   Analyze the missing values in ISBN columns and its potential impact.

   ```python
   # Check missing values in ISBN columns
   missing_isbn = df[['isbn', 'isbn13']].isnull().sum()
   print(missing_isbn)
   ```

### Conclusion and Next Steps
The suggested analyses can help in understanding dataset properties, identifying trends, and deriving actionable insights. Depending on the results, further analyses can be performed to dive deeper into specific areas such as demographic influences on ratings, popular genres if available, etc.

### Visualizations

![book_id_distribution.png](book_id_distribution.png)

![goodreads_book_id_distribution.png](goodreads_book_id_distribution.png)



### Additional Reports

- [Dataset Summary](summary_report.txt)