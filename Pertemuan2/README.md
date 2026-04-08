Nama: Windi Sulaiman Ismansa  
NIM: H1H024005  
Shift Awal : B  
Shift Akhir: A  
Pertemuan 2  


# 2.5.4 Pertanyaan Praktikum 
1\. Gambarkan rangkaian schematic yang digunakan pada percobaan!  
<img width="256" height="502" alt="Percobaan2A 2" src="https://github.com/user-attachments/assets/221d2e8f-806e-4000-8189-8e3421404470" />

2\. Apa yang terjadi jika nilai num lebih dari 15?  
Jika nilai num lebih dari 15 maka pogram akan mengalami kesalahan akses memori atau disebut buffer overflow. Yang  menyebabkan tampilan pada 7-segment menjadi acak atau karakter tidak beraturan, dan tidak menutup kemungkinan terjadinya crash.

3\. Apakah program ini menggunakan common cathode atau common anode? Jelaskan alasanya!  
Program ini menggunakan jenis Common Anode karena pada rangkaian pin 5V Arduino terhubung langsung ke kaki pusat (VCC) seven segment, sehingga semua anoda LED di dalamnya berbagi sumber tegangan positif yang sama. Kemudian pada sisi software digunakan logika pembalikan atau Active LOW melalui operator tanda seru (!) dalam kode digitalWrite, yang berfungsi mengirimkan sinyal nol volt atau LOW untuk menyalakan segmen dan sinyal HIGH untuk mematikannya.


4\. Modifikasi program agar tampilan berjalan dari F ke 0 dan berikan penjelasan disetiap baris kode nya dalam bentuk README.md!  


<img width="400" height="600" alt="f-0" src="https://github.com/user-attachments/assets/cc783661-d75a-4aac-b0e5-c391c6677dec" />  

* **`const int segmentPins[8] = {7, 6, 5, 11, 10, 8, 9, 4};`** Mendefinisikan pin digital Arduino yang terhubung ke segmen a, b, c, d, e, f, g, dan dp.
* **`byte digitPattern[16][8] = { ... };`** Matriks 2D yang menyimpan pola logika untuk membentuk karakter 0-9 dan A-F. Angka `1` berarti segmen aktif, `0` berarti mati.
* **`void displayDigit(int num)`** berfungsi untuk mengirimkan sinyal ke setiap pin segmen berdasarkan pola yang ada di matriks.
* **`digitalWrite(segmentPins[i], !digitPattern[num][i]);`** Mengirimkan logika terbalik ke pin. Karena menggunakan Common Anode, maka untuk menyalakan LED dibutuhkan sinyal LOW (`!1` = `0`).
* **`void setup()`** Mengatur semua pin segmen yang telah didefinisikan sebagai `OUTPUT` agar bisa mengirim arus.
* **`void loop()`** Inti dari program yang berjalan terus-menerus.
* **`for(int i = 15; i >= 0; i--)`** Melakukan perulangan mulai dari indeks 15 (karakter 'F') dan berkurang satu demi satu hingga mencapai 0.
* **`delay(1000);`** Memberikan jeda waktu selama 1 detik (1000 milidetik) sebelum berganti ke angka berikutnya.

# 2.6.4 Pertanyaan Praktikum 
1\. Gambarkan rangkaian schematic yang digunakan pada percobaan!  
<img width="256" height="502" alt="Percobaan1B 2" src="https://github.com/user-attachments/assets/c83b5479-1f46-4a3c-9249-86c501f79f85" />

2\. Mengapa pada push button digunakan mode INPUT_PULLUP pada Arduino Uno? Apa keuntungannya dibandingkan rangkaian biasa?
Mengapa digunakan?  

3\. Jika salah satu LED segmen tidak menyala, apa saja kemungkinan penyebabnya dari sisi hardware maupun software?  

4\. Modifikasi rangkaian dan program dengan dua push button yang berfungsi sebagai penambahan (increment) dan pengurangan (decrement pada sistem counter dan berikan penjelasan disetiap baris kode nya dalam bentuk README.md!  
<img width="400" height="600" alt="2 6 4" src="https://github.com/user-attachments/assets/8d4b1d70-d074-4f2b-b513-c0217a672fdf" />   

Menggunakan dua pushbutton untuk mengontrol tampilan dari 0-f pada rangkaian.
## Penjelasan Kode:
* **`const int btnUp = 3; btnDown = 2;`** berfungsi untuk mendefinisikan pin 3 untuk tambah dan pin 2 untuk kurang.
* **`pinMode(..., INPUT_PULLUP)`**: Untuk mengaktifkan resistor internal agar tombol tidak butuh resistor luar.
* **`if(lastBtnUpState == HIGH && stateUp == LOW)`**: mendeteksi 'Falling Edge' (tombol ditekan) agar angka hanya berubah satu kali tiap ditekan.
* **`if(currentDigit > 15) currentDigit = 0`**: Logika 'wrapping' agar setelah F kembali ke 0.
* **`if(currentDigit < 0) currentDigit = 15`**: Logika 'wrapping' agar setelah 0 kembali ke F saat dikurangi.
* **`delay(200)`**: Sebagai 'debounce' untuk mencegah satu tekanan tombol terbaca berkali-kali akibat getaran mekanis tombol.

# 2.7 Pertanyaan Praktikum
<div align="justify">
1\. Uraikan hasil tugas pada praktikum yang telah dilakukan pada setiap percobaan!  
Percobaan 1A (Automatic Counter):  
Hasil: Display menampilkan urutan heksadesimal (0, 1, 2, ... E, F) secara berulang dengan jeda 1 detik.  
Analisis: Program menggunakan perulangan for otomatis. Sistem ini membuktikan bahwa Arduino dapat melakukan tugas sekuensial berdasarkan waktu (time-based event).

Percobaan 1B (Manual Counter via Button)  
Hasil: Display hanya berganti angka ketika tombol ditekan. Angka akan kembali ke '0' setelah mencapai 'F'.  
Analisis: Program mengimplementasikan input handling. Penggunaan INPUT_PULLUP memastikan kestabilan pembacaan sinyal tanpa gangguan noise elektromagnetik (floating).

2\. Bagaimana prinsip kerja dari Seven Segment Display dalam menampilkan angka dan karakter? 

Seven Segment bekerja dengan prinsip dioda (LED) yang disusun membentuk pola angka.  
Tipe Common Anode (CA): Seluruh kaki positif (Anoda) dari kedelapan LED di dalam display dihubungkan ke satu jalur yaitu 5V (VCC).  
Aktif LOW: Karena Anoda sudah terhubung ke 5V, maka untuk menyalakan segmen tertentu, Arduino harus mengirimkan sinyal LOW (0V/GND) ke Katoda segmen tersebut agar terjadi perbedaan potensial.

Pembentukan Karakter: Setiap karakter (0-F) dibentuk dengan mengombinasikan segmen mana yang diberi sinyal LOW. Contohnya, untuk angka "1", hanya segmen b dan c yang diberi sinyal LOW, sementara segmen lainnya diberi sinyal HIGH.

3\. Jelaskan bagaimana sistem counter bekerja pada program tersebut! 
Sistem counter bekerja dengan menyimpan angka hitungan dalam variabel currentDigit yang berfungsi sebagai penunjuk indeks pada matriks pola segmen. Setiap kali tombol ditekan, program mendeteksi perubahan sinyal dan mengubah nilai variabel tersebut, baik bertambah (increment) maupun berkurang (decrement).

Untuk mencegah error, program menggunakan logika pembatas agar angka kembali ke 0 setelah mencapai F, atau kembali ke F jika dikurangi dari 0. Setelah nilai diperbarui, Arduino mengirimkan kombinasi sinyal biner dari array ke pin digital untuk menyalakan LED yang sesuai pada Seven Segment secara fisik.
</div>

