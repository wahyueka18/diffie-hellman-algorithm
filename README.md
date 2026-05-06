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

--- 

## 2. Parameter

Dalam algoritma Diffie-Hellman Key Exchange, terdapat beberapa jenis parameter yang digunakan untuk menghasilkan kunci rahasia bersama. Berikut adalah rincian fungsional dari masing-masing parameter:

### Parameter Publik
Parameter ini bersifat terbuka, ditransmisikan melalui jaringan, dan dapat diketahui oleh semua pihak, termasuk penyerang. 

* **$p$ (Bilangan Prima):** 
  Digunakan sebagai modulus dalam operasi matematika. Fungsi utama $p$ adalah membatasi hasil perhitungan dalam sistem bilangan modular agar proses enkripsi tetap terstruktur dan aman.
* **$g$ (Generator):** 
  Bilangan yang digunakan sebagai basis dalam operasi perpangkatan modulo $p$. Nilai $g$ harus dipilih sedemikian rupa sehingga dapat menghasilkan banyak kemungkinan nilai (siklik) dalam sistem modulo $p$.

### Parameter Privat
Parameter ini bersifat sangat rahasia, tidak pernah ditransmisikan, dan hanya diketahui oleh masing-masing pihak.

* **$a$ (Private Key PC 1):** 
  Bilangan acak yang dipilih oleh pihak pertama sebagai kunci rahasia pribadi. Nilai ini digunakan secara internal untuk menghasilkan kunci publik pihak pertama.
* **$b$ (Private Key PC 2):** 
  Bilangan acak yang dipilih oleh pihak kedua. Sama seperti $a$, nilai ini bersifat rahasia dan tidak boleh diketahui pihak mana pun.

### Parameter Hasil (Kunci Publik)
Parameter ini merupakan nilai yang dihasilkan dari perhitungan kombinasi parameter publik ($p$ dan $g$) dengan parameter privat ($a$ atau $b$). Hasil ini kemudian dipertukarkan.

* **$A$ (Public Key PC 1):** 
  Kunci publik yang dihasilkan oleh pihak pertama. Nilai ini kemudian dikirimkan ke pihak kedua melalui jaringan. Rumusnya adalah:
  $$A = g^a \pmod p$$
  
* **$B$ (Public Key PC 2):** 
  Kunci publik yang dihasilkan oleh pihak kedua. Nilai ini kemudian dikirimkan ke pihak pertama melalui jaringan. Rumusnya adalah:
  $$B = g^b \pmod p$$

### Parameter Akhir (Shared Secret Key)
Setelah proses pertukaran kunci publik selesai, masing-masing pihak menghitung kunci rahasia akhir menggunakan kunci publik yang diterima dari lawan komunikasi dan kunci privat miliknya sendiri.

* **Perhitungan oleh Pihak Pertama (PC 1):**
  $$Secret = B^a \pmod p$$

* **Perhitungan oleh Pihak Kedua (PC 2):** 
  $$Secret = A^b \pmod p$$

Berkat sifat matematika modular eksponensial, kedua hasil perhitungan tersebut akan bermuara pada nilai yang identik:
$$B^a \pmod p = A^b \pmod p = g^{ab} \pmod p$$

Nilai akhir yang identik inilah yang disebut sebagai **Shared Secret Key (Kunci Rahasia Bersama)**, yang selanjutnya dapat digunakan untuk mengenkripsi pesan.

---

## 3. Struktur Kode dan Fungsi Utama

### Struktur Kode

Kode ini dibagi menjadi dua bagian utama: Antarmuka Pengguna (HTML/UI) dan Logika Perhitungan (Python/PyScript).

#### 1. Antarmuka Pengguna (HTML & Tailwind CSS)
Bagian ini mengatur tata letak, gaya visual, dan elemen interaktif yang dilihat oleh pengguna.
*   **Bagian Input (`<input>`):** Terdapat empat form input yang mengumpulkan parameter utama algoritma:
    *   `val-p`: Bilangan prima (Public Prime - $p$).
    *   `val-g`: Generator (Public Base - $g$).
    *   `val-a`: Kunci privat untuk PC 1 ($a$).
    *   `val-b`: Kunci privat untuk PC 2 ($b$).
*   **Tombol Pemicu:** Tombol "Mulai Simulasi" menggunakan atribut `py-click="start_simulation"` yang berfungsi menjembatani event HTML dengan fungsi Python di dalam PyScript.
*   **Area Simulasi (Visualisasi Pertukaran):** Dibagi menjadi tiga kolom utama:
    *   **PC 1 (Kiri):** Menampilkan perhitungan kunci publik $A$ dan kunci rahasia akhir.
    *   **Jalur Internet (Tengah):** Elemen visual (animasi *packet*) yang menunjukkan proses transmisi data kunci publik secara menyilang.
    *   **PC 2 (Kanan):** Menampilkan perhitungan kunci publik $B$ dan kunci rahasia akhir.

### 2. Pustaka Pihak Ketiga (Dependencies)
*   **Tailwind CSS:** Diimpor melalui CDN (`https://cdn.tailwindcss.com`) untuk penataan gaya (*styling*) secara cepat (misal: *flexbox*, *grid*, animasi transisi).
*   **PyScript:** Diimpor melalui tag `<script type="module" ...>` untuk memungkinkan eksekusi kode Python di dalam tag `<py>`.

### Fungsi Utama (PyScript)

Logika inti dari simulasi ini berjalan di dalam tag `<script type="py">`. Di sini, Python berinteraksi langsung dengan DOM web.

#### `power(a, b, P)`
Fungsi ini adalah *helper* matematika yang mensimulasikan eksponensial modular.
*   **Cara Kerja:** Menghitung nilai dari $a^b \pmod P$. Fungsi ini menggunakan metode bawaan Python `pow(a, b) % P` untuk mendapatkan sisa hasil bagi, yang merupakan inti dari perhitungan kriptografi Diffie-Hellman.

#### `async def start_simulation(event)`
Ini adalah fungsi asinkron (berjalan tanpa memblokir peramban) yang merupakan otak dari animasi dan simulasi. Fungsi ini dieksekusi saat tombol "Mulai Simulasi" diklik. Langkah-langkah di dalamnya meliputi:

1.  **Reset Status DOM:** 
    Menyembunyikan elemen teks (*opacity = 0*) dan mereset posisi awal animasi paket yang melintas di "Jalur Internet".
2.  **Pengambilan Nilai:** 
    Mengambil dan mengonversi nilai input HTML (string) menjadi bilangan bulat (integer) Python untuk variabel $p, g, a$, dan $b$.
3.  **Perhitungan Kunci Publik:** 
    Menghitung kunci publik yang akan disebarkan melalui jaringan terbuka:
    *   PC 1: $A = g^a \pmod p$
    *   PC 2: $B = g^b \pmod p$
4.  **Visualisasi Langkah 1:** 
    Menampilkan hasil perhitungan kunci publik di layar masing-masing PC dengan animasi *fade-in*.
5.  **Animasi Jaringan (Pertukaran Kunci):** 
    Menggunakan `await asyncio.sleep()` untuk memberi jeda, lalu memodifikasi properti CSS (`left`, `right`, `opacity`) dari elemen paket (`packet-A` dan `packet-B`) agar seolah-olah saling menyeberang di layar simulasi.
6.  **Perhitungan Kunci Rahasia Bersama (Shared Secret):** 
    Setelah paket tiba, masing-masing PC menghitung kunci rahasia (yang seharusnya menghasilkan angka yang sama):
    *   PC 1 menghitung: $Secret = B^a \pmod p$
    *   PC 2 menghitung: $Secret = A^b \pmod p$
7.  **Visualisasi Langkah Terakhir:** 
    Menampilkan kunci rahasia yang identik pada layar PC 1 dan PC 2 dengan warna hijau (Emerald) sebagai tanda bahwa koneksi aman telah berhasil dibuat.

---

## 4. Persyaratan dan Cara Menjalankan

### Persyaratan Sistem
Untuk menjalankan simulasi ini dengan lancar, Anda memerlukan:
* **Perangkat:** Komputer, laptop, tablet, atau *smartphone*.
* **Perangkat Lunak:** Peramban (*browser*) web modern (seperti Google Chrome, Mozilla Firefox, Safari, Microsoft Edge, dll).
* **Koneksi:** Internet aktif (diperlukan untuk mengakses tautan web, serta memuat *library* Tailwind CSS dan PyScript).

### Cara Menjalankan Simulasi
Ikuti langkah-langkah berikut untuk menggunakan aplikasi simulasi:

1. **Akses Website:** 
   Buka peramban web Anda dan kunjungi tautan berikut: [diffie-hellman-algorithm.vercel.app](https://diffie-hellman-algorithm.vercel.app) (atau buka file `index.html` pada *browser* jika Anda menjalankannya secara lokal).
2. **Input Parameter Publik:** 
   Pada form yang tersedia di bagian atas, masukkan nilai numerik pada kolom **Prime (p)** dan **Generator (g)**. Pastikan nilai (p) adalah bilangan prima.
3. **Input Kunci Privat:** 
   Masukkan angka acak yang akan menjadi rahasia masing-masing pihak pada kolom **Privat PC 1 (a)** dan **Privat PC 2 (b)**.
4. **Mulai Simulasi:** 
   Klik tombol biru bertuliskan **"Mulai Simulasi"** untuk mengeksekusi proses perhitungan matematis.
5. **Observasi Pertukaran Kunci:** 
   Perhatikan animasi pada panel di bawahnya. PC 1 dan PC 2 akan menghitung Kunci Publik masing-masing (A dan B), lalu visualisasi akan menunjukkan kedua kunci tersebut saling bertukar melewati "Jalur Internet".
6. **Verifikasi Hasil Akhir:** 
   Lihat pada kotak berwarna hijau di masing-masing panel PC (Langkah "Menghitung Kunci Rahasia!"). Simulasi dinyatakan **berhasil** jika nilai *Secret Key* (Kunci Rahasia) yang dihitung oleh PC 1 dan PC 2 menghasilkan angka yang sama persis.

--- 

## 5. Hasil Uji

![Screenshot Hasil Simulasi Diffie-Hellman](https://github.com/wahyueka18/diffie-hellman-algorithm/blob/main/images/image.png?raw=true)

Berdasarkan gambar simulasi di atas, berikut adalah penjelasan langkah demi langkah dari proses pertukaran kunci:

1. **Penentuan Parameter Publik (Global)**
   Langkah pertama, kami menetapkan nilai publik yang bersifat terbuka dan bisa diketahui oleh siapa saja. Di sini, kami menggunakan angka **Prime (p) = 23** sebagai dasar perhitungan modulus dan **Generator (g) = 5** sebagai angka dasar yang akan dipangkatkan. Kedua angka ini adalah titik awal kerja kami.

2. **Penentuan Kunci Privat (Rahasia)**
   Selanjutnya, masing-masing pihak dalam tim kami menentukan angka rahasianya sendiri yang tidak akan pernah dibagikan ke pihak lain. Dapat kita lihat, PC 1 menggunakan angka privat **6**, sementara PC 2 menggunakan angka **15**. Angka-angka ini tetap terkunci rapat di dalam masing-masing PC.

3. **Perhitungan Kunci Publik (Public Key)**
   Setelah rahasia ditetapkan, kami mulai melakukan perhitungan untuk menghasilkan kunci publik yang bisa dikirim. 
   * PC 1 menghitung hasil dari $5^6 \pmod{23}$ dan menghasilkan angka **8**. 
   * Secara bersamaan, PC 2 memproses angka dasarnya dengan perhitungan $5^{15} \pmod{23}$ dan menghasilkan angka **19**. 
   Inilah yang kami sebut sebagai kunci publik.

4. **Proses Pertukaran (Exchange)**
   Sekarang masuk ke tahap simulasi jalur internet. Di sini, kami saling menukarkan kunci publik tersebut. Kami mengirim angka **8** dari PC 1 ke PC 2, dan sebaliknya, angka **19** dari PC 2 dikirim ke PC 1. Meskipun angka 8 dan 19 ini melewati jalur internet yang terbuka, informasi kunci privat kami tetap aman.

5. **Hasil Akhir: Kunci Rahasia Bersama (Shared Secret Key)**
   Inilah bagian paling krusial dari percobaan kami. Setelah menerima kunci dari lawan, masing-masing PC melakukan perhitungan akhir menggunakan kunci privat mereka. 
   * PC 1 menghitung hasil dari $19^6 \pmod{23}$ dan mendapatkan angka **2**. 
   * Begitu pula dengan PC 2, yang menghitung $8^{15} \pmod{23}$ dan mendapatkan hasil yang sama persis, yaitu **2**.

### Kesimpulan Percobaan
Dengan hasil ini, simulasi kami dinyatakan **berhasil**. Meskipun kami bekerja dengan kunci privat yang berbeda dan hanya saling bertukar angka publik di internet, kami tetap berhasil menghasilkan *Shared Secret Key* yang identik, yaitu **2**. Angka 2 inilah yang nantinya dapat kami gunakan sebagai kunci rahasia untuk mengunci atau mengenkripsi data pada algoritma selanjutnya, seperti algoritma DES (Data Encryption Standard) atau AES.

---

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
