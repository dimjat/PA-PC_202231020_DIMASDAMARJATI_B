
#### Nama    : Dimas Damarjati
#### NIM     : 202231020
#### Kelas   : B

#   UAS Pengolahan Citra Digital

Ini adalah bentuk readme dari proyek uas saya.
## Pendahuluan

## Latar Belakang:
   Telah dilakukannya berbagai praktikum pelajaran pengolahan citra yang mengajarkan berbagai metode pemrosesan citra digital. Termasuk metode yang saya kerjakan hari ini yaitu Deteksi Tepi Pola Objek yang mengandung didalamnya Canny Edge Detection serta Contours. Deteksi tepi adalah operasi yang banyak digunakan dalam pemrosesan gambar dan memainkan peran yang sangat penting dalam mengidentifikasi dan memisahkan bentuk geometris dalam gambar. Tepinya selalu berisi informasi penting dari gambar dimana objek dalam gambar dipisahkan oleh tepi gambar. Dengan demikian dapat dikatakan bahwa salah satu langkah paling signifikan dalam penglihatan sebuah mesin adalah pendeteksan tepi.

## Tujuan:
Membuat program untuk deteksi tepi pola objek pada sebuah gambar menggunakan teknik pengolahan citra digital dengan ketentuan sebagai berikut:

Ketentuan khusus gambar :
- Gambar merupakan bentuk foto diri
- Gambar diambil dari jarak minimal 2 meter dari objek (diri sendiri)
 
Ketentuan khusus Code :
- Output gambar harus menampil kan : 
    1. Original Image 
    2. Canny Edge Detection
    3. Contours Detection
## Teori Pendukung

Pengolahan citra digital adalah teknik untuk memanipulasi gambar melalui algoritma komputer. Dalam proyek ini saya menampilkan dua metode untuk mendeteksi tepi pola objek.

1. Deteksi Tepi Canny Edge: Merupakan metode pengolahan citra yang dapat mendeteksi tepi yang jelas dan mengurangi noise. Meskipun algoritma deteksi tepi Canny menunjukkan presisi tinggi, secara komputasi ia lebih kompleks dibandingkan dengan metode deteksi tepi lainnya. Ini dikarenakan algoritma Canny tradisional menggunakan filter Gaussian, yang memberikan detail tepi yang mewakili buram dan juga efeknya dalam menyaring noise kurang baik.

2. Deteksi Kontur (Contour Detection): Kontur adalah kurva yang menghubungkan semua titik yang memiliki intensitas yang sama. Dalam OpenCV, deteksi kontur dilakukan pada hasil dari gambar biner (gambar yang dihasilkan dari deteksi tepi Canny). 
## Pembahasan

### Program

import cv2
import numpy as np
import matplotlib.pyplot as plt

#### Muat gambar
img_path = 'PCDB_UAS_202231020.jpg'
img = cv2.imread(img_path)

#### Ubah gambar jadi grayscale
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

#### Terapkan deteksi tepi Canny
edges = cv2.Canny(gray, 100, 200)

#### Temukan kontur
contours, _ = cv2.findContours(edges, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

#### Salin gambar asli untuk kontur
img_contours = img.copy()
cv2.drawContours(img_contours, contours, -1, (0, 255, 0), 2)

### -> output 1 
fig, axs = plt.subplots(1, 2, figsize=(20, 10))

#### Tampilkan gambar asli
axs[0].imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
axs[0].set_title('Gambar Asli')
axs[0].axis('off')

#### Tampilkan hasil deteksi tepi Canny
axs[1].imshow(edges, cmap='gray')
axs[1].set_title('Deteksi Tepi Canny')
axs[1].axis('off')
plt.show()

### ->output 2
fig, axs = plt.subplots(1, 3, figsize=(20, 10))

#### Tampilkan gambar asli
axs[0].imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
axs[0].set_title('Gambar Asli')
axs[0].axis('off')

#### Tampilkan hasil deteksi tepi Canny
axs[1].imshow(edges, cmap='gray')
axs[1].set_title('Deteksi Tepi Canny')
axs[1].axis('off')

#### Tampilkan gambar dengan kontur terdeteksi
axs[2].imshow(cv2.cvtColor(img_contours, cv2.COLOR_BGR2RGB))
axs[2].set_title('Deteksi Kontur')
axs[2].axis('off')
plt.show()


## Penjelasan tahapan projek secara rinci:

1. Memuat gambar:
- Memuat library-library yang diperlukan seperti OpenCV untuk pengolahan citra, NumPy untuk representasi dan manipulasi gambar, serta matplotlib untuk memvisualisasikan hasilnya. Setelah itu gambar dimuat menggunakan 'cv2.imread()' dari library OpenCV mengikuti path file gambar tersebut yaitu 'PCDB_UAS_202231020.jpg'.

2. Mengubah gambar menjadi grayscale:
- Gambar yang barusan dimuat tadi diubah ke grayscale menggunakan 'cv2.cvtColor()' untuk memudahkan pendeteksian tepinya.

3. Menggunakan deteksi tepi canny edge:
- 'cv2.Canny()' dipakai untuk menggunakan deteksi canny edge pada gambar grayscale. Parameter yang digunakan disini adalah 100 dan 200 sebagai threshold rendah dan tinggi.

4. Menemukan Contours
- 'cv2.findContours()' digunakan untuk menemukan kontur pada gambar hasil dari canny edge sebelumnya lalu digambarkan ulang konturnya pada salinan gambar asli pakai 'cv2.drawContours()'. Hasilnya akan  menampilkan sebuah Array representasi data gambar yang menyimpan semua informasi warna yang dibutuhkan untuk merekonstruksi gambar aslinya. Masing-masing elemen dalam array tiga dimensi itu mewakili nilai warna pada setiap piksel gambar dalam format BGR (Blue, Green, Red).

- Dimensi pertama (baris) mewakili tinggi gambar (jumlah piksel vertikal).

- Dimensi kedua (kolom) mewakili lebar gambar (jumlah piksel horizontal).

- Dimensi ketiga (nilai warna) mewakili saluran warna BGR (nilai intensitas biru, hijau, dan merah) dari setiap piksel.

- Setiap elemen dalam array ini adalah array kecil yang berisi tiga nilai, yaitu intensitas warna biru, hijau, dan merah dari setiap piksel. Misalnya array ([203, 190, 182]) berarti nilai intensitas biru adalah 203, hijau adalah 190, dan merah adalah 182 untuk piksel tersebut.

- dtype=uint8 adalah format umum untuk menyimpan gambar dalam komputer.

5. Menampilkan Outputnya:
- Dalam output 1, dibuat dua subplot yang disusun dalam satu baris (1, 2) dengan ukuran keseluruhan 20x10 inci. Menggunakan 'settitle' untuk memberikan judulu kepada subplot. Subplot 1 menampilkan gambar asli dan subplot 2 menampilkan gambar deteksi canny edge. Sedangkan dalam output 2, dibuat 3 subplot dengan ukuran yang sama yaitu 10x20 inci. Lalu menampilkan gambar asli di subplot 1, gambar canny edge di subplot 2, serta hasil gambar contour dari canny edge pada subplot 3.

## Jurnal Referensi

- Ehsan Akbari Sekehravani, Eduard Babulak, Mehdi Masoodi, Implementing canny edge detection algorithm for noisy image, Vol. 9, No. 4, August 2020.


## Kesimpulan

- Kesimpulan yang dapat diambil yaitu pendeteksian pola tepi objek dapat dilakukan dengan pengolahan citra digital dengan menggunakan library NumPy, OpenCV dan Matplotlib dalam Python. Didalamnya ada langkah-langkah penting yang mencakup pemuatan gambar, pengkonversian ke grayscale, penerapan deteksi tepi Canny, dan pendeteksian contours dari gambarnya. Implementasinya pada proyek ini menunjukkan bahwa metode-metode tersebut dapat digunakan untuk meng-extract, menyalin, serta menampilkan informasi penting dari sebuah gambar digital. 