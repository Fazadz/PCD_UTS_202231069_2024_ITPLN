# PCD_UTS_202231069_2024_ITPLN

#### Nama: Faza Dzoukhar Doudayef Umairullah
#### NIM: 202231069

## No 1
Penjelasan Code:
import library
``` bash
import cv2
import matplotlib.pyplot as plt
import numpy as np
``` 

Code di atas merupakan code pembuka untuk mengimport library yang nantinya akan dipakai, adapun rinciannya sebagai berikut:
1. library cv2: Digunakan untuk akses ke berbagai fungsi komputer vision dan pemrosesan gambar dalam python.
2. library matplotlib.pyplot: Digunakan untuk membuat plot tertentu(histogram, diagram, dan plot lainnya). Adapun as plt adalah pengaliasan atau memudahkan coder untuk menulis sintaks terkait dengan hanya mengetik 'plt'
3. library numpy: numpy atau Numemrical Python, digunakan untuk membuat struktural array atau operasi array.

Membaca Data Gambar
``` bash
img = cv2.imread('nama.jpeg')
```

Code 'imread' berfungsi untuk membaca gambar yang telah diinput ke sebuah file dalam program python.

Mengubah citra dari BGR ke RGB:
``` bash
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```
Awalnya, gambar yang ditampilkan berformat BGR(Blue, Green, Red), lalu nantinya akan diubah ke format umum yakni RGB(Red, Green, Blue) agar gambar dapat diproses.
Penjabaran:
1. img: adalah gambar yang ingin dikonversi dari BGR ke RGB
2. cvtColor: command ini digunakan untuk mengonversi ruang warna
3. cv2.COLOR_BGR2RGB: digunakan untuk mengonversi gambar yang berformat BGR (Blue, Green, Red) menjadi RGB (Red, Green, Blue)
   
Menampilkan komponen citra Red, Green, Blue.
``` bash
R, G, B = cv2.split(img)

fig, axs = plt.subplots(1, 4, figsize=(20,20))

#Citra Asli
axs[0].imshow(img)
axs[0].set_title('Citra Asli')

#Red
axs[1].imshow(R, cmap='gray')
axs[1].set_title('Komponen Merah')

#Green
axs[2].imshow(G, cmap='gray')
axs[2].set_title('Komponen Hijau')

#Blue
axs[3].imshow(B, cmap='gray')
axs[3].set_title('Komponen Biru')

for ax in axs:
    ax.axis('off')

plt.show()
```
Setelah dikonversi, langkah selanjutnya ialah memecah komponennya menjadi satuan yakni Red, Green, dan Blue. Untuk memecahnya dapat menggunakan 'cv2.split(img)', setelahnya dibuat representasi array 2d atau matriksnya menggunakan axs dengan batasan 1 baris dan 4 kolom subplot. Pada outputnya muncul 4 gambar yang dikelompokkan sebagai berikut:
1. Gambar 1 menunjukkan gambar citra asli, yang artinya tidak ada perubahan dengan gambar yang diinput di file python
2. Gambar 2 menunjukkan gambar komponen red, yang artinya tinta yang berwana merah atau unsur yang berwarna merah akan terang dan warna lainnya akan redup
3. Gambar 3 menunjukkan komponen green, yang artinya tinta yang berwarna hijau atau unsur yang berwarna hijau akan terang dan warna lainnya akan redup.
Penjabaran:
1. Command 'cv2.split(img)' digunakan untuk memecahkan citra menjadi komponen Red, Green, dan Blue.
2. Command 'fig' digunakan untuk merepresentasikan seluruh figure gambar disebuah python, sedangkan 'axs' merupakan array yang berisi setiap subplot(array 2 dimensi/ matriksnya).
3. fungsi 'imshow(img)' digunakan untuk menampilkan gambar terkait, adapun set_title digunakan untuk menampilkan teks yang disertakan ke output.
4. Loop for ax in axs digunakan untuk membuat plot tanpa menampilkan sumbu-sumbunya.
5. Command plt.show: digunakan untuk menampilkan plot

Membuat Histogram:
``` bash
#membuat Histogram untuk citra asli 
histimg = cv2.calcHist([img],[0],None,[256],[0,256])

#membuat histogram untuk komponen R (merah)
histR = cv2.calcHist([R],[0],None,[256],[0,256])

#membuat histogram untuk komponen G (Hijau)
histG = cv2.calcHist([G],[0],None,[256],[0,256])

#membuat histogram untuk komponen B (biru)
histB = cv2.calcHist([B],[0],None,[256],[0,256])
```
Setelah itu, langkah selanjutnya ialah membuat histogram. Untuk membuat histogram menggunakan 'cv2.calcHist()', histogram dibuat sesuai perkomponen(Citra asli, Red, Green, Blue). Adapun histogram citra asli dibuat dengan paramater gambar asli(sesuai), untuk komponen Red, Green, Blue menggunakan komponen warnanya masing-masing. Outputnya berupa 4 yang mewakili tiap citra(Citra Asli, Red, Green, Blue).


Menampilkan Histogram:
``` bash
fig, axs = plt.subplots(2, 2, figsize=(20, 10))

#Citra Asli
axs[1,1].plot(histimg, color='black')
axs[1,1].set_title('Histogram Gambar Asli')

#Red
axs[0,0].plot(histR, color='red')
axs[0,0].set_title('Histogram Komponen Merah')

#Green
axs[0,1].plot(histG, color='green')
axs[0,1].set_title('Histogram Komponen Hijau')

#Blue
axs[1,0].plot(histB, color='blue')
axs[1,0].set_title('Histogram Komponen Biru')

plt.show()
```
Pada code ini, saya membuat empat subplot dalam satu gambar dengan 2 baris dan 2 kolom. Setiap subplot nantinya menapilkan histogram untuk citra asli dan masing masing komponen warna (Merah, Hijau, dan Biru). Plot histogram citra asli ditampilkan pada subplot kanan bawah, sedangkan histogram untuk komponen R, G, B ditampilkan pada subplot lainnya. setiap subplot diberikan judul sesuai dengan komponen warna yang mewakilinya. 

## No 2
Penjelasan kode:
``` bash
gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)
fig, axs = plt.subplots (2, 2, figsize=(10,10))

(thresh, binary1) = cv2.threshold(gray, 0, 0, cv2.THRESH_BINARY)
axs[0,0].imshow(binary1, cmap = 'gray')
axs[0,0].set_title('NONE')

(thresh, binary2) = cv2.threshold(gray, 20, 255, cv2.THRESH_BINARY)
axs[0,1].imshow(binary2, cmap = 'binary')
axs[0,1].set_title('BLUE')

(thresh, binary3) = cv2.threshold(gray, 70, 255, cv2.THRESH_BINARY)
axs[1,0].imshow(binary3, cmap = 'binary')
axs[1,0].set_title('RED-BLUE')

(thresh, binary4) = cv2.threshold(gray, 40, 255, cv2.THRESH_BINARY)
axs[1,1].imshow(binary4, cmap = 'binary')
axs[1,1].set_title('RED-GREEN-BLUE')
```
Untuk soal nomor 2, gambar akan diubah menjadi grayscale, yang nantinya muncul 4 subplot dalam satu gambar (2 baris dan 2 kolom). Untuk setiap subplot, dilakukan thresholding pada citra grayscale dengan menggunakan nilai ambang tertentu. Thresholding adalah proses mengubah citra ke citra biner di mana piksel di atas nilai ambang akan menjadi putih (255) dan di bawahnya menjadi hitam (0). Empat versi citra biner yang berbeda dihasilkan dengan menggunakan nilai ambang yang berbeda pula. Subplot pertama menunjukkan citra biner tanpa perubahan, sementara subplot kedua hingga keempat menunjukkan citra biner dengan threshold yang berbeda, dengan subplot kedua menggunakan nilai ambang 50, subplot ketiga menggunakan nilai ambang 70, dan subplot keempat menggunakan nilai ambang 90. Subplot-subplot tersebut ditampilkan menggunakan skala warna biner (hitam putih) untuk visualisasi hasil thresholding.


### Teori yang berkaitan dengan praktikum ini:
Pada praktikum kali ini, Deteksi warna, ambang batas, dan perubahan warna adalah konsep-konsep kunci dalam pemrosesan citra yang memainkan peran penting dalam berbagai aplikasi. Deteksi warna melibatkan identifikasi dan pemisahan area atau objek dalam citra berdasarkan warna mereka, sering kali menggunakan model warna seperti RGB atau HSV. 

Ambang batas, atau thresholding, digunakan untuk mengubah citra keabuan menjadi citra biner dengan memisahkan piksel berdasarkan nilai ambang, berguna untuk mengidentifikasi piksel dengan intensitas warna tertentu.

Perubahan warna merujuk pada analisis perubahan warna dalam citra dari waktu ke waktu atau dalam konteks spasial tertentu. Ini dapat melibatkan deteksi perubahan warna yang signifikan antara dua atau lebih citra yang diambil pada waktu yang berbeda, atau deteksi perubahan warna dalam suatu area tertentu dalam citra yang diakibatkan oleh peristiwa tertentu seperti pergerakan objek atau perubahan kondisi pencahayaan. 
