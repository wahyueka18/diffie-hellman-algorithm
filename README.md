# Simulasi Algoritma Diffie-Hellman (Tugas Keamanan Jaringan)

## 1. Teori Dasar

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

## 5. Hasil Uji

## 6. Kesimpulan