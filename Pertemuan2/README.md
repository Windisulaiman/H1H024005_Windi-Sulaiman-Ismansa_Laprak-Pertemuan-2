Nama: Windi Sulaiman Ismansa  
NIM: H1H024005  
Shift Awal : B  
Shift Akhir: A  
Pertemuan 2  


# 2.5.4 Pertanyaan Praktikum 
1\. Gambarkan rangkaian schematic yang digunakan pada percobaan!  
<img width="256" height="502" alt="Screenshot 2026-04-12 230000" src="https://github.com/user-attachments/assets/51098477-a512-4631-b6da-67dc0bdaee31" />

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
<img width="256" height="502" alt="Screenshot 2026-04-12 225944" src="https://github.com/user-attachments/assets/61c24546-aca8-49ae-adec-951c3d70e2a3" />

<img width="256" height="502" alt="Percobaan1B 2" src="https://github.com/user-attachments/assets/c83b5479-1f46-4a3c-9249-86c501f79f85" />

2\. Mengapa pada push button digunakan mode INPUT_PULLUP pada Arduino Uno? Apa keuntungannya dibandingkan rangkaian biasa?
Mengapa digunakan?  
<div align="justify">
Penggunaan mode **`INPUT_PULLUP`** pada push button bertujuan untuk memanfaatkan resistor internal yang sudah tertanam di dalam mikrokontroler Arduino guna menarik tegangan pin ke level HIGH (5V) secara default. Tujuannya untuk menghindari kondisi floating, yaitu di mana keadaa pin input tidak memiliki tegangan yang pasti sehingga dapat berubah-ubah antara HIGH dan LOW akibat gangguan elektromagnetik di sekitar rangkaian.  
Benefit yang diberikan dibandingkan rangkaian biasa adalah desain rangkaian lebih sederhana, karena user tidak perlu lagi memasang resistor pull-up eksternal secara fisik di breadboard, yang sekaligus menghemat ruang dan mengurangi jumlah komponen serta kabel yang digunakan. Dengan mode ini, tombol cukup dihubungkan langsung antara pin digital dan GND, sehingga saat tombol ditekan, sinyal akan berubah menjadi LOW, yang membuat pembacaan input menjadi jauh lebih stabil dan akurat.  
  
3\. Jika salah satu LED segmen tidak menyala, apa saja kemungkinan penyebabnya dari sisi hardware maupun software?  
Beberaapa penyebab seven segment tidak menya ialah koneksi kabel jumper yang longgar atau tertukar, resistor yang terpasang di jalur yang salah, LED segmen yang rusak, atau orientasi pemasangan seven segment yang terbalik pada breadboard. Kemudian pada software juga memungkinkan menyebabkan seven segment tidak menyala yang disebabkan oleh kesalahan indeks pada array digitPattern (nilai bit terbalik), nomor pin yang tidak sesuai deklarasi segmentPins[], atau lupa memanggil pinMode() untuk pin yang bersangkutan pada fungsi setup() [5].
</div>
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
Berdasarkan percobaan 2A (Automatic Counter) yang telah dilakukan, sistem berhasil menampilkan urutan karakter dari 0 hingga F secara otomatis dan terus menerus berputar. Dengan memanfaatkan struktur perulangan for di dalam fungsi loop() yang secara sekuensial memanggil indeks baris pada matriks digitPattern berdasarkan variabel penghitung yang dikelola oleh sistem. Dengan adanya instruksi delay(1000), setiap karakter tertahan selama satu detik pada layar sebelum berpindah ke karakter berikutnya, hal ini menunjukkan bahwa mikrokontroler mampu mengeksekusi transisi logika biner menjadi representasi visual berdasarkan parameter waktu yang ditentukan secara presisi dalam code program.  

Pada percobaan 1B (Manual Counter via Button) menunjukkan transisi karakter pada seven segment sepenuhnya dikendalikan melalui push button. Berbeda dengan sistem otomatis, rangkaian ini menggunakan program logika deteksi status (state detection) pada pin digital 3 yang dikonfigurasi sebagai INPUT_PULLUP, sehingga variabel currentDigit hanya akan bertambah (increment) ketika terdeteksi perubahan sinyal dari HIGH ke LOW saat tombol ditekan. Selaian itu penerapan teknik debounce sederhana melalui delay 200ms, yang berfungsi untuk meminimalkan pembacaan ganda akibat getaran mekanis pada tombol, sehingga perpindahan dari angka 0 menuju F dan kembali lagi ke 0 dapat berjalan secara stabil dan responsif sesuai dengan input fisik yang diberikan.  

2\. Bagaimana prinsip kerja dari Seven Segment Display dalam menampilkan angka dan karakter?  
Seven segment display bekerja berdasarkan prinsip aktivasi selektif segmen LED. Mikrokontroler mengirimkan kombinasi sinyal HIGH/LOW pada delapan pin (a–g dan dp) yang terhubung ke setiap segmen. Untuk konfigurasi Common Anode, segmen menyala ketika mendapat logika LOW. Dengan menyalakan kombinasi segmen yang tepat, komponen ini mampu merepresentasikan angka 0–9 dan karakter A–F. Array digitPattern berperan sebagai lookup table yang menyimpan pola bit untuk setiap karakter, sehingga program cukup memanggil satu fungsi displayDigit() tanpa menulis ulang pola untuk setiap tampilan [3].

3\. Jelaskan bagaimana sistem counter bekerja pada program tersebut!  
Sistem counter pada program percobaan bekerja dengan memanfaatkan variabel **`currentDigit`** sebagai penyimpan nilai numerik yang berfungsi sebagai indeks untuk mengakses matriks pola segmen. Ketika program mendeteksi perubahan sinyal pada tombol dari HIGH ke LOW akibat penggunaan **`INPUT_PULLUP`**, nilai pada variabel akan dimanipulasi melalui operasi penambahan (increment) atau pengurangan (decrement).

Agar sistem tetap stabil, program menerapkan logic wrapping atau pembatas yang memastikan nilai variabel selalu berada dalam rentang 0 hingga 15. jika hitungan melampaui batas maksimal (F), maka posisi akan dikembalikan ke nol, dan sebaliknya. Setelah nilai variabel diperbarui, fungsi **`displayDigit`** akan segera memanggil baris data biner yang relevan dari memori dan mengirimkan sinyal Active LOW ke pin Arduino untuk mengubah konfigurasi nyala LED pada seven segment.
</div>

