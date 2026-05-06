# Simulasi Algoritma Diffie-Hellman (Tugas Keamanan Jaringan)

## 1. Teori Dasar
Algoritma Diffie-Hellman (DH) adalah salah satu protokol kriptografi fundamental yang memungkinkan dua pihak untuk menyepakati sebuah kunci rahasia bersama (*shared secret key*) melalui saluran komunikasi publik yang tidak aman. Kunci rahasia ini nantinya dapat digunakan untuk enkripsi simetris pada komunikasi selanjutnya.

Penting untuk dicatat bahwa Diffie-Hellman **bukanlah algoritma enkripsi**, melainkan algoritma **pertukaran kunci (key exchange)**.

### Prinsip Kerja Matematis
Keamanan Diffie-Hellman didasarkan pada perhitungan aritmatika modular dan tingkat kesulitan dalam memecahkan masalah Logaritma Diskrit (*Discrete Logarithm Problem*). 

Berikut adalah alur pertukaran kuncinya:

**1. Penentuan Parameter Publik**
Kedua belah pihak (sebut saja Alice dan Bob) menyepakati dua variabel publik yang bisa dilihat oleh siapa saja:
* $p$: Sebuah bilangan prima yang sangat besar.
* $g$: Sebuah *generator*, yaitu bilangan bulat dasar yang lebih kecil dari $p$.

**2. Pembuatan Kunci Privat dan Publik**
Masing-masing pihak menghasilkan kunci privat secara lokal dan menghitung kunci publik mereka:
* **Alice** memilih kunci privat acak $a$, lalu menghitung kunci publik $A$:
  $$A = g^a \pmod p$$
* **Bob** memilih kunci privat acak $b$, lalu menghitung kunci publik $B$:
  $$B = g^b \pmod p$$

**3. Pertukaran Kunci Publik**
Alice mengirimkan kunci publik $A$ kepada Bob, dan Bob mengirimkan kunci publik $B$ kepada Alice melalui saluran yang terbuka.

**4. Perhitungan Kunci Rahasia Bersama (Shared Secret)**
Setelah menerima kunci publik masing-masing, keduanya menghitung kunci rahasia bersama ($S$) menggunakan kunci privat lokal mereka:
* **Alice** menghitung:
  $$S = B^a \pmod p$$
* **Bob** menghitung:
  $$S = A^b \pmod p$$

Secara matematis, perhitungan yang dilakukan oleh Alice dan Bob akan menghasilkan nilai $S$ yang identik:
$$S = (g^b)^a \pmod p = (g^a)^b \pmod p = g^{ab} \pmod p$$

### Tingkat Keamanan
Keamanan dari protokol ini terletak pada fakta bahwa meskipun pihak ketiga (*attacker*) dapat menyadap variabel publik ($p$, $g$, $A$, dan $B$), sangat sulit secara komputasi untuk mencari nilai privat $a$ atau $b$ dari variabel tersebut. Proses matematis ini mudah dihitung ke satu arah (eksponensial), tetapi sangat sulit untuk dibalikkan (logaritma diskrit).

## 2. Parameter
Parameter Publik
Parameter ini dapat diketahui oleh semua pihak, termasuk penyerang. 
 p (bilangan prima) 
Bilangan prima digunakan sebagai modulus dalam operasi matematika. Fungsi utama p adalah membatasi hasil perhitungan dalam sistem bilangan modular agar proses enkripsi tetap terstruktur dan aman.
g (generator) 
Generator adalah bilangan yang digunakan sebagai basis dalam operasi perpangkatan modulo p. Nilai g harus dipilih sedemikian rupa sehingga dapat menghasilkan banyak kemungkinan nilai dalam sistem modulo p.

Parameter Private
 Parameter ini bersifat rahasia dan hanya diketahui oleh masing-masing pihak
A (private key PC 1) 
Bilangan acak yang dipilih oleh pihak pertama sebagai kunci rahasia. Nilai ini digunakan untuk menghasilkan kunci publik.
B (private key PC 2) 
Bilangan acak yang dipilih oleh pihak kedua. Sama seperti a, nilai ini tidak boleh diketahui pihak lain.

Parameter Hasil (kunci publik) 
Parameter hasil merupakan nilai yang dihasilkan dari kombinasi parameter publik dan privat, kemudian dibagikan ke pihak lain dalam proses Diffie-Hellman Key Exchange.
A (publik key PC 1) 
Kunci publik yang dihasilkan oleh pihak pertama menggunakan rumus:
A = g^a  mod p
Nilai ini kemudian dikirimkan ke pihak kedua melalui jaringan.
B (publik key PC 2) 
Kunci publik yang dihasilkan oleh pihak kedua dengan rumus:
B = g^b mod p
Nilai ini kemudian dikirimkan ke pihak pertama

Parameter Akhir (shared secret key) 
Setelah pertukaran kunci publik, masing-masing pihak menghitung kunci rahasia menggunakan rumus:

Pihak pertama :
Secret = B^a mod p

Pihak kedua : 
Secret = A^b mod p

Kedua hasil tersebut akan menghasilkan nilai yang sama:
B^a mod p = A^b mod p = g^ab mod p

Inilah yang menjadi kunci rahasia bersama (shared secret key).

## 3. Struktur Kode dan Fungsi Utama

## 4. Persyaratan dan Cara Menjalankan

PERSYARATAN
- Perangkat         : Komputer, laptop, atau smartphone.
- Perangkat Lunak   : Peramban web modern (Google Chrome, Firefox, Safari, dll.)
- Koneksi           : Internet (jika website diakses melalui tautan URL web).

CARA MENJALANKAN SIMULASI 
- Akses Website: Buka peramban web dan kunjungi tautan diffie-hellman-algorithm.vercel.app
dijalankan secara lokal.
- Input Parameter Publik: Pada form yang tersedia, masukkan nilai bilangan prima pada kolom Prime (p) dan Generator (g).
- Input Kunci Privat: Masukkan angka acak yang akan menjadi rahasia masing-masing pihak pada kolom Privat PC 1 (a) dan Privat PC 2 (b).
- Mulai Simulasi: Klik tombol biru "Mulai Simulasi" untuk menjalankan proses perhitungan matematis.
- Observasi Pertukaran Kunci: Perhatikan panel hasil di bawahnya. PC 1 dan PC 2 akan menghasilkan Kunci Publik (A dan B) lalu disimulasikan saling bertukar kunci tersebut melewati "Jalur Internet".
- Verifikasi Hasil Akhir: Lihat pada kotak hijau di masing-masing panel PC. Simulasi dinyatakan berhasil jika nilai Kunci Rahasia (Secret Key) yang dihitung oleh PC 1 dan PC 2 menghasilkan angka yang sama persis.

## 5. Hasil Uji

## 6. Kesimpulan
Berdasarkan hasil perancangan, implementasi kode, dan simulasi yang telah dilakukan, dapat ditarik beberapa kesimpulan utama sebagai berikut:

### 1. Keberhasilan Protokol Pertukaran Kunci
Simulasi ini membuktikan bahwa algoritma **Diffie-Hellman (DH)** berhasil menjalankan fungsinya sebagai protokol pertukaran kunci. Dua entitas (PC 1 dan PC 2) dapat menghasilkan **Shared Secret Key** yang identik melalui jalur komunikasi publik tanpa perlu mengirimkan kunci rahasia tersebut secara langsung.

### 2. Peran Parameter Publik $p$ dan $g$
Variabel $p$ (Prime) dan $g$ (Generator) memegang peranan krusial dalam keamanan algoritma:
* **$p$ (Bilangan Prima):** Berfungsi sebagai modulus yang membatasi ruang angka hasil perhitungan. Semakin besar nilai $p$, semakin sulit bagi penyerang untuk melakukan *brute-force*.
* **$g$ (Generator):** Bertindak sebagai basis eksponensial yang memastikan distribusi kunci yang aman dalam ruang modular.

### 3. Keamanan melalui Masalah Logaritma Diskrit
Keamanan sistem ini bertumpu pada **Discrete Logarithm Problem**. Meskipun pihak ketiga (eavesdropper) dapat menyadap parameter publik ($p, g, A, B$), secara komputasi sangat sulit untuk mencari nilai kunci privat ($a$ atau $b$) yang diperlukan untuk merekonstruksi kunci rahasia bersama.

### 4. Validitas Matematis
Proses simulasi menunjukkan konsistensi matematis di mana:
$$S = (g^b)^a \pmod p = (g^a)^b \pmod p$$
Hasil akhirnya, baik di sisi PC 1 maupun PC 2, menunjukkan nilai **Secret Key** yang sama persis, yang menandakan bahwa simulasi berjalan dengan benar (Valid).

### 5. Catatan Implementasi di VS Code
Kode yang disusun menggunakan logika aritmatika modular memastikan bahwa perangkat dengan sumber daya terbatas (seperti yang disimulasikan pada web) dapat menjalankan proses enkripsi kunci ini dengan efisien sebelum digunakan lebih lanjut dalam algoritma simetris seperti AES.
