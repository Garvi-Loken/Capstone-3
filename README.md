Capstone-3 Capstone 3 Purwadhika - Bimayu Satriyo Gusmana
# PENDAHULUAN

**Problem Statement**

Keuntungan sebuah bisnis pada bidang perhotelan sangat bergantung kepada banyaknya kamar yang dipesan. Pada saat ini kemudahan pemesanan kamar dapat dilakukan dalam berbagai bentuk, seperti langsung datang ke hotel individu maupun agen, pemesanan lewat web hotel, pemesanan lewat paliaksi pihak ketiga. Namun kemudahan itu juga yang menjadi masalah baru yaitu masalah kemudahan dalam pembatalan pemesanan kamar. Dengan itu prediksi untuk mengetahui pembatalan pemesanan sangat membantu bisnis perhotelan. Tapi dengan prediksi tersebut juga dapat menimbulkan overbooking.

**Tujuan**

Tujuan dibuatnya model Machine Learning ini adalah untuk mengetahui atau mendeteksi pola pemesanan kamar apakah akan terjadi pembatalan pemesanan kamar. Dengan itu pemilik bisnis perhotelan bisa melihat probabilitas kamar yang batal dipesan dan juga bisa mengetahui strategi untuk membantu jika terjadinya overbooking.

**Pendekatan Analitik**

Untuk mencapai tujuan dari machine learning ini maka model yang digunakan adalah model klasifikasi karena tujuannya adalah mengetahui apakah pembatalan terjadi (ya/tidak).

**Evaluasi Metiks**

Dalam hal ini kelas positifnya adalah 1 atau batal
kelas negatifnya adalah 0 atau tidak batal

Probabilitas konsekuensi yang terjadi dari model prediksi adalah :
1. False Negative : Model memprediksi tamu tidak akan membatalkan pesanan namun ternyata membatalkan pesanan. Hal ini dapat merugikan pemilik hotel. 
2. False Positive : Model memprediksi tamu akan membatalkan pesanan namun ternyata tidak membatalkan pesanan. Hal ini dapat membuat overbooking.

Dari konsekuensi di atas maka metriks utama yang akan dipakai adalah F2 score.

# DATA UNDERSTANDING

Features
-	country: Country of origin.
-	market_segment: Market segment designation. 
-	previous_cancellations: Number of previous bookings that were cancelled by the customer prior to the current booking.
-	booking_changes: Number of changes/amendments made to the booking from the moment the booking was entered on the PMS until the moment of check-in or cancellation.
-	deposit_type: Indication on if the customer made a deposit to guarantee the booking. 
-	days_in_waiting_list: Number of days the booking was in the waiting list before it was confirmed to the customer.
-	customer_type: Type of booking.
-	reserved_room_type: Code of room type reserved. Code is presented instead of designation for anonymity reasons.
-	required_car_parking_space: Number of car parking spaces required by the customer.
-	total_of_special_request: Number of special requests made by the customer (e.g. twin bed or high floor).
-	is_canceled: Value indicating if the booking was canceled (1) or not (0).

![image](https://github.com/user-attachments/assets/32e29b7c-ecfd-453a-aebc-dfcf8d1dc56d)

Data memiliki 11 kolom dengan 83573 baris
2. Tipe data berupa int dan object. 5 kolom object (country, market_segment, deposit_type, customer_type, reserved_room_type) dan 6 kolom int (previous_cancellations, booking_changes, days_in_waiting_list, required_car_parking_spaces, total_of_special_requests, is_canceled)
3. Data yang missing value sebanyak 351 pada kolom country saja. Dari keseluruhan data hanya 0,41% saja.
4. Kelas dari kolom target tidak seimbang dengan kelas negatif sebanyak 63% dan kelas positif sebanyak 36%
5. Pada kolom country banyak number of uniqenya sebanyak 162 dengan didominasi oleh PRT sebanyak 40%

# DATA CLEANING

Pada kolom country isi uniqenya sangat banyak, sebanyak 163. Dengan persentasi tertinggi adalah PRT atau negara portugal dengan 40% dari total unique. Pada data set ini dijelaskan bahwa ini adalah dataset hotel pada negara Portugal jadi akan lebih mudah jika membaginya menjadi 2 uniqe saja.
1. Portugal.
2. Others.

# DATA PREPARATION

Tabel kategorikal dari data di atas ada sebanyak 5 tabel yaitu country, market_segment, deposit_type, customer_type, reserved_room_type.
Maka dari itu encoding diperlukan untuk mengubah tabel kategorikal menjadi angka.
Dari tabel di atas untuk encodingnya menggunakan One Hot Encoding, binary Encoding dan juga Ordinal Encoding.

1. Tabel country akan diencode menggunakan One Hot Encoding karena isinya sudah diubah menjadi 2 unique saja yaitu Portugal dan Other.
2. Tabel market_segment akan diencode menggunakan binary encoding karena uniqenya lebih dari 5, ini dilakukan untuk menghindari overfitting karena terlalu banyak tabel yang dibentuk.
3. Tabel deposit_type, customer_type sama seperti tabel country akan diencode menggunakan One Hot Encoding.
4. Tabel reserved_room_type akan diencode menggunakan Ordinal Encoding karena tipe kamar termasuk nilai yang bertingkat dimulai dari tipe A yang akan diubah ke angka 0 dan bertingkat ke selanjutnya.

# MODELING & EVALUATION

Mendefine model model
logreg = LogisticRegression()
knn = KNeighborsClassifier()
dectree = DecisionTreeClassifier()
randomfor = RandomForestClassifier()
adaboost = AdaBoostClassifier()
svm = SVC()
xgb = XGBClassifier()

![image](https://github.com/user-attachments/assets/f2f702d8-b926-4e36-8063-f1b20937df56)

Dari Cross Validation di atas Random Forest menjadi model terbaik dibandingkan dengan yang lain namun perbedaan dengan Decision tree sangat kecil. Akan tetapi Random Forest menjadi yang tertinggi dari semuanya, untuk itu model yang digunakan selanjutnya adalah random forest.
Random Forest sendiri adalah model machine learning yang bekerja dengan membangun banyak decision tree sebagai sebuah ensemble. Yang bekerja dengan membangun banyak decision tree, lalu menggabungkan hasilnya untuk membuat prediksi yang lebih akurat dan stabil.

![image](https://github.com/user-attachments/assets/d80cfe26-42f6-4810-ba1d-36c6b38cda64)

# KESIMPULAN & REKOMENDASI

**Kesimpulan**

Model ini bisa membantu bisnis perhotelan di portugal untuk mendeteksi resiko pembatalan sebesar 76% (dilihat dari score F2nya), namun bukan untuk keputusan overbooking. Dengan menggabungkan hasil prediksi, komunikasi ke pelanggan, dan sistem buffer internal, pemilik bisnis perhotelan bisa meningkatkan efisiensi tanpa mengorbankan pengalaman tamu.

Pemilik bisnis perhotelan juga dapat mengurangi kerugian dari kamar kosong dengan menyusun strategi overbooking yang aman.
Dengan menerapkan model ini, hotel tidak hanya bisa mengurangi pembatalan, tapi juga mengoptimalkan sumber daya, meningkatkan pendapatan, dan memberikan pengalaman pelanggan yang lebih baik secara proaktif.

**Rekomendasi**

Karena masih ada beberapa tamu yang diprediksi batal padahal tidak, jangan langsung gunakan model ini untuk overbooking otomatis. Tapi gunakan prediksi ini dengan :
1. Mengirim reminder atau konfirmasi kepada tamu.
2. Memberikan insentif agar mereka melanjutkan reservasi (misalnya diskon kecil atau check-in cepat atau memberikan makan sarapan).
3. Melakukan prioritas layanan atau follow-up manual untuk tamu yang berisiko membatalkan pesanan.
4. Untuk mengatasi false negatifnya (yang akan membatalkan namun tidak terprediksi) maka sediakan buffer kamar terbatas atau sistem waiting list untuk mengantisipasi kekosongan mendadak.
5. Jika ingin menerapkan overbooking, batasi hanya pada level yang aman berdasarkan historical rate pembatalan, dan konfirmasi ulang reservasi sebelum mengambil tindakan.
