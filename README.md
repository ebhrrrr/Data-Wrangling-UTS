## "Dari Data Mentah ke Dataset Siap Analisis: Harga Pangan Jawa Timur 2024"

## 1. Deskripsi Proyek

Proyek ini merupakan pengerjaan untuk penilaian tengah semester mata kuliah Data Wrangling, dimana berisikian implementasi proses data wrangling untuk mengolah dan menganalisis data harga komoditas pangan serta data cuaca di beberapa kabupaten/kota di provinsi Jawa Timur. 

Dengan data harga komoditas diperoleh dari Pusat Informasi Harga Pangan Strategis (PIHPS), sedangkan data cuaca diperoleh dari National Oceanic and Atmospheric Administration (NOAA).

Proses pengolahan dilakukan untuk menghasilkan dataset yang terstruktur dan siap digunakan dalam analisis. Analisis difokuskan pada tingkat fluktuasi harga komoditas dan hubungan antara curah hujan dengan harga cabai rawit merah.

## 2. Tujuan Proyek

1. Menggabungkan dan membersihkan data harga komoditas dari berbagai periode.
2. Mengubah struktur data harga dari format wide menjadi long.
3. Menyesuaikan tipe data dan menangani nilai yang tidak tersedia.
4. Mengolah data cuaca harian menjadi data mingguan.
5. Menggabungkan data harga dan cuaca berdasarkan wilayah dan periode waktu.
6. Menganalisis komoditas dengan tingkat fluktuasi harga tertinggi.
7. Menganalisis kecenderungan harga cabai rawit merah setelah periode curah hujan tinggi.

## 3. Sumber Data

### A. Data Harga Komoditas

Sumber: Pusat Informasi Harga Pangan Strategis (PIHPS).

File yang digunakan:
- `pihps_pasar_tradisional_jatim_2024.xlsx`

Data mencakup harga komoditas pangan di sembilan kabupaten/kota di Jawa Timur:
- Kabupaten Banyuwangi
- Kabupaten Jember
- Kabupaten Sumenep
- Kota Blitar
- Kota Kediri
- Kota Madiun
- Kota Malang
- Kota Probolinggo
- Kota Surabaya

### B. Data Cuaca

Sumber: National Oceanic and Atmospheric Administration (NOAA).

Data cuaca berisi informasi pengamatan stasiun cuaca, termasuk suhu dan curah hujan. Data ini digunakan untuk menganalisis kondisi cuaca pada wilayah yang memiliki stasiun pengamatan.

### C. Data Referensi Wilayah

File: `kode_wilayah_jatim.csv`

Data referensi digunakan untuk membantu proses pencocokan kode administratif wilayah antara dataset harga dan dataset cuaca.

## 4. Komoditas yang Dianalisis

Lima komoditas yang digunakan dalam analisis adalah:

1. Beras Kualitas Medium I
2. Cabai Rawit Merah
3. Bawang Merah Ukuran Sedang
4. Telur Ayam Ras Segar
5. Gula Pasir Lokal

## 5. Struktur Folder

```text
DATA-WRANGLING/
│
├── data_raw/
│   ├── pihps_pasar_tradisional_jatim_2024.xlsx
│   ├── pihps_pasar_tradisional_jatim_2025H1.xlsx
│   ├── data_noaa.csv
│   └── kode_wilayah_jatim.csv
│
├── data_processed/
│   ├── harga_long.csv
│   ├── harga_analisis.csv
│   ├── harga_mingguan.csv
│   ├── cuaca_harian.csv
│   ├── cuaca_mingguan.csv
│   └── data_akhir.csv
│
├── output/
│   ├── statistik_harga.csv
│   ├── komoditas_bergejolak.csv
│   ├── perbandingan_hujan.csv
│   └── grafik/
│
├── notebook/
│   └── analisis.ipynb
│
└── README.md
```

## 6. Tahapan Data Wrangling

### 6.1 Data Loading

Memuat dataset harga komoditas dari file Excel, data cuaca dari NOAA, serta data referensi kode wilayah.

### 6.2 Data Cleaning

Melakukan pembersihan data, meliputi:
- Menghapus spasi yang tidak diperlukan.
- Mengubah tanda `-` menjadi nilai kosong (`NaN`).
- Menghapus tanda koma pada angka harga agar dapat dibaca sebagai nilai numerik.
- Mengubah kode data khusus NOAA menjadi nilai kosong.
- Memeriksa data kosong dan kesesuaian format.

### 6.3 Data Transformation

Melakukan transformasi data, meliputi:
- Mengubah data harga dari format wide menjadi long.
- Mengubah kolom tanggal menjadi tipe datetime.
- Mengubah kolom harga menjadi tipe numerik.
- Mengubah suhu dari Fahrenheit menjadi Celsius.
- Mengubah curah hujan dari inci menjadi milimeter.
- Mengubah data cuaca harian menjadi data mingguan.
- Membuat fitur tambahan seperti Z-score dan persentase perubahan harga.

### 6.4 Data Integration

Menggabungkan dataset harga dan cuaca menggunakan kode wilayah serta periode minggu sebagai kunci penggabungan.

Pada analisis hubungan curah hujan dan harga, data curah hujan juga digeser satu minggu untuk membandingkan kondisi hujan pada minggu sebelumnya dengan harga komoditas pada minggu berikutnya.

### 6.5 Data Validation

Melakukan pemeriksaan terhadap:
- Tipe data setiap kolom.
- Jumlah nilai kosong.
- Duplikasi data.
- Kesesuaian kode wilayah.
- Kesesuaian periode waktu.
- Hasil penggabungan dataset.

## 7. Kamus Data (Data Dictionary)

Kamus data menjelaskan nama kolom, tipe data, dan fungsi setiap atribut yang digunakan dalam dataset hasil pengolahan.

### Dataset Akhir (`data_akhir`)


| Nama Kolom | Keterangan |
|---|---|
| `kode` | Kode administratif wilayah. |
| `minggu` | Periode minggu pengamatan. |
| `harga_cabai_rawit_merah` | Rata-rata harga cabai rawit merah mingguan. |
| `jumlah_hari_harga` | Jumlah hari dengan data harga. |
| `curah_hujan_mm` | Total curah hujan mingguan (mm). |
| `suhu_rata_rata` | Rata-rata suhu mingguan (°C). |
| `jumlah_hari_cuaca` | Jumlah hari dengan data cuaca. |
| `jumlah_hari_hujan_tercatat` | Jumlah hari dengan data curah hujan valid. |
| `nama_wilayah` | Nama kabupaten/kota. |
| `kepadatan_penduduk` | Kepadatan penduduk wilayah. |
| `jumlah_kecamatan` | Jumlah kecamatan. |
| `jumlah_kelurahan` | Jumlah kelurahan. |
| `jumlah_desa` | Jumlah desa. |

## 8. Analisis Data

### 8.1 Analisis Fluktuasi Harga Komoditas

Analisis dilakukan dengan menghitung koefisien variasi (Coefficient of Variation/CV) untuk mengetahui tingkat keragaman harga setiap komoditas pada masing-masing kabupaten/kota.

Rumus:

\[
CV = \frac{\text{Standar Deviasi}}{\text{Rata-rata}} \times 100\%
\]

Semakin tinggi nilai CV, semakin besar fluktuasi harga komoditas relatif terhadap rata-ratanya.

### 8.2 Analisis Hubungan Curah Hujan dan Harga Cabai Rawit

Analisis dilakukan dengan membandingkan rata-rata harga cabai rawit merah pada minggu setelah periode hujan tinggi dan minggu setelah periode hujan tidak tinggi.

Kategori hujan tinggi ditentukan berdasarkan kuartil ketiga (Q3) curah hujan pada masing-masing wilayah. Analisis ini digunakan untuk melihat kecenderungan perubahan harga, bukan untuk membuktikan hubungan sebab-akibat.

## 9. Tools dan Library

Tools dan library yang digunakan:
- Python
- Google Colab / Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn
- OpenPyXL

## 10. Output Proyek

Hasil akhir dari proyek ini meliputi:
- Dataset harga komoditas dalam format long.
- Dataset harga mingguan.
- Dataset cuaca harian dan mingguan.
- Dataset hasil integrasi harga dan cuaca.
- Tabel statistik harga dan koefisien variasi.
- Tabel komoditas dengan fluktuasi harga tertinggi pada setiap wilayah.
- Tabel perbandingan harga cabai rawit setelah periode hujan tinggi dan tidak tinggi.
- Visualisasi hasil analisis.

## 11. Kesimpulan

Proyek ini menerapkan tahapan data wrangling mulai dari pemuatan data, pembersihan, transformasi, integrasi, hingga validasi. Hasil pengolahan digunakan untuk menganalisis fluktuasi harga komoditas pangan serta kecenderungan harga cabai rawit merah setelah periode curah hujan tinggi di beberapa wilayah Jawa Timur.

Melalui proses tersebut, data dari sumber dan format yang berbeda dapat disusun menjadi dataset yang lebih terstruktur dan siap digunakan untuk analisis lebih lanjut.

## 12. Cara Menjalankan Proyek

1. Unduh atau siapkan seluruh dataset pada folder `data_raw`.
2. Buka file notebook pada folder `notebook`.
3. Pastikan library yang dibutuhkan sudah terpasang.
4. Sesuaikan lokasi file dataset dengan struktur folder.
5. Jalankan setiap sel notebook secara berurutan.
6. Simpan hasil pengolahan pada folder `data_processed` dan hasil analisis pada folder `output`.
