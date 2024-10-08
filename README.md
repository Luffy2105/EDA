# Exploratory Data Analysis
EDA atau Exploratory Data Analysis adalah pendekatan dalam analisis data yang bertujuan untuk mengeksplorasi dan memahami data sebelum melakukan analisis lebih lanjut atau penerapan model statistik. Dalam EDA, peneliti atau analis menggunakan berbagai teknik visualisasi dan statistik deskriptif untuk mengidentifikasi pola, hubungan, dan anomali dalam data.

Beberapa langkah umum dalam EDA meliputi:

* Visualisasi Data: Menggunakan grafik seperti histogram, scatter plot, atau box plot untuk melihat distribusi dan hubungan antar variabel.
* Statistik Deskriptif: Menghitung ukuran-ukuran seperti mean, median, modus, varians, dan standar deviasi untuk memahami karakteristik data.
* Pembersihan Data: Mengidentifikasi dan menangani nilai yang hilang, outlier, atau kesalahan dalam data.
* Pemeriksaan Asumsi: Menilai apakah data memenuhi asumsi-asumsi yang diperlukan untuk analisis statistik lebih lanjut.

Proses EDA dengan menggunakan data set berikut "https://www.kaggle.com/datasets/gianinamariapetrascu/top-250-anime-2023"


## 1. Load Data

```sh
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
df = pd.read_csv("/content/top250_anime.csv")
df
```

## 2. Basic infornation about the dataset

```sh
# Menampilkan 5 baris pertama dari dataset
print(df.head())

# Menampilkan informasi dasar tentang dataset
print(df.info())

# Menampilkan statistik deskriptif
print(df.describe())

# Menampilkan nama kolom
print(df.columns.tolist())
```

## 3. cek nilai duplikat dan nilai unik

```sh
duplicates = df.duplicated().sum()
print(duplicates)

unique = df.nunique()
print(unique)
```

## 4. Visualisakan jumlah nilai unik

```sh
# Type - Bar Plot
plt.figure(figsize=(8, 4))
sns.countplot(data=df, x='Type', palette='Set2')
plt.title('Count of Types')
plt.xlabel('Type')
plt.ylabel('Count')
plt.show()
```
![image](https://github.com/user-attachments/assets/3cc417ba-ba00-46c6-b9ee-39bcf27ca8d2)


```sh
# Popularity - Histogram
plt.figure(figsize=(8, 4))
plt.hist(df['Popularity'], bins=20, color='green', alpha=0.7)
plt.title('Histogram of Popularity')
plt.xlabel('Popularity')
plt.ylabel('Frequency')
plt.grid()
plt.show()
```

## 5. Menemukan semua null values

```sh
# Memeriksa nilai yang hilang
print(df.isnull().sum())
```

## 6. Reaplace semua null values

```sh
data_dropped = df.dropna(inplace=True)

data_after_cleaning = df.isnull().sum()
data_after_cleaning
```

## 7. Mengetahui tipe data

```sh
print(df.dtypes)
```

## 8. filter data

```sh

# Flter berdasarkan genre
action_anime = df[df['Genre'] == 'Action']
print("\nAnime dengan Genre 'Action':")
action_anime

# Filter berdasarkan skor
high_score_anime = df[df['Score'] > 8.0]
print("\nAnime dengan Skor lebih dari 8.0:")
high_score_anime

# Filter berdasarkan popularitas
popular_anime = df[df['Popularity'] > 200]
print("\nAnime dengan Popularitas lebih dari 200:")
popular_anime
```

## 9. Membuat box plot

```sh

# Score berdasarkan Type
plt.figure(figsize=(10, 6))
sns.boxplot(data=df, x='Type', y='Score', palette='magma')
plt.title('Box Plot Skor berdasarkan Tipe')
plt.xlabel('Tipe')
plt.ylabel('Skor')
plt.grid()
plt.show()
```
![image](https://github.com/user-attachments/assets/878ae082-acac-466b-b08b-49274eaeacac)


```sh
# Menentukan genre yang ingin ditampilkan
genres = ['Action', 'Drama', 'Fantasy']

# Memfilter data untuk genre yang diinginkan
filtered_data = df[df['Genre'].isin(genres)]

plt.figure(figsize=(8, 4))
sns.boxplot(data=filtered_data, x='Genre', y='Popularity', palette='Set2')
plt.title('Box Plot Skor untuk Genre Action, Drama, dan Fantasy')
plt.xlabel('Genre')
plt.ylabel('Popularity')
plt.grid()
plt.show()
```

## 10. Korelasi

```sh

# Mengatur ukuran figure
plt.figure(figsize=(8, 4))

# Menghitung korelasi dan membuat heatmap
corr_matrix = df.select_dtypes('number').corr()
sns.heatmap(corr_matrix, annot=True, cmap='coolwarm')
plt.title('Heatmap of Correlation Matrix')
plt.show()
```
![image](https://github.com/user-attachments/assets/31282815-731c-4e94-bbb1-d96acaff2626)


```sh

correlation_score_Duration = df['Score'].corr(df['Duration'])
print(f'Korelasi antara Score dan Duration: {correlation_score_Duration}')

# Membuat matriks korelasi untuk visualisasi heatmap
correlation_matrix = df[['Score', 'Duration']].corr()

# Membuat heatmap
plt.figure(figsize=(6, 5))
sns.heatmap(correlation_matrix, annot=True, fmt=".2f", cmap='coolwarm', square=True, cbar_kws={"shrink": .8})
plt.title('correlation_score_Duration')
plt.show()
```

```sh

# Scatter plot Score vs Popularity
plt.figure(figsize=(8, 4))
sns.scatterplot(data=df, x='Popularity', y='Score', color='blue')
plt.title('Score vs Popularity')
plt.xlabel('Popularity')
plt.ylabel('Score')
plt.grid()
plt.show()

# Menghitung korelasi
correlation_score_popularity = df['Score'].corr(df['Popularity'])
print(f'Korelasi antara Score dan Popularity: {correlation_score_popularity}')
```
![image](https://github.com/user-attachments/assets/36f80916-8fcf-43ab-aa1e-65c3e0f3dd08)


```sh

# Scatter plot Episodes vs Duration
plt.figure(figsize=(8, 4))
sns.scatterplot(data=df, x='Episodes', y='Duration', color='orange')
plt.title('Episodes vs Duration')
plt.xlabel('Episodes')
plt.ylabel('Duration')
plt.grid()
plt.show()

# Menghitung korelasi
correlation_episodes_duration = df['Episodes'].corr(df['Duration'])
print(f'Korelasi antara Episodes dan Duration: {correlation_episodes_duration}')
```
