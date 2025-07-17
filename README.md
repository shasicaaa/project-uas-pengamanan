# JWT CRUD API UAS Starter

Silakan lanjutkan pengembangan API dan perbaiki bug yang ditemukan.

# UAS Keamanan Komputer

## Identitas
- Nama: Shasica Feby Juliananta
- NIM: 221080200015
- Kelas: Pengamanan Sistem Komputer 6B1/B4
- Repo GitHub: [https://github.com/shasicaaa/project-latihanci4-jwt.git]

---

## Bagian A – Bug Fixing JWT REST API

### Bug 1: Token tetap aktif setelah logout
**Penjelasan:**  
JWT bersifat stateless, sehingga logout tidak secara otomatis membuat token tidak berlaku. Hal ini berbahaya karena token lama masih bisa digunakan.
**Solusi:**  
1. Tambahkan mekanisme blacklist dengan menyimpan jti token ke database saat logout.
2. Middleware validasi JWT harus mengecek apakah jti sudah diblacklist.
3. Alternatif: gunakan access token pendek dan refresh token.

### Bug 2: Tidak ada pembatasan akses endpoint
**Penjelasan:**  
Semua endpoint bisa diakses siapa saja asal memiliki token, tanpa membedakan peran (role) user.
**Solusi:**  
1. Tambahkan middleware otorisasi berbasis role.
2. Contoh: hanya admin yang bisa akses /api/users atau operasi update user lain.

### Bug 3: User bisa mengakses data user lain
**Penjelasan:**  
User biasa bisa mengakses/mengubah data user lain hanya dengan mengganti user_id di request.
**Solusi:**  
1. Tambahkan validasi di backend bahwa req.user.id === body.user_id (untuk user biasa).
2. Jika tidak cocok dan user bukan admin → return 403.

## Bagian B – Simulasi Serangan dan Solusi

### Jenis Serangan: Broken Access Control  
Jenis serangan mengarah ke user, karena user bisa mengganti user_id lainnya.
**Simulasi Postman:**  
![alt text](image.png)
**Solusi Implementasi:**  
Menambahkan code pada file AuthFilter.php
![alt text](image-1.png)

## Bagian C – Refleksi Teori & Etika

### 1. CIA Triad dalam Keamanan Informasi  
1. Kerahasiaan (Confidentiality):
Memastikan bahwa informasi hanya dapat diakses oleh pihak yang berwenang. Ini berarti mencegah akses yang tidak sah, baik disengaja maupun tidak disengaja, ke data sensitif. Contohnya, penggunaan enkripsi untuk melindungi data saat transit atau penyimpanan, serta pembatasan akses pengguna melalui otentikasi dan otorisasi. 
2. Integritas (Integrity):
Memastikan bahwa data tidak diubah atau dimodifikasi tanpa izin. Hal ini mencakup menjaga keakuratan dan keutuhan data dari perubahan yang tidak sah, baik disengaja maupun tidak disengaja. Contohnya, penggunaan checksum untuk memverifikasi keaslian data dan mencegah korupsi data. 
3. Ketersediaan (Availability):
Memastikan bahwa informasi dan sistem yang relevan tersedia dan dapat diakses oleh pihak yang berwenang ketika dibutuhkan. Ini berarti memastikan bahwa sistem dan data dapat diakses dan digunakan tanpa gangguan, baik karena serangan siber maupun masalah teknis. Contohnya, penerapan redundansi, backup, dan pemulihan bencana untuk memastikan ketersediaan sistem. 

### 2. UU ITE yang relevan  
1. Pasal 30 Ayat (1), (2), dan (3) UU ITE:
“Setiap orang dengan sengaja dan tanpa hak atau melawan hukum mengakses komputer dan/atau sistem elektronik milik orang lain...”
•	Pelanggaran: Akses ilegal ke sistem atau data tanpa otorisasi.
•	Sanksi: Diatur dalam Pasal 46 UU ITE, dengan pidana penjara maksimal 8 tahun.
2. Pasal 32 Ayat (1) UU ITE:
“Setiap orang dengan sengaja dan tanpa hak atau melawan hukum mengubah, menambah, mengurangi, mentransmisikan, merusak, menghilangkan, memindahkan, atau menyembunyikan suatu informasi elektronik dan/atau dokumen elektronik milik orang lain...”
•	Pelanggaran: Perusakan atau manipulasi data digital.
•	Sanksi: Diatur dalam Pasal 48, pidana penjara maksimal 9 tahun.

### 3. Pandangan Al-Qur'an  
- Surah Al-Baqarah: 205  
Artinya:
"Dan apabila dia berpaling (dari kamu), dia berusaha (melakukan) kerusakan di bumi, dan merusak tanaman-tanaman dan ternak. Dan Allah tidak menyukai kerusakan." 
Tafsir:
Ayat ini menjelaskan bahwa orang yang berpaling dari kebenaran dan berbuat kerusakan di bumi, baik dengan merusak tanaman, ternak, maupun tatanan sosial, tidak disukai Allah. Kerusakan yang dimaksud tidak hanya terbatas pada kerusakan fisik, tetapi juga mencakup kerusakan moral dan sosial. Dalam konteks cyber ethics, ayat ini bisa ditafsirkan sebagai larangan untuk melakukan tindakan yang merusak sistem informasi, seperti menyebarkan berita palsu, melakukan perundungan dunia maya (cyberbullying), atau meretas sistem. 

### 4. Etika Cyber dan Kejujuran  
Kejujuran diperlukan saat bekerja dengan data sensitif, laporan audit, dan investigasi digital. Seorang profesional keamanan tidak boleh memanipulasi hasil atau menutupi kelemahan sistem. Dan Amanah berarti menjaga tanggung jawab atas data yang dipercayakan. Misalnya, admin sistem tidak boleh menyalahgunakan aksesnya untuk melihat atau menyebarkan data pribadi pengguna.
Contoh penerapan:
•	Tidak membocorkan kerentanan sebelum diperbaiki (responsible disclosure).
•	Melindungi hak akses walaupun tidak ada pengawasan.
•	Menolak perintah atasan jika bertentangan dengan hukum atau etika.
