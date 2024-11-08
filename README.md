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

Output:
![image](https://github.com/user-attachments/assets/0bf05383-1741-44db-b591-37b15058b048)
![image](https://github.com/user-attachments/assets/402a23d1-6cd9-4ba4-a8d0-7b9e0afcb2a1)

### **Dataset Size/Structure**
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

## 💻 Basic Descriptive Statistics

### Mean, Median and Standard Deviation of Streams
Since the streams has an object data type, we must convert it into a numerical data type before it can be processed.

Input: 
```python
sp_data['streams'] = pd.to_numeric(sp_data['streams'], errors='coerce')

print(sp_data['streams'].dtype)
```
Output:
```
float64
```
- `pd.to_numeric()` function was used to convert the datatype of `streams` column into a `float64` datatype

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
- `.sort_index()` was used to sort the indices in descending order.

Output: <br>
![Tracks by release year](https://github.com/user-attachments/assets/2c9a362a-4bac-4a4d-81e3-04ac431110e4)

<ins>**General Description:**</ins> The left histogram shows the number of tracks released each year, showing an increase in recent years especially after 2020. This shows that a lot of songs were released during that periond in time. The right box plot shows the distribution of release years, showing the outliers which are tracks released before 2020.

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

Output:
![download](https://github.com/user-attachments/assets/0680283f-000a-4d1f-969c-3873524c9f5c)

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

Output:
![download](https://github.com/user-attachments/assets/6e92d142-bb12-45e3-8d8c-4479ac4e6e78)

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

Output:
![download](https://github.com/user-attachments/assets/3bee8bd1-d88a-4612-80b5-fc27bb5e157a)

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

Output:
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
Output:
![download](https://github.com/user-attachments/assets/36256d69-4179-4e03-8f2e-0cb34de314eb)



## 🌠 Platform Popularity


## 🔎 Advanced Analysis


## 🌐 Resources
- [Pandas Documentation](https://www.datacamp.com/cheat-sheet/pandas-cheat-sheet-for-data-science-in-python)
- [Matplotlib Documentation](https://matplotlib.org/stable/contents.html)
- [Seaborn Cheatsheet](https://www.datacamp.com/cheat-sheet/python-seaborn-cheat-sheet)
- [Most Streamed Spotify Songs 2023 Dataset](https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023)
- [Sahoo, K., Samal, A. K., Pramanik, J., & Pani, S. K. (2019). Exploratory data analysis using Python. International Journal of Innovative Technology and Exploring Engineering, 8(12), 4727-4735](https://www.researchgate.net/profile/Dr-Subhendu-Pani/publication/337146539_IJITEE/links/5dc70b124585151435fb427e/IJITEE.pdf)


## 📜 Version History

### 1.1 
- Created the `README.md` file
- Uploaded the `spotify-2023.xlsx` to the repository

### 1.2 
- Added `Background Information` tab
- Added `Resources` tab

### 1.3
- Added `General Guidelines` tab
- Added `Documentation` tab
- Added `Overview of the Dataset` tab 
- Added `Basic Descriptive Statistics` tab
- Added `Top Performers` tab
- Added `Temporal Trends` tab
- Added `Genre and Music Characteristics`
- Added `Platform Popularity` tab
- Added `Advanced Analysis` tab

### 1.4
- Added `Software and Libraries Used` tab


---
