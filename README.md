# Tugas 1 BigData

## ETL Menggunakan KNIME

### Dataset 
Pada tugas 1 ini dataset yang saya gunakan adalah Dataset Air Quality.
  - Sumber Dataset : https://archive.ics.uci.edu/ml/datasets/Air+quality
  -  Deskripsi singkat :
  
     Dataset berisi tanggapan dari perangkat multisensor gas yang digunakan di lapangan di kota Italia. Rata-rata respons setiap jam dicatat bersama dengan referensi konsentrasi gas dari penganalisa bersertifikat.

### Business Understanding
  Dataset merupakan data _Air Quality_ yang dapat digunakan untuk berbagai macam kebutuhan, misalnya seperti penelitian ataupun pengukuran kelayakan udara yang ada. Proses yang dilakukan pada data pun bisa bermacam-macam. Misalnya, untuk menentukan apakah udara saat ini tingkat kualitas udaranya dapat dibilang layak atau tidak, bisa dengan menghitung rata-rata dari standar kelayakan per kategori konsentrasi materi atribut, dsb.
  
### Data Understanding
  Dataset berisi 9358 baris data contoh respons rata-rata per jam dari berbagai 5 sensor kimia oksida logam yang tertanam dalam Perangkat Multisensor Kimia Kualitas Udara. Perangkat itu terletak di lapangan di area yang sangat tercemar, di permukaan jalan, di dalam kota Italia. 
  
  Data direkam dari Maret 2004 hingga Februari 2005 (satu tahun) mewakili catatan terpanjang yang tersedia secara bebas dari respons perangkat sensor bahan kimia kualitas udara yang digunakan. 
  Terdapat 15 atribut pada dataset dengan jumlah total 9358 baris data.
   - Informasi atribut :
      - Date (DD/MM/YYYY)
      - Time (HH.MM.SS)
      - True hourly averaged concentration CO in mg/m^3 (reference analyzer)
      - PT08.S1 (tin oxide) hourly averaged sensor response (nominally CO targeted)
      - True hourly averaged overall Non Metanic HydroCarbons concentration in microg/m^3 (reference analyzer)
      - True hourly averaged Benzene concentration in microg/m^3 (reference analyzer)
      - PT08.S2 (titania) hourly averaged sensor response (nominally NMHC targeted)
      - True hourly averaged NOx concentration in ppb (reference analyzer)
      - PT08.S3 (tungsten oxide) hourly averaged sensor response (nominally NOx targeted)
      - True hourly averaged NO2 concentration in microg/m^3 (reference analyzer)
      - PT08.S4 (tungsten oxide) hourly averaged sensor response (nominally NO2 targeted)
      - PT08.S5 (indium oxide) hourly averaged sensor response (nominally O3 targeted)
      - Temperature in Â°C
      - Relative Humidity (%)
      - AH Absolute Humidity
### Data Preparation
  Dataset berupa 1 file excel (.xls) yang memiliki 9358 record data dan 15 atribut. Dataset kemudian dibagi menjadi 2 bagian menggunakan fitur partitioning pada aplikasi KNIME. Inputan berupa 1 file excel (.xls) yang kemudian di split menjadi 2 dengan relative 50% secara random:
    - __data 1__, dimana data dimasukkan ke dalam sebuah database dengan jumlah baris data 4678.
    - __data 2__, dimana data berupa file excel dengan jumlah baris data 4679.
    ![Komponen Sistem Operasi](https://github.com/afrchmdi/Tugas1-BigData-ETL-KNIME/blob/master/split-data.png)
### Modeling
Jelaskan proses membaca data dari dua sumber yang berbeda
Jelaskan proses modeling (join atau append) yang dilakukan beserta setting node pada KNIME

  Pada tahap ini dataset telah terbagi menjadi 2 bagian dengan bentuk yang berbeda, __data 1__ berupa database sedangkan __data 2__ berupa file excel (.xls).
  Untuk membaca kedua data yang berbeda ini digunakan fitur database reader dan excel reader pada KNIME untuk membaca masing-masing data.
  
  Proses modelling yang dilakukan adalah append karena dataset awal berupa 1 file yang di split menjadi 2. Setting node pada KNIME :
  1. __Connector MYSQL__ untuk menghubungkan koneksi pada database.
  2. __Database Reader__ untuk membaca database hasil koneksi yang dilakukan sebelumnya (data 1).
  3. __Excel Reader__ untuk membaca file excel (data 2).
  4. __Concatenate__ untuk menggabungkan/meng-append kedua tabel menjadi 1 dimana data 2 di concatenate pada data 1.
  5. __Database Writer__ untuk memasukkan hasil penggabungan ke dalam database yang diinginkan.
  6. __Excel Writer__ untuk memasukkan hasil penggabungan tabel menjadi sebuah file excel (.xls).
  
  ![Komponen Sistem Operasi](https://github.com/afrchmdi/Tugas1-BigData-ETL-KNIME/blob/master/modelling.png)
  
### Evaluation
  Proses pengappend an dataset berhasil dilakukan, output berupa sebuah 1 file excel yang merupakan gabungan dari data 1 dan data 2 yang di split secara random.
  
### Deployment
  OUput hasil dari penggabungan dataset berupa 1 file excel (.xls) dan juga database.
  
