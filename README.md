# Klaster-Film-Disney-Mengungkap-Pola-Genre-dan-Pendapatan-ML
Proyek ini bertujuan untuk menganalisis dan mengelompokkan film-film Disney berdasarkan karakteristik genre, peringkat MPAA (Motion Picture Association of America), dan pendapatan yang disesuaikan dengan inflasi. Dengan menggunakan teknik clustering K-Means dan reduksi dimensi PCA, kami mengidentifikasi pola-pola menarik dalam dataset film Disney.

## Daftar Isi
- [Tentang Proyek](#tentang-proyek)
- [Dataset](#dataset)
- [Metodologi](#metodologi)
- [Hasil Analisis Klaster](#hasil-analisis-klaster)
- [Visualisasi](#visualisasi)
- [Persyaratan](#persyaratan)
- [Instalasi](#instalasi)
- [Penggunaan](#penggunaan)
- [Kontribusi](#kontribusi)
- [Lisensi](#lisensi)
- [Kontak](#kontak)

## Tentang Proyek

Proyek ini merupakan studi eksplorasi data pada dataset film Disney. Tujuan utamanya adalah untuk:
- Melakukan *data preprocessing* pada data film Disney, termasuk penanganan nilai yang hilang dan *encoding* fitur kategorikal.
- Menerapkan algoritma *clustering* K-Means untuk mengelompokkan film berdasarkan fitur-fitur yang dipilih (genre, MPAA rating, pendapatan).
- Menggunakan Principal Component Analysis (PCA) untuk reduksi dimensi agar hasil *clustering* dapat divisualisasikan.
- Menganalisis karakteristik masing-masing klaster untuk mendapatkan wawasan tentang film-film Disney.

## Dataset

Dataset yang digunakan adalah `disney_movies.csv` yang berisi informasi tentang film-film yang dirilis oleh Disney, meliputi kolom-kolom berikut:
- `movie_title`: Judul film
- `release_date`: Tanggal rilis film
- `genre`: Genre film
- `mpaa_rating`: Peringkat MPAA film (G, PG, PG-13, R, Not Rated)
- `total_gross`: Pendapatan kotor total film
- `inflation_adjusted_gross`: Pendapatan kotor yang disesuaikan dengan inflasi

## Metodologi

Proyek ini mengikuti langkah-langkah metodologi sebagai berikut:

1.  **Pemuatan Data**: Membaca dataset `disney_movies.csv` ke dalam Pandas DataFrame.
2.  **Eksplorasi Data Awal**:
    * Memeriksa informasi umum DataFrame (`df.info()`).
    * Melihat beberapa baris data teratas (`df.head()`).
    * Memeriksa dan menangani nilai-nilai yang hilang (NaN) dengan menghapusnya.
3.  ***Clustering* Berdasarkan Genre dan *MPAA Rating***:
    * Membersihkan spasi ekstra pada kolom `genre` dan `mpaa_rating`.
    * Menerapkan *One-Hot Encoding* pada kolom `genre` dan `mpaa_rating`.
    * Melakukan *clustering* K-Means dengan `n_clusters=5`.
    * Menerapkan PCA untuk mereduksi dimensi menjadi 2 komponen untuk visualisasi.
    * Menganalisis informasi dominan untuk setiap klaster (jumlah film, genre dominan, MPAA rating dominan).
    * Membuat *scatterplot* PCA untuk memvisualisasikan klaster.
4.  ***Clustering* Berdasarkan Genre dan Pendapatan yang Disesuaikan Inflasi**:
    * Memilih kolom `genre` dan `inflation_adjusted_gross`.
    * Melakukan *One-Hot Encoding* pada kolom `genre`.
    * Menggabungkan fitur genre yang sudah di-*encode* dengan pendapatan.
    * Melakukan *Standard Scaling* pada fitur gabungan.
    * Menggunakan Metode *Elbow* untuk menentukan jumlah klaster (k) yang optimal.
    * Menerapkan *clustering* K-Means dengan `n_clusters=3` (berdasarkan hasil *Elbow Method*).
    * Menerapkan PCA untuk visualisasi hasil *clustering*.
    * Mengubah label klaster dari 0, 1, 2 menjadi 1, 2, 3 untuk keterbacaan.
    * Menganalisis dan menyusun narasi hasil *clustering*, termasuk jumlah film, rata-rata pendapatan, rentang pendapatan, dan genre dominan untuk setiap klaster.

## Hasil Analisis Klaster

### Klastering Berdasarkan Genre dan MPAA Rating

| Cluster | Number of Films | Dominant Genre | Dominant MPAA Rating |
| :------ | :-------------- | :------------- | :------------------- |
| 0       | 53              | Drama          | PG                   |
| 1       | 182             | Comedy         | PG                   |
| 2       | 129             | Action         | PG-13                |
| 3       | 129             | Adventure      | PG                   |
| 4       | 86              | Drama          | PG-13                |

### Klastering Berdasarkan Genre dan Pendapatan (Inflation-Adjusted Gross)

Berdasarkan analisis klaster ini, film-film Disney dapat dikelompokkan menjadi tiga kategori utama berdasarkan genre dan performa pendapatan mereka yang disesuaikan dengan inflasi:

-   **🟢 Klaster 1: Kelompok Berpendapatan Tertinggi.**
    * Genre dominan: Comedy
    * Jumlah film: 405 film
    * Rata-rata pendapatan: $124,573,028
    * Rentang pendapatan: $2,984 s.d. $5,228,953,251
    * *Wawasan*: Klaster ini merupakan kelompok terbesar dan memiliki rata-rata pendapatan tertinggi, didominasi oleh film-film bergenre Komedi. Rentang pendapatan yang sangat lebar menunjukkan adanya beberapa *blockbuster* komedi yang sangat sukses, menarik banyak penonton dan menghasilkan pendapatan besar.

-   **🟢 Klaster 2: Kelompok Berpendapatan Sedang.**
    * Genre dominan: Thriller/Suspense
    * Jumlah film: 21 film
    * Rata-rata pendapatan: $96,464,069
    * Rentang pendapatan: $3,957,025 s.d. $485,424,724
    * *Wawasan*: Meskipun jumlah filmnya lebih sedikit dibandingkan klaster 1, klaster ini menunjukkan performa pendapatan yang solid, dengan genre *Thriller/Suspense* menjadi yang paling umum. Kisaran pendapatannya menunjukkan konsistensi dalam menarik minat penonton untuk genre ini.

-   **🟢 Klaster 3: Kelompok Berpendapatan Terendah.**
    * Genre dominan: Romantic Comedy
    * Jumlah film: 21 film
    * Rata-rata pendapatan: $79,272,868
    * Rentang pendapatan: $907,414 s.d. $356,389,765
    * *Wawasan*: Klaster ini memiliki jumlah film yang sama dengan klaster 2 tetapi dengan rata-rata pendapatan terendah. Film-film bergenre Komedi Romantis cenderung memiliki pendapatan yang lebih moderat, dengan beberapa pengecualian di batas atas rentang.

## Visualisasi

Proyek ini menghasilkan beberapa visualisasi penting, terutama *scatterplot* PCA yang menunjukkan hasil *clustering*. Visualisasi ini membantu dalam memahami bagaimana film-film dikelompokkan berdasarkan fitur-fitur yang digunakan.

## Persyaratan

Pastikan Anda memiliki Python terinstal di sistem Anda. Proyek ini juga memerlukan beberapa pustaka Python yang dapat diinstal melalui `pip`.
