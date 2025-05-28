# Laporan Proyek Machine Learning - Dhea Rachma Febiana - Rekomendasi Lagu Populer

## Project Overview

Revolusi digital mengubah cara bagaimana pelanggan menikmati dan mengakses musik secara signifikan.  Industri musik telah mengalami pergeseran menuju layanan streaming musik yang berbasis langganan sejak awal tahun 2000-an.  Dengan munculnya platform streaming musik seperti Spotify, Apple Music, Amazon Music, dan YouTube Music, pergeseran ini mencapai puncaknya di pasar musik global.  Sebuah laporan oleh International Federation of the Phonographic Industry (IFPI) menyatakan bahwa pada tahun 2024, streaming musik akan menyumbang lebih dari 67% dari pendapatan industri musik global, dengan total pendapatan diperkirakan mencapai $17.5 miliar.  Fenomena ini tidak hanya mengubah struktur bisnis industri musik, tetapi juga menimbulkan masalah baru tentang cara pengguna mendengarkan dan menemukan musik.

Spotify, yang diluncurkan pada tahun 2006 di Swedia, telah berkembang menjadi salah satu platform streaming musik terbesar dan paling berpengaruh di dunia. Per tahun 2024, Spotify melayani lebih dari 500 juta pengguna aktif bulanan di lebih dari 180 negara, dengan lebih dari 220 juta pengguna premium dan menyediakan akses ke lebih dari 100 juta lagu serta 5 juta podcast. Platform ini tidak hanya berfungsi sebagai perpustakaan musik digital, tetapi juga sebagai platform discovery yang memungkinkan pengguna menemukan musik baru melalui berbagai fitur seperti Discover Weekly, Release Radar, dan Daily Mix. Keberhasilan Spotify dalam mempertahankan posisinya sebagai market leader tidak terlepas dari investasi besar dalam teknologi machine learning dan artificial intelligence untuk sistem rekomendasinya, yang menjadi salah satu diferensiasi utama platform ini dari kompetitor.

Pengguna layanan streaming musik seperti Spotify sering kali dihadapkan pada tantangan menemukan **lagu populer** yang sesuai dengan selera mereka dari koleksi musik yang tersedia. Meskipun algoritma rekomendasi sudah banyak digunakan, sistem ini terkadang menyarankan lagu-lagu yang kurang dikenal atau tidak sesuai dengan ekspektasi pengguna, terutama mereka yang lebih memilih untuk tetap mendengarkan lagu-lagu yang sudah terbukti populer. Lagu-lagu populer memiliki keunggulan karena telah mendapatkan penerimaan luas dari publik, sering kali ditandai dengan tingginya jumlah streaming, keberadaan dalam tangga lagu, atau penempatan dalam playlist utama. Oleh karena itu, membangun sistem rekomendasi yang secara khusus **berfokus pada lagu-lagu populer** akan memberikan nilai tambah bagi pengguna yang menginginkan eksplorasi musik baru tanpa keluar dari zona kenyamanan popularitas.

Penelitian menunjukkan bahwa pengguna cenderung lebih sering mengeksplorasi musik baru jika rekomendasi yang diterima berada dalam lingkup genre atau popularitas yang familiar. Dengan demikian, sistem rekomendasi lagu populer ini tidak hanya relevan dari sisi teknis, tetapi juga mendukung kebutuhan psikologis pengguna akan keakraban dan kenyamanan dalam pengalaman mendengarkan musik (Celma.,2010).

##### Mengapa dan Bagaimana Masalah Ini Harus Diselesaikan
Masalah ini perlu diselesaikan karena meskipun platform streaming musik seperti Spotify telah menyediakan daftar lagu-lagu populer, tidak semua lagu populer tersebut sesuai dengan preferensi audio masing-masing pengguna. Tanpa sistem yang mampu memahami karakteristik konten musik, pengguna bisa kesulitan menemukan lagu populer yang benar-benar cocok dengan selera mereka—misalnya dari segi energi, tempo, valensi, atau danceability. Hal ini dapat menurunkan tingkat kepuasan, keterlibatan, dan loyalitas pengguna terhadap platform.

Untuk menjawab permasalahan tersebut, proyek ini menggunakan pendekatan Content-Based Filtering, di mana setiap lagu populer direpresentasikan dalam bentuk vektor fitur numerik berdasarkan atribut audionya. Sistem kemudian merekomendasikan lagu-lagu populer lain yang memiliki profil audio serupa. Pendekatan ini sangat ideal dalam konteks cold-start (pengguna baru), serta menjaga konsistensi suasana musik dalam daftar rekomendasi. Studi oleh Wang et al. (2021) menunjukkan bahwa sistem rekomendasi berbasis konten dengan cosine similarity dapat menghasilkan rekomendasi yang relevan dan akurat, meskipun tanpa riwayat interaksi pengguna yang panjang.

##### Referensi
Celma, Ò. (2010). Music recommendation and discovery: The long tail, long fail, and long play in the digital music space. Springer. https://www.researchgate.net/publication/220692469



## Business Understanding

Dalam industri musik digital, pengguna sering kali mengalami kesulitan dalam menemukan lagu-lagu baru yang sesuai dengan preferensi pribadi mereka. Platform seperti Spotify memiliki katalog yang sangat besar, namun tidak semua lagu populer relevan dengan selera setiap pengguna. Oleh karena itu, penting untuk memahami bagaimana sistem rekomendasi dapat membantu pengguna menjelajahi musik baru yang mirip secara audio dengan lagu favorit mereka, meskipun tidak selalu memiliki tingkat popularitas yang sama.


### Problem Statements
- Pengguna kesulitan menemukan lagu populer yang cocok dengan preferensi pribadinya secara audio.
Meskipun platform menyediakan banyak opsi populer, belum tentu lagu-lagu tersebut cocok secara karakteristik musik (misal: mood, tempo, atau energi) dengan selera pengguna.


### Goals
- Membangun sistem rekomendasi lagu yang mampu menyarankan lagu-lagu baru berdasarkan kesamaan fitur audio dengan lagu yang disukai pengguna. Fitur audio mencakup energi, tempo, valensi, danceability, liveness, dan lain-lain yang memengaruhi karakteristik musik.


### Solution statements
- Content-Based Filtering menggunakan fitur audio numerik dan cosine similarity.
Pendekatan ini membandingkan fitur numerik antar lagu dan mengukur kedekatan menggunakan cosine similarity, sehingga lagu yang direkomendasikan akan memiliki karakteristik audio yang serupa dengan lagu acuan.
- Integrasi optional PCA untuk efisiensi dimensi dan kecepatan komputasi.
PCA digunakan untuk mereduksi kompleksitas fitur numerik sebelum menghitung similarity, menjaga performa dan skalabilitas sistem.

## Data Understanding
Dataset yang digunakan dalam proyek ini adalah Spotify Music Dataset, yang tersedia publik di Kaggle. Dataset ini berisi informasi dari lagu-lagu dengan tingkat popularitas tinggi. Data awal terdiri dari 1686 baris dan 29 kolom, namun setelah proses pembersihan (cleaning), jumlah baris berkurang menjadi 1685 baris karena ditemukan satu baris data yang memiliki missing value pada kolom track_album_name, dan baris tersebut dihapus untuk menjaga kualitas data. Dan tidak ditemukan data duplikat setelah dilakukan pengecekan.
Dataset: https://www.kaggle.com/datasets/solomonameh/spotify-music-dataset?select=high_popularity_spotify_data.csv

#### Variabel yang Digunakan (untuk modelling dan similarity): 
- energy (float): Intensitas dan kekuatan lagu
- danceability (float): Kesesuaian lagu untuk menari
- valence (float): Suasana/positif-negatif emosional lagu
- tempo (float): Kecepatan beat (BPM)
- loudness (float): Volume keseluruhan lagu
- speechiness (float): Keberadaan spoken word
- acousticness (float): Tingkat ke-akustikan
- instrumentalness (float): Probabilitas lagu bersifat instrumental
- liveness (float): Kemungkinan live performance
- playlist_genre (kategori): Genre playlist (diubah menjadi one-hot encoding untuk modelling)
- track_name, track_artist (untuk identifikasi lagu saat output)

#### Variabel yang Dibuang
- track_href, uri, analysis_url, id, track_id, track_album_id, playlist_id: Merupakan URL/ID teknis dari sistem Spotify dan tidak memiliki kontribusi dalam analisis fitur audio.
- type: Sama untuk seluruh data (audio_features), tidak informatif.

#### Variabel yang Tidak Digunakan dalam Modelling, tetapi tetap dipertahankan untuk referensi:
- track_popularity: Tidak digunakan karena rekomendasi tidak berbasis popularitas.
- track_album_release_date: Informasi tanggal, tidak relevan dalam model berbasis konten audio.
- playlist_subgenre: Redundan dengan playlist_genre.
- mode, key, duration_ms, time_signature: Tidak dipilih karena kontribusi terhadap similarity dianggap minimal berdasarkan korelasi dan eksperimen awal.

### Exploratory Data Analysis (EDA)
1. Analisis Univariate
   
  ```
for col in numerical_cols:
    print(f"📌 Variabel: {col}")
    print("Tipe data:", df[col].dtype)
    print("Jumlah nilai unik:", df[col].nunique())
    print("Nilai minimum:", df[col].min())
    print("Nilai maksimum:", df[col].max())
    print("Rata-rata:", df[col].mean())
    print("Median:", df[col].median())
    print("Standar deviasi:", df[col].std())
    print("-" * 50)
```
![image](https://github.com/user-attachments/assets/be4ac6fd-4518-4fdb-8665-345cd74fb35b)

Langkah pertama adalah melakukan analisis univariat terhadap 10 fitur numerik berikut:
energy, danceability, valence, tempo, loudness, speechiness, acousticness, instrumentalness, liveness, dan track_popularity

Untuk setiap variabel di atas, dihitung statistik deskriptif seperti tipe data, jumlah nilai unik, nilai minimum dan maksimum, rata-rata, median, dan standar deviasi. Hasil ini membantu melihat apakah terdapat nilai ekstrim, distribusi miring (skewed), atau variabel yang memiliki rentang nilai yang terlalu sempit/lebar.

2. Visualisasi Distribusi
```
sns.set(style="whitegrid")
plt.figure(figsize=(16, 20))

# Kolom numerik yang ingin dieksplorasi

numerical_cols = ['energy', 'danceability', 'valence', 'tempo', 
                  'loudness', 'speechiness', 'acousticness', 
                  'instrumentalness', 'liveness', 'track_popularity']

# Plot histogram tiap variabel
for i, col in enumerate(numerical_cols, 1):
    plt.subplot(5, 2, i)
    sns.histplot(df[col], kde=True, color='skyblue')
    plt.title(f'Distribusi: {col}')
    plt.xlabel(col)
    plt.ylabel('Frekuensi')

plt.tight_layout()
plt.show()
```
![image](https://github.com/user-attachments/assets/be0c2155-ce2b-4777-aa16-be2c70edc5a6)

Visualisasi distribusi fitur menunjukkan bahwa lagu-lagu populer dalam dataset umumnya memiliki tingkat energi dan danceability yang tinggi, dengan sebaran valence yang beragam. Tempo lagu cenderung berkelompok di sekitar 100–120 BPM, sedangkan fitur seperti speechiness, acousticness, dan instrumentalness mendekati nol, menandakan mayoritas lagu populer bersifat vokal, studio-produced, dan tidak akustik. Distribusi ini mendukung pemilihan fitur numerik sebagai dasar yang relevan untuk sistem rekomendasi berbasis konten.

## Data Preparation
1. Menghapus Missing Value dan Duplikasi Data
```
df_clean = df.dropna().drop_duplicates()

```
Ditemukan 1 nilai kosong pada kolom track_album_name, sehingga dilakukan penghapusan baris tersebut menggunakan dropna(). Setelah proses pembersihan, dilakukan pengecekan dan penghapusan duplikasi dengan drop_duplicates() agar tidak ada lagu yang memengaruhi distribusi atau perhitungan similarity secara berlebihan.

2. Seleksi Fitur Numerik
```
features = [
    'energy', 'danceability', 'valence', 'tempo', 'loudness',
    'speechiness', 'acousticness', 'instrumentalness', 'liveness'
]
```
Dipilih 9 fitur numerik utama (energy, danceability, valence, tempo, loudness, speechiness, acousticness, instrumentalness, liveness) sebagai dasar perhitungan similarity karena fitur ini mencerminkan karakteristik audio secara langsung.

3. Normalisasi (Standardization)
```
scaler = StandardScaler()
X_scaled = scaler.fit_transform(df_clean[features])
df_scaled = pd.DataFrame(X_scaled, columns=features)
```
Fitur numerik dinormalisasi menggunakan StandardScaler() agar semua fitur memiliki skala yang seragam. Ini penting karena cosine similarity sensitif terhadap skala antar fitur.

4. One-Hot Encoding untuk Variabel Kategori
```
df_encoded = pd.get_dummies(df_clean['playlist_genre'])
```
Kolom playlist_genre diubah menjadi representasi numerik menggunakan teknik one-hot encoding untuk memasukkan aspek genre dalam vektor fitur lagu.

5. Penggabungan Fitur
```
X_combined = pd.concat([df_scaled.reset_index(drop=True), df_encoded.reset_index(drop=True)], axis=1)
```
Hasil normalisasi fitur numerik (df_scaled) dan hasil encoding kategori (df_encoded) digabung menggunakan pd.concat() untuk membentuk dataset akhir yang siap digunakan.

6. Dimensionality Reduction (PCA)
```
use_pca = True
if use_pca:
    pca = PCA(n_components=0.95)
    X_final = pd.DataFrame(pca.fit_transform(X_combined))
else:
    X_final = X_combined.copy()

print("Jumlah baris dan kolom hasil PCA (X_final):", X_final.shape)
```
Untuk meningkatkan efisiensi komputasi dan mengurangi redundansi fitur, digunakan Principal Component Analysis (PCA) dengan n_components=0.95. Ini berarti model hanya mempertahankan komponen-komponen yang secara kumulatif menjelaskan 95% variansi dalam data.

7. Pemisahan Metadata
```
df_metadata = df_clean[['track_name', 'track_artist', 'playlist_genre']].reset_index(drop=True)
```
Kolom track_name, track_artist, dan playlist_genre dipisahkan ke dalam variabel df_metadata agar tidak ikut terlibat dalam proses perhitungan cosine similarity, namun tetap tersedia untuk keperluan identifikasi hasil rekomendasi.

## Modeling
Pada tahap ini, sistem rekomendasi dibangun menggunakan pendekatan Content-Based Filtering. Pendekatan ini memanfaatkan kesamaan konten antar lagu yang direpresentasikan oleh fitur numerik audio. Teknik perhitungan yang digunakan adalah cosine similarity, yang menghitung kedekatan antar vektor fitur audio dari masing-masing lagu.

1. Perhitungan Cosine Similarity
```
similarity_matrix = cosine_similarity(X_final)

```
Setelah fitur numerik dari lagu diproses dan direduksi (dengan atau tanpa PCA), cosine similarity dihitung menggunakan fungsi cosine_similarity() dari sklearn. Hasilnya berupa matriks 2 dimensi (similarity_matrix) yang berisi nilai kemiripan antara semua pasangan lagu.

2. Pemetaan Indeks ke Judul Lagu
```
similarity_df = pd.DataFrame(similarity_matrix, 
                             index=df_clean['track_name'], 
                             columns=df_clean['track_name'])
similarity_df.head()

```
Untuk mempermudah pembacaan dan pemanggilan hasil rekomendasi, hasil similarity diubah menjadi DataFrame (similarity_df) dengan indeks dan kolom berupa nama lagu (track_name).

3. Fungsi Rekomendasi recommend_similar_songs()
```
def recommend_similar_songs(song_name, top_n=5):
    if song_name not in df_clean['track_name'].values:
        print(f"❌ Lagu '{song_name}' tidak ditemukan dalam dataset.")
        return

    idx = df_clean[df_clean['track_name'] == song_name].index[0]

    sim_scores = list(enumerate(similarity_matrix[idx]))

    sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)[1:top_n+1]

    song_indices = [i[0] for i in sim_scores]
    similarities = [i[1] for i in sim_scores]

    recommended = df_clean.iloc[song_indices][['track_name', 'track_artist', 'playlist_genre']].copy()
    recommended['similarity_score'] = similarities

    return recommended.reset_index(drop=True)

```
Fungsi ini merupakan inti dari sistem rekomendasi. Berikut rincian langkah di dalamnya:
- Pengecekan Input: Fungsi akan memeriksa apakah song_name yang dimasukkan oleh pengguna tersedia dalam dataset. Jika tidak ditemukan, sistem akan mengeluarkan peringatan.
- Identifikasi Lagu Target: Fungsi mengambil index dari lagu yang dicari di dalam df_clean.
- Pengambilan Skor Similarity: Dengan menggunakan index tersebut, sistem mengambil satu baris dari similarity_matrix, yang berisi skor kemiripan lagu target terhadap semua lagu lain.
- Pengurutan & Pemilihan Lagu Mirip: Skor similarity diurutkan dari tertinggi ke terendah (kecuali diri sendiri), lalu dipilih top_n lagu teratas sebagai kandidat rekomendasi.
- Ambil Metadata Lagu: Fungsi mengambil nama lagu, nama artis, dan genre dari df_clean berdasarkan index yang dipilih, dan menambahkan kolom similarity_score.
Output: Fungsi mengembalikan tabel rekomendasi yang telah diurutkan berdasarkan kemiripan dengan lagu input pengguna.

4. Contoh Penggunaan
```
recommend_similar_songs("Ghostride")
```
Jika pengguna memasukkan "Ghostride", sistem akan merekomendasikan 5 lagu teratas yang paling mirip dari sisi fitur audio, seperti berikut:

| No | track_name                               | track_artist                                        | playlist_genre | similarity_score |
|----|-------------------------------------------|-----------------------------------------------------|----------------|------------------|
| 1  | Ghostride                                 | Crumb                                               | pop            | 0.969791         |
| 2  | Experience                                | Ludovico Einaudi, Daniel Hope, I Virtuosi Italiani | classical      | 0.899723         |
| 3  | Anchor                                    | Novo Amor                                           | ambient        | 0.895345         |
| 4  | Instant Crush (feat. Julian Casablancas) | Daft Punk, Julian Casablancas                      | rock           | 0.879868         |
| 5  | Black Friday (pretty like the sun)        | Lost Frequencies, Tom Odell                         | gaming         | 0.875253         |


## Evaluation
1. Distribusi Skor Cosine Similarity
Untuk memahami pola kemiripan antar lagu secara keseluruhan, semua nilai dari matriks similarity diubah menjadi satu array menggunakan .flatten(), kemudian divisualisasikan dalam bentuk histogram.

![image](https://github.com/user-attachments/assets/b49a39f2-07e8-4968-8d2c-21fb4e631219)

Hasil visualisasi menunjukkan bahwa sebagian besar pasangan lagu memiliki skor similarity rendah (< 0.5), sementara hanya sebagian kecil yang memiliki skor tinggi (> 0.8). Ini menunjukkan bahwa sistem mampu membedakan karakteristik audio antar lagu dengan cukup baik, dan hanya menganggap sedikit lagu yang benar-benar mirip — hal yang ideal dalam sistem rekomendasi berbasis konten.

2.  Intra-List Similarity (ILS)
Metrik utama yang digunakan adalah Intra-List Similarity (ILS). ILS mengukur konsistensi kemiripan antar item dalam satu daftar rekomendasi. Semakin tinggi skor ILS, semakin mirip item-item dalam daftar tersebut — artinya sistem berhasil memberikan hasil yang homogen secara konten.

Formula ILS:
ILS dihitung sebagai rata-rata skor cosine similarity antar item yang direkomendasikan, tanpa menyertakan diagonal (diri sendiri). 

![image](https://github.com/user-attachments/assets/1ba42581-6136-43e7-837f-4da29d45210f)

di mana **𝑁** adalah jumlah item dalam daftar rekomendasi.

Hasil Evaluasi:
Contoh evaluasi dengan input lagu "Ghostride" menghasilkan rekomendasi dengan skor ILS sekitar 0.62. Artinya, lagu-lagu yang direkomendasikan memiliki tingkat kemiripan internal yang cukup tinggi, sesuai dengan pendekatan content-based filtering. Ini menunjukkan bahwa sistem dapat mengembalikan daftar lagu yang secara karakteristik audio konsisten dan sesuai dengan lagu acuan.

