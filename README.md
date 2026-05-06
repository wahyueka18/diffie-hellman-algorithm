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

## 3. Struktur Kode dan Fungsi Utama

## 4. Persyaratan dan Cara Menjalankan

## 5. Hasil Uji

## 6. Kesimpulan