# Laporan Analisis Data Universitas Amerika Serikat

## PENDAHULUAN
Menggunakan data `universities.csv`, laporan ini bertujuan untuk menganalisis lanskap pendidikan tinggi di Amerika Serikat. Dataset ini mencakup berbagai metrik penting dari sejumlah universitas, mulai dari data demografis, jenis institusi (negeri vs swasta), biaya pendidikan (*tuition*), hingga indikator performa akademik seperti tingkat kelulusan. Analisis ini difokuskan untuk memahami distribusi tipe universitas, hubungan antara biaya yang dikeluarkan dengan tingkat kelulusan, serta mengidentifikasi wilayah geografis dengan biaya hidup paling terjangkau bagi mahasiswa.

## PREPARATION
Tahap ini berfokus pada pembersihan dan penyesuaian tipe data agar siap diolah:
1.  **Handling Missing Data:** Mengisi nilai yang hilang (*missing values*) pada kolom bertipe integer dan float menggunakan nilai median untuk menjaga distribusi data.
2.  **Column Renaming:** Mengubah nama kolom `Public (1)/ Private (2)` menjadi `Category` agar lebih mudah dibaca.
3.  **Data Type Conversion:** Menggunakan node *Number to String* untuk mengubah nilai indeks `1` menjadi "Public" dan `2` menjadi "Private", sehingga dapat dikategorikan dalam visualisasi.

## PROCESSING
Tahap pengolahan data dilakukan untuk mempersiapkan visualisasi yang spesifik:
1.  **Feature Engineering (Biaya Hidup):** Menggunakan node *Math Formula* untuk menjumlahkan kolom `room` dan `board` guna mendapatkan variabel baru yaitu "Total Living Cost".
2.  **Color Management:** Menggunakan node *Color Manager* untuk menetapkan skema warna yang konsisten (Biru untuk Public, Hijau untuk Private) guna memudahkan identifikasi pada Scatter Plot.
3.  **Aggregation (Untuk Bar Chart):** Menggunakan node *GroupBy* untuk mengelompokkan data berdasarkan `State` dan menghitung rata-rata (*mean*) dari "Total Living Cost".
4.  **Sorting & Filtering:** Menggunakan node *Sorter* (Ascending) pada hasil agregasi biaya hidup, kemudian menggunakan node *Row Filter* untuk hanya mengambil 10 negara bagian dengan rata-rata biaya hidup terendah.

## VISUALIZATION
Berikut adalah instrumen visualisasi yang digunakan dalam workflow:
* **Pie Chart:** Memvisualisasikan proporsi perbandingan jumlah antara universitas swasta (*Private*) dan negeri (*Public*).
  ![Proporsi Universitas Negeri vs Swasta](pie_chart_public_vs_private.png)
* **Scatter Plot:** Memetakan hubungan korelasi antara variabel `out-of-state tuition` (X) dengan `Graduation rate` (Y), dengan pembedaan warna berdasarkan kategori universitas.
  ![Hubungan Biaya Kuliah dan Tingkat Kelulusan](scatter_plot_tuition_vs_graduation.png)
* **Bar Chart:** Menampilkan peringkat 10 negara bagian (*State*) dengan rata-rata biaya hidup (*living cost*) termurah.
  ![10 Negara Bagian dengan Biaya Hidup Terendah](bar_chart_top10_cheapest_states.png)
* **Box Plot (Baru):** Membandingkan distribusi tingkat penerimaan (*Acceptance Rate*) antara kategori Public dan Private untuk melihat sebaran selektivitas dan mendeteksi adanya outliers.
  ![10 Negara Bagian dengan Biaya Hidup Terendah]()

## INSIGHT
Berdasarkan visualisasi yang dihasilkan, ditemukan beberapa wawasan kunci:

**1. Dominasi Institusi Swasta**
Berdasarkan Pie Chart, populasi universitas di Amerika Serikat didominasi oleh universitas swasta (*private*) dibandingkan universitas negeri (*public*). Hal ini menunjukkan banyaknya opsi institusi pendidikan mandiri yang tersedia di pasar pendidikan AS.

**2. Pola Geografis Biaya Hidup**
Analisis Bar Chart memperlihatkan pola geografis yang konsisten untuk biaya hidup terendah:
* **Pusat Wilayah Murah:** Negara bagian dengan biaya terendah terpusat di dua wilayah utama, yaitu **Midwest** (North Dakota, Nebraska, South Dakota) dan **Selatan** (Mississippi, Tennessee, Louisiana, Arkansas, Oklahoma).
* **Geographic Arbitrage:** Kehadiran negara bagian seperti Wyoming dan Utah dalam daftar 10 besar menyoroti peluang bagi mahasiswa untuk mendapatkan kualitas hidup yang tinggi dengan biaya rendah, jauh lebih terjangkau dibandingkan kawasan pesisir padat seperti New York atau California. Temuan ini mengindikasikan bahwa wilayah tengah dan selatan menjadi opsi paling strategis secara finansial bagi mahasiswa dengan anggaran terbatas.

**3. Korelasi Biaya Pendidikan dan Tingkat Kelulusan**
Analisis Scatter Plot menunjukkan adanya **korelasi positif** antara biaya kuliah dan tingkat kelulusan.
* **Institusi Swasta (Hijau):** Mendominasi area biaya tinggi (di atas $15,000) namun juga menguasai tingkat kelulusan tertinggi (di atas 80-90%). Ini menunjukkan bahwa biaya premium sering kali berbanding lurus dengan dukungan akademik yang lebih baik.
* **Institusi Negeri (Biru):** Terkonsentrasi di sisi kiri grafik (biaya lebih rendah, mayoritas di bawah $15,000) dengan tingkat kelulusan moderat (30-70%). Terdapat batas atas (*ceiling effect*) di mana jarang sekali universitas negeri yang memiliki biaya sangat tinggi.

## KESIMPULAN
Analisis ini menyimpulkan bahwa lanskap pendidikan tinggi AS menawarkan *trade-off* yang jelas antara biaya dan performa. Universitas swasta menawarkan peluang kelulusan tertinggi namun dengan biaya yang signifikan, sementara universitas negeri menyediakan akses pendidikan yang terjangkau dengan tingkat keberhasilan yang moderat.

Bagi calon mahasiswa dengan batasan anggaran, strategi terbaik adalah menargetkan universitas negeri yang berlokasi di wilayah Midwest atau Selatan AS. Kombinasi ini menawarkan efisiensi finansial ganda: biaya kuliah (*tuition*) yang lebih rendah dari sektor publik dan penghematan biaya hidup (*living cost*) dari faktor geografis, tanpa harus sepenuhnya mengorbankan kualitas pendidikan.
