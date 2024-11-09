#  ECE2112: Exploratory Data Analysis on Spotify 2023 Dataset

## 📖 Background Information

### <span style="color:blue"> **Exploratory Data Analysis** </span>
Exploratory Data Analysis (EDA) is an approach used to investigate and summarize the main characteristics of a dataset, often through visualizations and descriptive statistics. It aims to uncover patterns, spot anomalies, test hypotheses, and check assumptions to provide a general understanding of the data. EDA typically involves libraries like Pandas for data manipulation, Matplotlib, and Seaborn for visual representation, which together aid in drawing insights about trends and relationships within the dataset. [(<sup>1</sup>)](#-resources) <br> 

For this activity, an Exploratory Data Analysis (EDA) of the "Most Streamed Spotify Songs 2023" will be conducted.

## ✒️ General Guidelines
1. Begin by familiarizing yourself with the structure of the dataset. Check for missing values and data types, and perform an initial exploration to understand the different features available.
2. Provide summary statistics to give an overview of key metrics such as the number of streams, release dates, and musical attributes (e.g., BPM, danceability).
3. Use appropriate visualizations (e.g., bar charts, histograms, scatter plots) to uncover trends and patterns in the data. Ensure that your plots are well-labeled and easy to interpret.
4. Investigate correlations between different variables and provide insights based on your findings. Explore relationships between streams and other musical characteristics like tempo, energy, or playlists.
5. Based on your analysis, offer any insights or recommendations regarding the tracks, artists, or musical trends that could be useful for understanding what makes a track popular.

## 📚 Software and Libraries Used
![Anaconda](https://img.shields.io/badge/Anaconda-42B029?style=for-the-badge&logo=anaconda&logoColor=white)
![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-3776AB?style=for-the-badge&logo=python&logoColor=white)

> [!IMPORTANT]  
> In order to run the code, a Python IDE is needed, which in this case is Jupyter Notebook accessed through Anaconda.

The libraries can be imported by:
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

## 📙 Overview of the Dataset 
> [!IMPORTANT]  
> To access the dataset, download the `.csv` file from the [_Kaggle_ Website](https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023) or through the [spotify-2023.csv](spotify-2023.csv) file in this repository.

### **Loading the Dataset**
Input:
```python
sp_data = pd.read_csv('spotify-2023.csv', encoding='windows-1252')
sp_data
```
- `encoding='windows-1252'` was used due to the data set having an object datatype which cannot be read by the default encoding of the `pd.read_csv()` function

Output: <br>
![image](https://github.com/user-attachments/assets/0bf05383-1741-44db-b591-37b15058b048)
![image](https://github.com/user-attachments/assets/402a23d1-6cd9-4ba4-a8d0-7b9e0afcb2a1)

### **Dataset Size**
Input:
```python
sp_row, sp_col = sp_data.shape
print(f"The data set contains {sp_row} rows and {sp_col} columns.")
```
- `.shape` function was used to store the size of the dataset (row and column) into the `sp_row` and `sp_col` variables.

Output:
```
The data set contains 953 rows and 24 columns.
```

### **Data types of each column**
Input:
```python
data_summary = pd.DataFrame({
    'Column Name': sp_data.columns,
    'Data Type': sp_data.dtypes.values})

print(data_summary)
```
- `data_summary` Data Frame was created solely to have column names but the `.dtypes` function can be used as well.

Output:
```python
             Column Name Data Type
0             track_name    object
1         artist(s)_name    object
2           artist_count     int64
3          released_year     int64
4         released_month     int64
5           released_day     int64
6   in_spotify_playlists     int64
7      in_spotify_charts     int64
8                streams    object
9     in_apple_playlists     int64
10       in_apple_charts     int64
11   in_deezer_playlists    object
12      in_deezer_charts     int64
13      in_shazam_charts    object
14                   bpm     int64
15                   key    object
16                  mode    object
17        danceability_%     int64
18             valence_%     int64
19              energy_%     int64
20        acousticness_%     int64
21    instrumentalness_%     int64
22            liveness_%     int64
23         speechiness_%     int64
```
<ins>**General Description:**</ins> As shown above, the data types of each column appear to be either _object_ or _int64_. The columns with the object data type are: 
   - `track_name`
   - `artist(s)_name`
   - `streams`
   - `in_deezer_playlists`
   - `in_shazam_charts`
   - `mode`
<br>While the other columns are int64 data types.

### Null Count for Each Column
Input:
```python
sp_data.isnull().sum()
```
Output:
```python
track_name               0
artist(s)_name           0
artist_count             0
released_year            0
released_month           0
released_day             0
in_spotify_playlists     0
in_spotify_charts        0
streams                  0
in_apple_playlists       0
in_apple_charts          0
in_deezer_playlists      0
in_deezer_charts         0
in_shazam_charts        50
bpm                      0
key                     95
mode                     0
danceability_%           0
valence_%                0
energy_%                 0
acousticness_%           0
instrumentalness_%       0
liveness_%               0
speechiness_%            0
dtype: int64
```
<ins>**General Description:**</ins> It can be observed that only the `key` and the `in_shazam_charts` columns are the ones with null values. 

## 💻 Basic Descriptive Statistics

### Mean, Median and Standard Deviation of Streams
Since the streams has the object data type, we must convert it into a numerical data type before it can be processed.

Input: 
```python
sp_data['streams'] = pd.to_numeric(sp_data['streams'], errors='coerce')

print(sp_data['streams'].dtype)
```
- `pd.to_numeric()` function was used to convert the datatype of `streams` column into a `float64` datatype
Output:
```
float64
```

> [!NOTE]
> This `streams` column can now be processed for the calculations of the mean, median and std. Furthermore, it will also allow us to utilize it for other statistics.

Input:
```python
mean = round(sp_data['streams'].mean(),4)
median = round(sp_data['streams'].median(),4)
std = round(sp_data['streams'].std(),4)

print(f" Mean: {mean} \n Median: {median} \n Standard Deviation: {std}")
```
- `.mean()`, `.median()`, and `.std()` functions were used to calculate for the mean, median and standard deviation respectively while `.round()` function was utilized to round the result to 4 decimal places.

Output:
```python
 Mean: 514137424.9391 
 Median: 290530915.0 
 Standard Deviation: 566856949.0389
```


### Distribution of Tracks by Released Year 
Input:
```python
# Count the number of tracks for each release year
rel_year = sp_data['released_year'].value_counts().sort_index()

# Plot for the distribution of released year
plt.figure(figsize=(12, 5))

# Plot for tracks by release year
plt.subplot(1, 2, 1)
plt.bar(rel_year.index, rel_year.values, color='olive', zorder=3)
plt.grid(axis='y', linestyle='--', zorder=0)

plt.title('Tracks by Release Year', fontsize=14, fontweight='bold', color='olive')
plt.xlabel('Release Year', fontsize=12)
plt.ylabel('Number of Tracks', fontsize=12)

# Plot to show outliers
plt.subplot(1, 2, 2)
plt.boxplot(sp_data['released_year'].dropna(), vert=True, patch_artist=True)
plt.title('Outliers', fontsize=14, fontweight='bold', color='olive')
plt.ylabel('Release Year', fontsize=12)
plt.grid(axis='y', linestyle='--')

plt.show()
```
- `.value_counts()` function was used to count the occurances of the how many tracks were released in that year/by the artist.
- `.sort_index()` was used to sort the index in descending order.

Output: <br>
![Tracks by release year](https://github.com/user-attachments/assets/2c9a362a-4bac-4a4d-81e3-04ac431110e4)

<ins>**General Description:**</ins> The left histogram shows the number of tracks released each year, showing an increase in recent years especially after 2020. This shows that a lot of songs were released during that period in time. The right box plot shows the distribution of release years, showing the outliers which are tracks released before 2020.

### Distribution of Tracks by Number of Artist(s)
Input:
```python
# Calculates the number of tracks by the number of the artist who produced it
artist_count = sp_data['artist_count'].value_counts().sort_index()

# Plot for the distribution of artist count using bar plot
plt.figure(figsize=(12, 5))

# Plot for tracks by number of artists
plt.subplot(1, 2, 1)
plt.bar(artist_count.index, artist_count.values, color='sienna', zorder=3)
plt.grid(axis='y', linestyle='--', zorder=0)

plt.title('Tracks by Number of Artists', fontsize=14, fontweight='bold', color='sienna')
plt.xlabel('Number of Artists', fontsize=12)
plt.ylabel('Number of tracks', fontsize=12)

# Plot to show outliers using box plot
plt.subplot(1, 2, 2)
plt.boxplot(sp_data['artist_count'].dropna(), vert=True, patch_artist=True)
plt.grid(axis='y', linestyle='--', zorder=0)


plt.title('Outliers', fontsize=14, fontweight='bold', color='sienna')
plt.ylabel('Number of Artists', fontsize=12)

plt.show()
```
Output:
![download](https://github.com/user-attachments/assets/8871d80a-6f2e-4621-8735-a2c90223414d)

<ins>**General Description:**</ins> The left histogram shows the distribution of tracks by the number of artists, showing that most tracks are by single artists. The box plot on the right shows the outliers with high numbers of artists, which indicates that tracks with more than 3 artists are less frequent.

## 🎤 Top Performers

### Top 5 Most Streamed Tracks
Input: 
```python
top_stream = sp_data.sort_values('streams', ascending=False).head().reset_index(drop=True)
top_stream
```
- The _top_stream_ variable was used to sort the _sp_data_ data set by the number of _streams_ using the `.sort_values()` function and to only show the first five entries using the `.head()` function.

Output:
![image](https://github.com/user-attachments/assets/7f22ae72-f391-4c1b-b167-5a84068e1dac)

Additionally, it can be plotted using a bar graph to further understand the result and to visualize the data itself.

Input:
```python
plt.figure(figsize=(12, 6))
plt.barh(top_stream['track_name'], top_stream['streams'], zorder=3, color=['#133C55', '#386FA4', '#59A5D8', '#84D2F6', '#91E5F6'])
plt.grid(axis='x', linestyle='--', zorder=0)

plt.title('Top 5 Most Streamed Tracks', fontsize=16, fontweight='bold', color='#0F2F43')
plt.ylabel('Track Name', fontsize=12)
plt.xlabel('No. of Streams', fontsize=12)
plt.gca().invert_yaxis()

plt.show()
```

Output:<br>
![download](https://github.com/user-attachments/assets/0680283f-000a-4d1f-969c-3873524c9f5c)

<ins>**General Description:**</ins> As observed from the bar plot above, the top 5 most streamed tracks according to the number of streams are **Blinding Lights**, **Shape of You**, **Someone You Loved**, **Dance Monkey** and **Sunflower** in order.

### Top 5 Most Frequent Artists
Input:
```python
most_freq = sp_data['artist(s)_name'].value_counts().head().reset_index()
most_freq

# Plots the top 5 artists with most frequent artist
plt.figure(figsize=(12, 6))
plt.barh(most_freq['artist(s)_name'], most_freq['count'], zorder=3, color=['#E7E247','#3D3B30','#4D5061','#5C80BC','#E9EDDE'])
plt.grid(axis='x', linestyle='--', zorder=0)

plt.title('Top 5 Artists with Most Released Number of Tracks', fontsize=16, fontweight='bold', color='navy')
plt.xlabel('No. of Tracks', fontsize=12)
plt.ylabel('Artist(s) Name', fontsize=12)
plt.gca().invert_yaxis()

plt.show()
```

Output: <br>
![download](https://github.com/user-attachments/assets/6e92d142-bb12-45e3-8d8c-4479ac4e6e78)
<ins>**General Description:**</ins> As observed from the bar plot above, the top 5 artist with the most amount of released tracks are `Taylor Swift`, `The Weeknd`, `Bad Bunny`, `SZA`, and `Harry Styles`.

## 📈 Temporal Trends
### Tracks Released Over Time (Annually)
Input:
```python
# Plots a linegraph that shows the distribution of tracks over time
plt.figure(figsize=(12, 6))  
plt.plot(rel_year.index, rel_year.values, marker='8', color='coral')
plt.grid(axis='y', linestyle='--')

plt.title('Tracks Released over Time', fontsize=16, fontweight='bold', color='coral')
plt.xlabel('Years', fontsize=12)
plt.ylabel('No. of Tracks Released', fontsize=12)
plt.xticks(rel_year.index, rotation=90, fontsize=8)

plt.show()
```

Output: <br>
![download](https://github.com/user-attachments/assets/3bee8bd1-d88a-4612-80b5-fc27bb5e157a)
<ins>**General Description:**</ins> Based from the observation of the line graph, it was observed that there was a jump in the number of tracks released around the 2020 year mark. Furthermore, the latest/oldest track released that is recorded in spotify was found out to be in 1930.

### Tracks Released Over Time (Monthly)
Input:
```python
# Counts the total number of tracks released each month
monthly_track = sp_data['released_month'].value_counts().sort_index()
monthly_track
```

Output:
```python
released_month
1     134
2      61
3      86
4      66
5     128
6      86
7      62
8      46
9      56
10     73
11     80
12     75
Name: count, dtype: int64
```
Input:
```python
# Plot the Monthly Distribution of Released Tracks using a line graph
plt.figure(figsize=(12, 6))
plt.plot(monthly_track.index, monthly_track.values, zorder=3, color='teal', marker='8')
plt.xticks(ticks=monthly_track.index, labels=['January', 'February', 'March', 'April', 'May', 'June', 
                                    'July', 'August', 'September', 'October', 'November', 'December'])
plt.grid(axis='y', linestyle='--', zorder=0)
plt.grid(axis='x', linestyle='--', zorder=0)

plt.ylabel('Number of Tracks')
plt.xlabel('Month')
plt.title('Monthly Distribution of Released Tracks', fontweight='bold', color='teal')

plt.show()
```

Output: <br>
![download](https://github.com/user-attachments/assets/9b2d8a19-cb59-4e37-a2c5-1fa0b133fbc3)

<ins>**General Description:**</ins> Based from the observation of the line graph, it goes to show that most tracks were released around the month of Janurary; while, the month of August, experiences the least amount of tracks released.

## 🎶 Genre and Music Characteristics
### Correlation between Musical Attributes
Input:
```python
# Calculates the correlation of the musical attributes with the stream
corr = sp_data[['streams', 'bpm', 'danceability_%', 
                'valence_%',	'energy_%',	'acousticness_%', 
                'instrumentalness_%', 'liveness_%', 'speechiness_%']].corr()

# Plots a heat map between the correlation of streams and musical attributes
plt.figure(figsize=(12, 10))
sns.heatmap(corr, cmap='coolwarm', annot=True, linecolor='black',linewidths=0.3)
plt.title("Correlation Heatmap between Streams and Musical Attributes", fontweight='bold', color='green', fontsize=16)
plt.show()
```
Output: <br>
![download](https://github.com/user-attachments/assets/36256d69-4179-4e03-8f2e-0cb34de314eb)

<ins>**General Description:**</ins> The heatmap shows the correlation between the _streams_ and the _musical attributes_ in addition to the correlation between the musical attributes itself. From observation, there doesn't seem to be an attribute that influence the number of streams the most since the correlation between the _streams_ and _musical attributes_ display a negative value. Therefore, it can be said that due to the different tastes of people, the number of streams is not influenced by its musical attribute.

For the correlation between `danceablity_%` and `energy_%`, the heatmap shows a moderate correlation due to the positive value it exhibits. Additionally, a low correlation seems to be exhibited between `valence_%` and `acousticness_%` due to its negative value.

## 🌠 Platform Popularity
### Platform Popularity Distribution
Input:
```python
# Converts the data type of in_deezer_playlist from object to float/numeric
sp_data['in_deezer_playlists'] = pd.to_numeric(sp_data['in_deezer_playlists'], errors='coerce')

# Calculating the track counts in different platforms
spotify_playlist = sp_data['in_spotify_playlists'].sum()
deezer_playlist = sp_data['in_deezer_playlists'].sum()
apple_playlist = sp_data['in_apple_playlists'].sum()

print(f"\n Track count in Spotify Playlists: {spotify_playlist} \n Track count in Deezer Playlists: {deezer_playlist} \n Track count in Apple Playlists: {apple_playlist}")
```
Output:
```
 Track count in Spotify Playlists: 4955719 
 Track count in Deezer Playlists: 95913.0 
 Track count in Apple Playlists: 64625
```
To plot the data calculated, we will use a bar plot to see the differences between the platforms.<br>
Input: 
```python
# Putting counts into a list for easy plotting
platforms = ['Spotify Playlists', 'Deezer Playlists', 'Apple Playlists']
no_playlist = [spotify_playlist, deezer_playlist, apple_playlist]

# Plots a bar graph for the Platform popularity Distribution
plt.figure(figsize=(10, 6))
plt.barh(platforms, no_playlist, color=['#1DB954', '#E07A5F', '#FA4D09'], zorder=3)
plt.grid(axis='x', linestyle='--', zorder=0)

plt.title('Platform Popularity Distribution', fontweight='bold', color='#90A583', fontsize=16)
plt.xlabel('No. of Tracks', fontsize=12)
plt.ylabel('Platform', fontsize=12)
plt.gca().invert_yaxis()  

plt.show()
```
Output: <br>
![download](https://github.com/user-attachments/assets/e7b6df34-e429-4f67-b849-42d9254599dd)
<ins>**General Description:**</ins> Based on the observation of the bar plot for `Platform Popularity Distribution`, there was a stark difference between the 3 platforms included in the dataset. Furthermore, it indicates that Spotify, as a platform, dominates in terms of the volume of tracks featured it its playlists.

## 🔎 Advanced Analysis
### Distribution of Keys by Streams
Input:
```python
streams_by_key = sp_data.groupby('key')['streams'].sum().sort_values(ascending=False)
streams_by_key
```
Output:
```python
key   streams
C#    7.251363e+10
G     4.344954e+10
G#    4.339898e+10
D     4.289157e+10
B     4.206718e+10
F     4.169173e+10
F#    3.813251e+10
E     3.580483e+10
A#    3.149110e+10
A     3.025426e+10
D#    1.825021e+10
Name: streams, dtype: float64
```
Input:
```python
# Plots the Distribution of Musical Keys by streams using a bar graph
plt.figure(figsize=(12, 6))
plt.barh(streams_by_key.index, streams_by_key.values, color=['#F94144', '#F65A38', '#F3722C', '#F8961E', '#F9C74F', '#C5C35E', '#90BE6D', '#43AA8B', '#3A9278','#4D908E','#577590'], zorder=3)
plt.grid(axis='x', linestyle='--', zorder=0)

plt.title('Distribution of Musical Keys by Streams', fontweight='bold', color='black', fontsize=16)
plt.xlabel('No. of Streams', fontsize=12)
plt.ylabel('Musical Keys', fontsize=12)
plt.gca().invert_yaxis()  

plt.show()
```
Output: <br>
![download](https://github.com/user-attachments/assets/d82a4fc1-b56e-4ab6-a5ee-7e2fe38f3f61)

<ins>**General Description:**</ins> Based from the observation of the bar graph for the `Distribution of of Musical Keys by Streams`, it appears that tracks using the C# key has the highest amount of streams. On the other hand, tracks with the D# key have the least amount of streams.

### Distribution of Mode by Streams
Input:
```python
streams_by_mode = sp_data.groupby('mode')['streams'].sum().sort_values(ascending=False)
streams_by_mode
```
Output:
```python
mode     streams
Major    2.936232e+11
Minor    1.958356e+11
Name: streams, dtype: float64
```
Input:
```python
# Plots the Distribution of Mode by streams using a bar graph
plt.figure(figsize=(12, 3))
plt.barh(streams_by_mode.index, streams_by_mode.values, color=['#F94144','#577590'], zorder=3)
plt.grid(axis='x', linestyle='--', zorder=0)

plt.title('Distribution of Mode by Streams', fontweight='bold', color='black', fontsize=14)
plt.xlabel('No. of Streams', fontsize=12)
plt.ylabel('Mode', fontsize=12)

plt.show()
```
Output: <br>
![download](https://github.com/user-attachments/assets/34b99f4c-1eb0-41d7-9aa1-d6b854bd7819)

<ins>**General Description:**</ins> Based from the observation of the bar graph for the `Distribution of Mode by Streams`, it was observed that tracks with a mode of major was preferred over tracks with a mode of minor.

### Top 10 Most Frequently Appearing Artist in Playlists
Input:
```python
# Create a separate DataFrame for calculating the total playlist count
playlist = sp_data[['artist(s)_name', 'in_spotify_playlists', 'in_deezer_playlists', 'in_apple_playlists']].copy()

# Calculate the total playlist count in the Playlist
playlist['total_playlist'] = (
    playlist['in_spotify_playlists'] + 
    playlist['in_deezer_playlists'] + 
    playlist['in_apple_playlists']
)

artist_popularity = playlist.groupby('artist(s)_name')['total_playlist'].sum().sort_values(ascending=False).head(10)
artist_popularity
```
Output:
```python
artist(s)_name
Taylor Swift      114815.0
Harry Styles       91898.0
The Weeknd         77431.0
Bad Bunny          52657.0
Frank Ocean        52162.0
Olivia Rodrigo     49359.0
SZA                45786.0
Doja Cat           36405.0
Ed Sheeran         30690.0
Arctic Monkeys     28068.0
Name: total_playlist, dtype: float64
```
Input:
```python
plt.figure(figsize=(12, 6))
plt.barh(artist_popularity.index, artist_popularity.values, color='#FF6347', zorder=3)
plt.grid(axis='x', linestyle='--', zorder=0)

plt.title('Top 10 Most Frequently Appearing Artist in Playlists')
plt.xlabel('Total Appearances')
plt.gca().invert_yaxis()  # Flip to have the highest at the top

for index, value in enumerate(artist_popularity.values):
    plt.text(value, index, f'{value:,}', color='black')
plt.show()
```
Output: <br>
![download](https://github.com/user-attachments/assets/808f06dd-d1f1-42f1-bdbb-dc296997d612)


### Top 10 Most Frequently Appearing Artist in Charts
Input:
```python
# Converts the data type from object to float/numeric
sp_data['in_shazam_charts'] = pd.to_numeric(sp_data['in_shazam_charts'], errors='coerce')

# Create a separate DataFrame for calculating the total chart counts
charts = sp_data[['artist(s)_name', 'in_spotify_charts', 'in_apple_charts', 'in_deezer_charts', 'in_shazam_charts']].copy()

# Calculate the total charts in the new DataFrame
charts['total_charts'] = (
    charts['in_spotify_charts'] + 
    charts['in_apple_charts'] + 
    charts['in_shazam_charts'] + 
    charts['in_deezer_charts']
)

# Summing total chart appearances for each artist and getting the top 10
charts_popularity = charts.groupby('artist(s)_name')['total_charts'].sum().sort_values(ascending=False).head(10)
charts_popularity
```
Output:
```python
artist(s)_name
Taylor Swift         4277.0
The Weeknd           1952.0
Bad Bunny            1779.0
SZA                  1653.0
Olivia Rodrigo       1495.0
NewJeans             1341.0
Dave, Central Cee    1267.0
Ed Sheeran           1260.0
Gunna                1257.0
Latto, Jung Kook     1246.0
Name: total_charts, dtype: float64
```
Input:
```python
plt.figure(figsize=(12, 6))
plt.barh(charts_popularity.index, charts_popularity.values, color='#FF6347', zorder=3)
plt.grid(axis='x', linestyle='--', zorder=0)

plt.title('Top 10 Most Frequently Appearing Artist in Charts')
plt.xlabel('Total Appearances')
plt.gca().invert_yaxis()  

for index, value in enumerate(charts_popularity.values):
    plt.text(value, index, f'{value:,}', color='black')
plt.show()
```
Output:<br>
![download](https://github.com/user-attachments/assets/9c55e485-d705-4ab6-a88a-172c3298a055)
<ins>**General Description:**</ins> Based from the outputs of the last two bar plots, it was observed that tracks of `Taylor Swift` tops the plots of Most frequently appearing artist in playlists and in charts. Honorable mentions that are still within the top 10 in both of the plots are `The Weeknd`, `Bad bunny`, `Olivia Rodrigo`, `SZA` and `Ed Sheeran`.

## 📝 Conclusion
In conclusion, this exploratory data analysis on Spotify's most streamed songs of 2023 provided valuable insights into the factors that may contribute to a song's popularity. By examining various musical attributes like danceability, and energy, alongside basic statistics and visualizations, it allowed for identifying the patterns and trends across top-performing tracks. The artist and release year distributions highlighted shifts in music preferences over time, showing that recent tracks often dominate streaming charts. Analyzing correlations among attributes also suggested possible relationships between musical elements and the number of streams. This analysis demonstrates how usefel an Exploratory Data Analysis actually is and how powerful it can be in looking for trends of raw data.

## ✒️ Author
### Submitted by: Amboy, John Gabriel D. | 2ECE-A

## 🌐 Resources
- [Pandas Documentation](https://www.datacamp.com/cheat-sheet/pandas-cheat-sheet-for-data-science-in-python)
- [Matplotlib Documentation](https://matplotlib.org/stable/contents.html)
- [Seaborn Cheatsheet](https://www.datacamp.com/cheat-sheet/python-seaborn-cheat-sheet)
- [Most Streamed Spotify Songs 2023 Dataset](https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023)
- [Sahoo, K., Samal, A. K., Pramanik, J., & Pani, S. K. (2019). Exploratory data analysis using Python. International Journal of Innovative Technology and Exploring Engineering, 8(12), 4727-4735](https://www.researchgate.net/profile/Dr-Subhendu-Pani/publication/337146539_IJITEE/links/5dc70b124585151435fb427e/IJITEE.pdf)

---
