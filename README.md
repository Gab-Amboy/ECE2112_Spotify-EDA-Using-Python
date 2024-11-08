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

### Loading the Dataset
Input:
```python
sp_data = pd.read_csv('spotify-2023.csv', encoding='windows-1252')
sp_data
```
- `encoding='windows-1252'` was used due to the data set having an object datatype which cannot be read by the default encoding of the `pd.read_csv()` function

Output:
![image](https://github.com/user-attachments/assets/0bf05383-1741-44db-b591-37b15058b048)
![image](https://github.com/user-attachments/assets/402a23d1-6cd9-4ba4-a8d0-7b9e0afcb2a1)




## 💻 Basic Descriptive Statistics


## 🎤 Top Performers


## 📈 Temporal Trends


## 🎶 Genre and Music Characteristics


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
