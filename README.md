# UTS PCD C

## 1. Menganalisis citra 
Citra 'uts.jpg' memiliki distribusi warna   yang cukup   merata di seluruh saluran warna, ditunjukkan oleh histogram yang memiliki distribusi yang relatif merata.
 - Histogram merah menunjukkan bahwa intensitas piksel merah paling banyak terkonsentrasi di sekitar nilai 100-150. 
 - Histogram hijau menunjukkan intensitas piksel hijau yang cukup merata dengan sedikit puncak di sekitar nilai 100.
 - Histogram biru menunjukkan intensitas piksel biru yang juga merata dengan sedikit puncak di sekitar nilai 100.
 - Histogram warna gabungan menunjukkan kombinasi intensitas piksel dari semua saluran warna, dengan distribusi yang merata namun dengan beberapa puncak yang menunjukkan kemungkinan warna dominan dalam gambar.

Adapun beberapa proses analisis citra yang dilakukan
    
a. Pemisahan Saluran Warna,  itra asli dibagi menjadi saluran warna merah, hijau, dan biru menggunakan slicing array numpy. Ini memungkinkan kita untuk melihat kontribusi setiap saluran warna terhadap citra secara terpisah.

b. Visualisasi Histogram, histogram digunakan untuk menunjukkan distribusi intensitas piksel dalam citra. Histogram dihitung untuk setiap saluran warna (merah, hijau, biru) serta histogram gabungan dari seluruh citra. Ini membantu dalam memahami bagaimana intensitas piksel didistribusikan di seluruh saluran warna.

c. Konversi Warna, karena OpenCV membaca gambar dalam format BGR, sedangkan matplotlib menampilkan dalam format RGB, ada konversi warna yang dilakukan menggunakan `cv2.cvtColor()`. Ini penting agar citra ditampilkan dengan benar.

d. Visualisasi, subplot digunakan untuk menampilkan citra asli dan saluran warna terpisah, serta subplot terpisah untuk setiap histogram. Ini membantu dalam membandingkan distribusi intensitas piksel antara saluran warna dan melihat hubungan antara mereka.

Dengan demikian, proses analisis citra tersebut terfokus pada pemahaman tentang bagaimana distribusi intensitas piksel berbeda di setiap saluran warna, serta bagaimana distribusi keseluruhan warna dalam citra. Ini memberikan pemahaman yang lebih mendalam tentang komposisi warna dan informasi visual dalam citra.

## 2. Menganalisis Histogram

A. Histogram Merah, Hijau, dan Biru menghitung histogram untuk setiap saluran warna merah, hijau, dan biru menggunakan `cv2.calcHist()`. Histogram-histogram ini menunjukkan distribusi intensitas piksel dalam masing-masing saluran warna. Dari histogram-histogram ini, dapat dilihat seberapa banyak piksel dengan intensitas tertentu yang ada dalam gambar. Misalnya, jika terdapat puncak pada nilai intensitas tertentu dalam histogram merah, ini menunjukkan bahwa ada banyak piksel dengan intensitas merah yang sama dalam gambar. 

B. Histogram Warna Gabungan juga menghitung histogram untuk warna gabungan menggunakan ketiga saluran warna (merah, hijau, biru) dari gambar yang sudah dikonversi ke format RGB. Histogram warna gabungan ini menunjukkan distribusi kombinasi intensitas piksel dari semua saluran warna. Dari histogram ini, kita dapat melihat distribusi intensitas piksel secara keseluruhan dalam gambar. Histogram warna gabungan ini memberikan gambaran tentang bagaimana intensitas piksel tersebar di seluruh warna dalam gambar.

Dengan menganalisis histogram-histogram ini, dapat diperoleh pemahaman yang lebih dalam tentang karakteristik warna dalam gambar 'uts.jpg'. Kita bisa melihat seberapa merata distribusi warna dalam gambar, apakah ada warna tertentu yang dominan, dan seberapa besar variasi warna dalam gambar. Informasi ini penting dalam banyak aplikasi pengolahan citra, seperti segmentasi warna, deteksi objek, atau penyesuaian warna.

## 3. Nilai ambang batas yang didapat 
Setiap fungsi menggunakan konversi ruang warna HSV untuk memudahkan dalam mendeteksi warna tertentu, karena HSV memisahkan informasi warna (Hue), kecerahan (Value), dan saturasi (Saturation).

A. Deteksi Warna Biru 
- Nilai ambang batas bawah [100, 50, 50]
- Nilai ambang batas atas [130, 255, 255]

B. Deteksi Warna Merah
- Nilai ambang batas bawah: [0, 50, 50]
- Nilai ambang batas atas: [10, 255, 255]
- (Merah melintasi nilai nol dalam skala Hue)
- Nilai ambang batas bawah tambahan: [170, 50, 50]
- Nilai ambang batas atas tambahan: [180, 255, 255]

C. Deteksi Warna Hijau
- Nilai ambang batas bawah: [40, 50, 50]
- Nilai ambang batas atas: [80, 255, 255]

Nilai-nilai ini dipilih dengan mempertimbangkan sifat warna dalam ruang warna HSV dan tujuan deteksi warna yang dilakukan. Alasan di balik pemilihan nili-nilai amban batas ini adalah :
- Hue (H), Nilai Hue dalam rentang 0-180 (dalam OpenCV), yang merepresentasikan warna dalam lingkup 360 derajat. Dalam pemilihan nilai ambang batas, diperhatikan bahwa warna merah memiliki nilai Hue mendekati 0 (atau mendekati 180 karena warna melintasi nilai 0 dalam lingkup warna), warna hijau berada di sekitar 60-120, dan warna biru berada di sekitar 100-150. Nilai-nilai ambang batas ini dipilih untuk mencakup rentang Hue yang mewakili warna yang diinginkan.
- Saturation (S) dan Value (V), Nilai ambang batas untuk S dan V dipilih untuk menentukan seberapa jenuh dan seberapa cerah warna yang ingin dideteksi. Rentang yang luas digunakan untuk memungkinkan deteksi warna yang cukup fleksibel terhadap variasi dalam gambar.
Pemilihan nilai ambang batas ini mungkin berbeda tergantung pada kondisi cahaya, sifat gambar, dan prefensi pengguna.

## 4. Penjelasan tahapan cara menyelesaikan projek
 #### A. Tahapan Cara Deteksi warna biru, merah dan hijau pada gambar

Tahap 1: Membaca Gambar dan Membuat Plot

- Membaca Gambar, gambar yang disimpan dengan nama 'uts.jpg' dibaca menggunakan fungsi `imread` dari library OpenCV dan disimpan dalam variabel `color_image`.
- Membuat Plot, plot untuk gambar asli, warna merah, hijau, dan biru dibuat menggunakan fungsi `subplots` dan `imshow` dari matplotlib. Plot ini menampilkan gambar asli dan warna-warna yang terdiri dari gambar.

Tahap 2: Membuat Histogram

- Membuat Histogram, histogram untuk warna merah, hijau, dan biru dibuat menggunakan fungsi `calcHist` dari OpenCV. Histogram ini menunjukkan distribusi intensitas warna dalam gambar.

Tahap 3: Membuat Fungsi untuk Meningkatkan Brightness dan Mendeteksi Warna

- Meningkatkan Brightness, fungsi `increase_brightness` dibuat untuk meningkatkan brightness dari gambar. Fungsi ini menggunakan konversi warna dari BGR ke HSV, lalu meningkatkan nilai brightness dan mengembalikan ke BGR.
- Mendeteksi Warna, fungsi `detect_and_highlight_blue`, `detect_and_highlight_red_blue`, dan `detect_and_highlight_red_green_blue` dibuat untuk mendeteksi warna biru, merah-biru, dan merah-hijau-biru secara terpisah. Fungsi-fungsi ini menggunakan konversi warna dari BGR ke HSV, lalu menggunakan mask untuk mendeteksi warna dan mengembalikan gambar yang telah ditekan warna.

Tahap 4: Menerapkan Fungsi untuk Meningkatkan Brightness dan Mendeteksi Warna

- Meningkatkan Brightness, fungsi `increase_brightness` diterapkan pada gambar yang dibaca awal untuk meningkatkan brightness.
-  Mendeteksi Warna, fungsi `detect_and_highlight_blue`, `detect_and_highlight_red_blue`, dan `detect_and_highlight_red_green_blue` diterapkan pada gambar yang telah ditingkatkan brightness untuk mendeteksi warna.

Tahap 5: Menampilkan Hasil

- Menampilkan Hasil, hasil dari masing-masing fungsi diterapkan pada gambar ditampilkan menggunakan fungsi `imshow` dari matplotlib. Hasil ini menampilkan gambar yang telah ditingkatkan brightness dan ditekan warna.

#### B. Tahapan Cara Membuat dan Menampilkan Plot Histogram

Tahap 1: Membaca Gambar dan Konversi Warna

- Membaca Gambar, gambar yang disimpan dengan nama 'uts.jpg' dibaca menggunakan fungsi `imread` dari OpenCV dan disimpan dalam variabel `color_image`.
- Konversi Warna, Konversi warna dari BGR ke RGB dilakukan menggunakan fungsi `cvtColor` dari OpenCV. Fungsi ini digunakan untuk memastikan bahwa warna dalam gambar sesuai dengan format yang digunakan oleh matplotlib.

Tahap 2: Membuat Histogram

- Membuat Histogram Biru, histogram untuk warna biru dibuat menggunakan fungsi `calcHist` dari OpenCV. Histogram ini menunjukkan distribusi intensitas warna biru dalam gambar.
- Membuat Histogram Hijau, histogram untuk warna hijau dibuat menggunakan fungsi `calcHist` dari OpenCV. Histogram ini menunjukkan distribusi intensitas warna hijau dalam gambar.
- Membuat Histogram Merah, histogram untuk warna merah dibuat menggunakan fungsi `calcHist` dari OpenCV. Histogram ini menunjukkan distribusi intensitas warna merah dalam gambar.
- Membuat Histogram Warna, histogram untuk warna-warna dalam gambar dibuat menggunakan fungsi `calcHist` dari OpenCV. Histogram ini menunjukkan distribusi intensitas warna-warna dalam gambar.

Tahap 3: Membuat Plot Histogram

- Membuat Plot Histogram Biru, plot histogram biru dibuat menggunakan fungsi `plot` dari matplotlib. Plot ini menampilkan histogram biru dengan warna biru.
- Membuat Plot Histogram Hijau, plot histogram hijau dibuat menggunakan fungsi `plot` dari matplotlib. Plot ini menampilkan histogram hijau dengan warna hijau.
- Membuat Plot Histogram Merah, plot histogram merah dibuat menggunakan fungsi `plot` dari matplotlib. Plot ini menampilkan histogram merah dengan warna merah.
- Membuat Plot Histogram Warna, plot histogram warna dibuat menggunakan fungsi `plot` dari matplotlib. Plot ini menampilkan histogram warna dengan warna abu-abu.

Tahap 4: Menampilkan Plot Histogram

- Menampilkan Plot Histogram, plot histogram untuk warna biru, hijau, merah, dan warna dibuat dan ditampilkan menggunakan fungsi `figure` dan `subplot` dari matplotlib. Plot ini menampilkan histogram untuk masing-masing warna dan warna dalam gambar.

#### C. Tahapan Cara Mencari Nilai Ambang atas yang Didapat 

Tahap 1: Membuat Fungsi untuk Meningkatkan Brightness dan Mendeteksi Warna
- Meningkatkan Brightness, fungsi `increase_brightness` dibuat untuk meningkatkan brightness dari gambar. Fungsi ini menggunakan konversi warna dari BGR ke HSV, lalu meningkatkan nilai brightness dan mengembalikan ke BGR.
- Mendeteksi Warna, fungsi `detect_and_highlight_blue`, `detect_and_highlight_red_blue`, dan `detect_and_highlight_red_green_blue` dibuat untuk mendeteksi warna biru, merah-biru, dan merah-hijau-biru secara terpisah. Fungsi-fungsi ini menggunakan konversi warna dari BGR ke HSV, lalu menggunakan mask untuk mendeteksi warna dan mengembalikan gambar yang telah ditekan warna.

Tahap 2: Membaca Gambar dan Meningkatkan Brightness
- Membaca Gambar, gambar yang disimpan dengan nama 'uts.jpg' dibaca menggunakan fungsi `imread` dari OpenCV dan disimpan dalam variabel `image`.
- Meningkatkan Brightness, fungsi `increase_brightness` diterapkan pada gambar yang dibaca untuk meningkatkan brightness.

Tahap 3: Mendeteksi Warna
- Mendeteksi Warna Biru, fungsi `detect_and_highlight_blue` diterapkan pada gambar yang telah ditingkatkan brightness untuk mendeteksi warna biru.
- Mendeteksi Warna Merah-Biru, fungsi `detect_and_highlight_red_blue` diterapkan pada gambar yang telah ditingkatkan brightness untuk mendeteksi warna merah-biru.
- Mendeteksi Warna Merah-Hijau-Biru, fungsi `detect_and_highlight_red_green_blue` diterapkan pada gambar yang telah ditingkatkan brightness untuk mendeteksi warna merah-hijau-biru.

Tahap 4: Menampilkan Hasil
- Menampilkan Hasil, hasil dari masing-masing fungsi diterapkan pada gambar ditampilkan menggunakan fungsi `imshow` dari matplotlib. Hasil ini menampilkan gambar yang telah ditingkatkan brightness dan ditekan warna.

## 5. Teori yang mendukung mengenai projek
Teori yang Mendukung Proyek
1. Color Space Conversion, menggunakan konversi warna dari warna RGB ke HSV (Hue, Saturation, Value) untuk mendeteksi warna. Konversi warna ini didasarkan pada teori bahwa warna dalam RGB memiliki nilai yang berbeda untuk masing-masing warna, sedangkan dalam HSV, warna didefinisikan oleh nilai hue yang menentukan warna, nilai saturation yang menentukan keintensifan warna, dan nilai value yang menentukan kecerahan warna. Dengan menggunakan HSV, deteksi warna menjadi lebih mudah dan akurat karena nilai hue dapat digunakan untuk membedakan warna yang berbeda.

2. Histogram, menggunakan histogram untuk menganalisis distribusi nilai warna dalam gambar. Histogram didasarkan pada teori bahwa histogram adalah grafik yang menampilkan frekuensi nilai dalam suatu distribusi statistik. Dalam konteks warna, histogram digunakan untuk menganalisis bagaimana nilai warna dalam gambar dibagi. Dengan menggunakan histogram, dapat diperoleh informasi tentang bagaimana warna dalam gambar dibagi dan bagaimana warna tersebut dapat digunakan untuk deteksi warna.

3. Image Processing, menggunakan berbagai teknik pengolahan gambar seperti peningkatan kecerahan, deteksi warna, dan penggabungan masker. Teknik-teknik ini didasarkan pada teori bahwa pengolahan gambar dapat dilakukan dengan menggunakan algoritma yang spesifik untuk masing-masing tugas. Contohnya, peningkatan kecerahan dapat dilakukan dengan menambahkan nilai kecerahan dalam HSV, sedangkan deteksi warna dapat dilakukan dengan menggunakan masker warna yang sesuai.

4. Color Detection, menggunakan masker warna untuk mendeteksi warna dalam gambar. Masker warna didasarkan pada teori bahwa warna dalam gambar dapat didefinisikan oleh nilai warna yang spesifik. Dengan menggunakan masker warna, dapat diperoleh gambar yang hanya menampilkan warna yang spesifik, sehingga memudahkan deteksi warna.

5. Image Segmentation, menggunakan penggabungan masker warna untuk mengsegmentasi gambar. Penggabungan masker warna didasarkan pada teori bahwa gambar dapat dipecah menjadi bagian-bagian yang berbeda berdasarkan warna. Dengan menggunakan penggabungan masker warna, dapat diperoleh gambar yang tersegmentasi secara efektif, sehingga memudahkan analisis warna.

Dalam sintesis, proyek ini menggunakan berbagai teori dan teknik pengolahan gambar untuk mendeteksi warna dan mengolah gambar. Teknik-teknik ini didasarkan pada teori bahwa pengolahan gambar dapat dilakukan dengan menggunakan algoritma yang spesifik untuk masing-masing tugas, dan bahwa warna dalam gambar dapat didefinisikan oleh nilai warna yang spesifik. Dengan menggunakan berbagai teori dan teknik ini, proyek ini dapat menghasilkan gambar yang terolah secara efektif dan memudahkan analisis warna.







   
