# Simulasi Algoritma Diffie-Hellman (Tugas Keamanan Jaringan)

## 1. Teori Dasar

## 2. Parameter

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
