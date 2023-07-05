
# PROJECT UAS PENGOLAHAN CITRA A

Perkenalkan saya Fathur Aulia Rezky (202131168). Pada project ini saya mendapatkan judul tugas yaitu DETEKSI MARKA JALAN. 

Sebelum ke program, terlebih dahulu saya akan menjelaskan apa itu deteksi marka jalan. 

## Deteksi Marka Jalan
Deteksi marka jalan adalah proses identifikasi dan pelacakan garis atau marka yang terdapat pada permukaan jalan. Marka jalan adalah tanda atau garis yang digambar pada jalan untuk memberikan petunjuk kepada pengendara mengenai jalur yang harus diikuti, pembatasan kecepatan, persimpangan, dan aturan lalu lintas lainnya. Deteksi marka jalan dapat dilakukan dengan menggunakan teknologi komputer vision, di mana gambar atau video jalan diambil dan dianalisis untuk mendeteksi posisi dan bentuk marka jalan.

Deteksi marka jalan merupakan komponen penting dalam sistem pengenalan lalu lintas yang cerdas dan otomatis. Dengan mengenali marka jalan, kendaraan otonom atau sistem bantuan pengemudi dapat memahami dan mengikuti aturan lalu lintas serta menjaga keamanan dalam berlalu lintas. Selain itu, deteksi marka jalan juga dapat digunakan untuk memantau dan mengukur kepadatan lalu lintas, memperingatkan pengemudi jika keluar jalur, dan memberikan informasi visual kepada pengemudi tentang kondisi jalan yang berubah.

Metode deteksi marka jalan dapat bervariasi, termasuk penggunaan pengolahan citra dan algoritma pengenalan pola. Teknologi yang digunakan dapat mencakup penggunaan kamera, lidar, atau sensor lainnya. Tujuan utamanya adalah untuk mengidentifikasi marka jalan dengan akurasi tinggi dan memberikan informasi yang berguna kepada pengemudi atau sistem kendaraan.

## Penjelasan Program

1. Mengimpor library yang diperlukan: cv2, numpy, dan matplotlib.

import cv2
import numpy as np
import matplotlib.pyplot as plt

2. Membaca gambar "parkiran.jpeg" menggunakan fungsi cv2.imread().

image = cv2.imread('parkiran.jpeg')

3. Mengkonversi gambar ke dalam mode warna RGB menggunakan fungsi cv2.cvtColor().

image_asli = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

4. Melakukan pengaburan (blurring) pada gambar menggunakan GaussianBlur untuk mengurangi noise atau detail yang tidak relevan dalam deteksi marka jalan.

blurred_frame = cv2.GaussianBlur(image, (5, 5), 0)

5. Mengkonversi gambar ke dalam mode warna HSV menggunakan fungsi cv2.cvtColor().

hsv = cv2.cvtColor(blurred_frame, cv2.COLOR_BGR2HSV)

6. Menentukan rentang warna putih yang akan di-deteksi pada gambar menggunakan lower_white dan upper_white.

lower_white = np.array([0, 0, 200], dtype=np.uint8)
upper_white = np.array([255, 30, 255], dtype=np.uint8)

7. Menerapkan mask pada gambar HSV menggunakan fungsi cv2.inRange() untuk mendapatkan area yang hanya berisi warna putih.

mask = cv2.inRange(hsv, lower_white, upper_white)

8. Menggunakan deteksi tepi (edge detection) pada mask menggunakan fungsi cv2.Canny() dengan parameter threshold 50 dan 100.

edges = cv2.Canny(mask, 50, 100)

9. Menggunakan transformasi Hough pada tepi gambar menggunakan fungsi cv2.HoughLinesP() untuk mendeteksi garis-garis yang mungkin merupakan marka jalan.

lines = cv2.HoughLinesP(edges, 1, np.pi / 180, 50, maxLineGap=50)

10. Jika terdapat garis yang terdeteksi, maka program akan menggambar garis-garis tersebut pada gambar asli menggunakan cv2.line().

if lines is not None:
    for line in lines:
        x1, y1, x2, y2 = line[0]
        cv2.line(image, (x1, y1), (x2, y2), (0, 255, 0), 75)

11. Mengkonversi gambar hasil deteksi marka jalan ke dalam mode warna RGB menggunakan fungsi cv2.cvtColor().

image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

12. Menampilkan gambar asli dan gambar dengan marka jalan yang telah terdeteksi dalam bentuk subplot menggunakan matplotlib.

fig, ax = plt.subplots(1, 2, figsize=(12, 6))
ax[0].imshow(image_asli)
ax[0].set_title('Gambar Asli')

ax[1].imshow(image_rgb)
ax[1].set_title('Deteksi Marka Jalan')

plt.show()

Dengan menjalankan program di atas, Anda akan melihat gambar asli dan gambar dengan marka jalan yang telah terdeteksi. Gambar dengan marka jalan yang terdeteksi ditampilkan dengan garis-garis berwarna hijau yang menunjukkan posisi marka jalan.

## Sumber 
https://youtu.be/F5_ZJLRICtw

sekian penjelasan saya tentang Project UAS Pengolahan Citra-A  yaitu Deteksi marka Jalan








