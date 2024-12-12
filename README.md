# Automated Data Analysis

## Dataset: E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\goodreads.csv

### Summary

- Shape: (10000, 23)
- Columns: {'book_id': 'int64', 'goodreads_book_id': 'int64', 'best_book_id': 'int64', 'work_id': 'int64', 'books_count': 'int64', 'isbn': 'object', 'isbn13': 'float64', 'authors': 'object', 'original_publication_year': 'float64', 'original_title': 'object', 'title': 'object', 'language_code': 'object', 'average_rating': 'float64', 'ratings_count': 'int64', 'work_ratings_count': 'int64', 'work_text_reviews_count': 'int64', 'ratings_1': 'int64', 'ratings_2': 'int64', 'ratings_3': 'int64', 'ratings_4': 'int64', 'ratings_5': 'int64', 'image_url': 'object', 'small_image_url': 'object'}
- Missing values: {'book_id': 0, 'goodreads_book_id': 0, 'best_book_id': 0, 'work_id': 0, 'books_count': 0, 'isbn': 700, 'isbn13': 585, 'authors': 0, 'original_publication_year': 21, 'original_title': 585, 'title': 0, 'language_code': 1084, 'average_rating': 0, 'ratings_count': 0, 'work_ratings_count': 0, 'work_text_reviews_count': 0, 'ratings_1': 0, 'ratings_2': 0, 'ratings_3': 0, 'ratings_4': 0, 'ratings_5': 0, 'image_url': 0, 'small_image_url': 0}

### Insights

Based on the dataset details you've provided, there are numerous potential insights and analyses that you could conduct. Here are some suggested analyses, along with relevant Python code snippets to help you execute them:

### Suggested Analyses & Insights

1. **Distribution of Average Ratings**:
   - Analyze the distribution of average ratings across the dataset to identify popular trends in book ratings.

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the data
df = pd.read_csv(r'E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\goodreads.csv')

# Plotting the distribution of average ratings
plt.figure(figsize=(10, 6))
sns.histplot(df['average_rating'], bins=30, kde=True)
plt.title('Distribution of Average Ratings')
plt.xlabel('Average Rating')
plt.ylabel('Frequency')
plt.show()
```

2. **Top Authors by the Number of Books**:
   - Identify the top authors with the most books represented in the dataset.

```python
# Count occurrences of each author
top_authors = df['authors'].value_counts().head(10)

# Plotting top authors
plt.figure(figsize=(12, 6))
top_authors.plot(kind='bar')
plt.title('Top 10 Authors by Number of Books')
plt.xlabel('Authors')
plt.ylabel('Number of Books')
plt.xticks(rotation=45)
plt.show()
```

3. **Average Rating by Publication Year**:
   - Investigate how the average rating varies with the year of publication.

```python
# Cleaning the data for publication year
df['original_publication_year'] = df['original_publication_year'].dropna().astype(int)

# Grouping by publication year and calculating average rating
avg_rating_by_year = df.groupby('original_publication_year')['average_rating'].mean().reset_index()

# Plotting the average rating over the year
plt.figure(figsize=(12, 6))
sns.lineplot(data=avg_rating_by_year, x='original_publication_year', y='average_rating')
plt.title('Average Rating by Publication Year')
plt.xlabel('Publication Year')
plt.ylabel('Average Rating')
plt.show()
```

4. **Rating Counts vs Average Ratings**:
   - Explore the relationship between the total number of ratings and the average rating to determine if there’s a correlation.

```python
# Scatter plot for ratings_count and average_rating
plt.figure(figsize=(10, 6))
sns.scatterplot(x='ratings_count', y='average_rating', data=df)
plt.title('Ratings Count vs Average Rating')
plt.xlabel('Ratings Count')
plt.ylabel('Average Rating')
plt.xscale('log')  # Log scale for better visibility
plt.show()
```

5. **Books by Language**:
   - Analyze the number of books available per language to understand the linguistic diversity of the dataset.

```python
# Count the number of books for each language
language_counts = df['language_code'].value_counts()

# Plotting the language distribution
plt.figure(figsize=(12, 6))
language_counts.plot(kind='bar')
plt.title('Number of Books by Language')
plt.xlabel('Language Code')
plt.ylabel('Number of Books')
plt.xticks(rotation=45)
plt.show()
```

6. **Trend Analysis on Ratings**:
   - Analyze the distribution of ratings (1 to 5) for highly rated books.

```python
# Filter for books with average rating more than a certain threshold, e.g., 4.0
highly_rated_books = df[df['average_rating'] > 4.0]

# Melt the ratings columns for easier plotting
ratings_columns = ['ratings_1', 'ratings_2', 'ratings_3', 'ratings_4', 'ratings_5']
melted_ratings = highly_rated_books.melt(value_vars=ratings_columns, 
                                           var_name='rating', 
                                           value_name='count')

# Plotting the distribution of ratings
plt.figure(figsize=(10, 6))
sns.barplot(x='rating', y='count', data=melted_ratings)
plt.title('Distribution of Ratings (1 to 5) for Highly Rated Books')
plt.xlabel('Ratings')
plt.ylabel('Count')
plt.show()
```

### Additional Considerations

- **Handling Missing Values**: Investigate the reasons for missing values in `isbn`, `isbn13`, and `original_publication_year`. This can affect the analysis, especially if those columns are integral to your analyses.

- **Normalization of Ratings**: Consider normalizing the ratings count if you wish to compare or aggregate rating performance across various sections of your dataset.

- **Filtering Data**: Depending on your analysis goals, you might want to filter out books with low ratings or those with very few ratings before diving deeper into ratings analysis.

By carrying out these analyses, you can uncover various insights that could help in understanding reader preferences, the impact of publication year on ratings, and overall trends in the dataset.

### Visualizations

![correlation_heatmap.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\correlation_heatmap.png)

![book_id_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\book_id_distribution.png)

![goodreads_book_id_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\goodreads_book_id_distribution.png)

![best_book_id_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\best_book_id_distribution.png)

![work_id_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\work_id_distribution.png)

![books_count_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\books_count_distribution.png)

![isbn13_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\isbn13_distribution.png)

![original_publication_year_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\original_publication_year_distribution.png)

![average_rating_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\average_rating_distribution.png)

![ratings_count_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\ratings_count_distribution.png)

![work_ratings_count_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\work_ratings_count_distribution.png)

![work_text_reviews_count_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\work_text_reviews_count_distribution.png)

![ratings_1_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\ratings_1_distribution.png)

![ratings_2_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\ratings_2_distribution.png)

![ratings_3_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\ratings_3_distribution.png)

![ratings_4_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\ratings_4_distribution.png)

![ratings_5_distribution.png](E:\RajC\IIT\IIT Madras\Sep 2024\TDS\Project\P2\\charts\ratings_5_distribution.png)

