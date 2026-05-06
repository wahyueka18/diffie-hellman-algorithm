![alt text](https://github.com/wahyueka18/diffie-hellman-algorithm/blob/vayu-branch/images/hasil%20skenario.png?raw=true)
1. Penentuan Parameter Publik (Global)
"Langkah pertama, kami menetapkan nilai publik yang bersifat terbuka dan bisa diketahui oleh siapa saja. Di sini, kami menggunakan angka Prime (p) = 23 sebagai dasar perhitungan modulus dan Generator (g) = 5 sebagai angka dasar yang akan dipangkatkan. Kedua angka ini adalah titik awal kerja kami."
2. Penentuan Kunci Privat (Rahasia)
"Selanjutnya, masing-masing pihak dalam tim kami menentukan angka rahasianya sendiri yang tidak akan pernah dibagikan ke pihak lain. Dapat kita lihat, PC 1 menggunakan angka privat 6, sementara PC 2 menggunakan angka 15. Angka-angka ini tetap terkunci rapat di dalam masing-masing PC."
3. Perhitungan Kunci Publik (Public Key)
"Setelah rahasia ditetapkan, kami mulai melakukan perhitungan untuk menghasilkan kunci publik yang bisa dikirim. PC 1 menghitung hasil dari 5^6 mod 23 dan menghasilkan angka 8. Secara bersamaan, PC 2 memproses angka dasarnya dan menghasilkan angka 19. Inilah yang kami sebut sebagai kunci publik."
4. Proses Pertukaran (Exchange)
"Nah, sekarang masuk ke tahap simulasi jalur internet. Di sini, kami saling menukarkan kunci publik tersebut. Kami mengirim angka 8 dari PC 1 ke PC 2, dan sebaliknya, angka 19 dari PC 2 dikirim ke PC 1. Meskipun angka 8 dan 19 ini melewati jalur terbuka, informasi kunci privat kami tetap aman."
5. Hasil Akhir: Kunci Rahasia Bersama (Shared Secret Key)
"Inilah bagian paling krusial dari percobaan kami. Setelah menerima kunci dari lawan, masing-masing PC melakukan perhitungan akhir menggunakan kunci privat mereka. PC 1 menghitung hasil dari 19^6 mod 23 dan mendapatkan angka 2. Begitu pula dengan PC 2, yang menghitung 8^15 mod 23 dan mendapatkan hasil yang sama persis, yaitu 2."
Kesimpulan Percobaan:
"Dengan hasil ini, simulasi kami dinyatakan berhasil. Meskipun kami bekerja dengan kunci privat yang berbeda dan hanya saling bertukar angka publik di internet, kami tetap berhasil menghasilkan Shared Secret Key yang sama, yaitu 2. Angka 2 inilah yang nantinya akan kami gunakan sebagai kunci untuk mengunci data pada algoritma selanjutnya, seperti DES."
