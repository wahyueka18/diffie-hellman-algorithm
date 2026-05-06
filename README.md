# Simulasi Algoritma Diffie-Hellman (Tugas Keamanan Jaringan)

## 1. Teori Dasar

## 2. Parameter

## 3. Struktur Kode dan Fungsi Utama

## 4. Persyaratan dan Cara Menjalankan

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
