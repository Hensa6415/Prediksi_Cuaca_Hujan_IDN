1. Perlu melakukan install depedensi/library.

pip install numpy pandas matplotlib seaborn

(Catatan Pastikan Depedensi/Library PIP sudah terinstall)

2. Jika sudah tinggal jalankan.

python main.py


A. Pendahuluan
Tujuan Proyek: 
Proyek ini bertujuan untuk membangun sebuah sistem kecerdasan buatan (Machine Learning),
yang dapat memprediksi apakah hujan akan turun dalam 6 jam ke depan atau tidak.

Kenapa ini penting?: 
Prediksi cuaca jangka pendek sangat berguna untuk berbagai hal, 
mulai dari perencanaan aktivitas harian, pertanian, hingga mitigasi bencana skala kecil.

Pendekatan: 
Alih-alih menggunakan model AI instan yang sudah jadi, 
proyek ini membangun model algoritma Logistic Regression (Regresi Logistik),
secara murni (dari nol) menggunakan perhitungan matematika dasar, agar kita benar-benar memahami cara kerja AI di belakang layar.

B. Dataset (Dari Mana Datanya?)
Sumber Data: 
Saya menggunakan dataset historis cuaca ("Kaggle Indonesia Hourly Weather for Rain Prediction").
https://www.kaggle.com/datasets/karanroyka/indonesia-hourly-weather-for-rain-prediction 
Data ini berisi catatan cuaca per jam dari berbagai kota di Indonesia.

- Fitur Cuaca (Variabel Input): Model ini belajar dari 6 faktor cuaca utama:

    Suhu (Temperature)

    Kelembapan (Relative Humidity)

    Suhu yang dirasakan (Apparent Temperature)

    Tekanan Udara (Surface Pressure)

    Tutupan Awan (Cloud Cover)

    Kecepatan Angin (Wind Speed)

Target (Yang ingin ditebak): 
Kolom rain_next_6h, yang bernilai 0 (Tidak Hujan) atau 1 (Hujan).

Pembersihan Data (Data Cleaning): 
Saya memastikan tidak ada data yang kosong/bolong (NaN). 
Jika ada baris yang datanya hilang, kita membuangnya agar model tidak kebingungan.

Standarisasi (Scaling): 
Karena satuan setiap fitur berbeda (contoh: kecepatan angin angkanya kecil, 
sedangkan tekanan udara angkanya besar sampai ratusan), 
saya mengecilkan skalanya menggunakan rumus Z-score Normalization agar semuanya seimbang dan adil saat dinilai oleh model.

C. Pembuatan Model
Algoritma: 
Custom Logistic Regression. Ini adalah algoritma matematika 
yang mencari garis batas terbaik untuk memisahkan kondisi "Hujan" dan "Tidak Hujan".

Proses Belajar (Training):

    Model diberikan ribuan data historis cuaca beserta jawabannya (apakah saat itu hujan atau tidak).

    Model menggunakan fungsi Sigmoid untuk mengubah angka bebas menjadi persentase peluang (0% hingga 100%).

    Dengan metode Gradient Descent, model akan terus-menerus mencoba menebak, menghitung seberapa besar kesalahannya (error), 
    lalu mengoreksi bobot/nilai kepentingannya sendiri berulang-ulang (sebanyak 1000 iterasi/putaran) sampai tebakannya menjadi sangat akurat.

- Proses Ujian (Testing): 
Setelah model "pintar", ia dites menggunakan sekumpulan data baru (test.csv) 
yang belum pernah ia lihat sebelumnya untuk membuktikan kehebatannya.

D. Hasil Dan Evaluasi
Akurasi: Berapa persentase model menjawab dengan benar? (Misalnya: 85%).

Confusion Matrix (Rincian Tebakan):

    Berapa kali model menebak hujan dan memang benar hujan (True Positive)?

    Berapa kali model menebak cerah dan memang benar cerah (True Negative)?

    Berapa kali model memberi Alarm Palsu (menebak hujan, padahal cerah - False Positive)?

    Berapa kali model Kecolongan (menebak cerah, padahal hujan turun - False Negative)?

Analisis Lanjutan:

    Precision: Jika model bilang "Nanti Hujan", seberapa yakin bahwa itu benar-benar terjadi?

    Recall: Dari seluruh kejadian hujan asli, seberapa banyak yang berhasil ditangkap oleh radar model?

E. Kesimpulan Visual
Grafik Distribusi Target (Bar Chart): 
Menggambarkan proporsi data. Apakah di masa lalu lebih sering hujan atau tidak hujan? 
Ini membantu kita mengetahui apakah model cenderung menebak satu arah (bias) atau tidak.

Matriks Korelasi (Peta Panas / Heatmap): 
Ini adalah jantung dari analisis. Lihat pada baris/kolom target (rain_next_6h).

    Warna Merah Pekat (Korelasi Positif) menunjukkan faktor yang paling kuat mendatangkan hujan. 
    Biasanya, Kelembapan (Humidity) dan Tutupan Awan (Cloud Cover) memiliki nilai positif tinggi. 
    Artinya, semakin tinggi kelembapan, semakin besar peluang hujan.

    Warna Biru Pekat (Korelasi Negatif) menunjukkan faktor penahan hujan. 
    Misalnya, semakin tinggi suhu (Temperature) atau tekanan udara, biasanya peluang hujan justru menurun.

- Ringkasan -
Proyek ini adalah sistem Machine Learning pemrediksi hujan yang dibangun murni dari awal tanpa menggunakan library instan. 
Sistem ini belajar dari 6 variabel cuaca historis, menyamakan skala datanya, lalu mencari pola matematis menggunakan regresi logistik. 
Hasilnya, model ini tidak hanya bisa menebak apakah akan hujan atau tidak, 
tapi juga bisa menunjukkan lewat visualisasi bahwa kelembapan dan awan adalah penyebab utama hujan.