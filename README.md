Project Instructions
Perform exploratory data analysis on the netflix_data.csv data to understand more about movies from the 1990s decade.

What was the most frequent movie duration in the 1990s? Save an approximate answer as an integer called duration.

A movie is considered short if it is less than 90 minutes. Count the number of short action movies released in the 1990s and save this integer as short_movie_count.
import pandas as pd

# Load the data and store as netflix_df.
netflix_df = pd.read_csv('netflix_data.csv')

# Filter out TV Shows and store it  as netflix_subset
netflix_subset = netflix_df[netflix_df['type'] == 'Movie']

# Keep only specific columns
netflix_movies = netflix_subset[['title', 'country', 'genre', 'release_year', 'duration']]

# Convert 'duration' to numeric, assuming it's in the format "xx min"
if netflix_movies['duration'].dtype == 'object':
    netflix_movies['duration'] = pd.to_numeric(netflix_movies['duration'].str.replace(' min', '').str.strip(), errors='coerce')

# Filter for movies shorter than 60 minutes
short_movies = netflix_movies[netflix_movies['duration'] < 60]
print(short_movies)
import matplotlib.pyplot as plt

# Create colors based on genre
colors = []
for _, row in netflix_movies.iterrows():
    if 'Children' in row['genre']:
        colors.append('blue')
    elif 'Documentaries' in row['genre']:
        colors.append('yellow')
    elif 'Stand-Up' in row['genre']:
        colors.append('green')
    else:
        colors.append('brown')

# Plotting
fig, bx= plt.subplots()
bx.scatter(netflix_movies['release_year'], netflix_movies['duration'], c=colors)
bx.set_title('Movie Duration by Year of Release')
bx.set_xlabel('Release year')
bx.set_ylabel('Duration (min)')
plt.show()
# Answering the question based on your visual interpretation of the plot
answer = "no"  # Change to "yes" if you conclude movies are getting shorter

title  ... duration
35                                            #Rucker50  ...       56
55                  100 Things to do Before High School  ...       44
67    13TH: A Conversation with Oprah Winfrey & Ava ...  ...       37
101                                   3 Seconds Divorce  ...       53
146                                      A 3 Minute Hug  ...       28
...                                                 ...  ...      ...
7679                    WWII: Report from the Aleutians  ...       45
7692  Ya no estoy aquí: Una conversación entre Guill...  ...       15
7718                     Yoo Byung Jae: Discomfort Zone  ...       54
7771                                               Zion  ...       12
7784                                  Zulu Man in Japan  ...       44

[420 rows x 5 columns]



