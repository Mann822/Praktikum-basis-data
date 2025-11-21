📘 RANGKUMAN BAB 1 – Konversi ER Diagram ke Skema Relasi 

Bab 1 membahas tentang bagaimana cara mengubah ERD (Entity Relationship Diagram) menjadi skema relasi, lalu akhirnya menjadi tabel nyata di dalam database MySQL.

Ini penting karena ERD hanyalah desain, sedangkan tabel adalah bentuk nyata dalam database.


---

🔹 1. Konsep Dasar yang Harus Dipahami

1. Entitas

Entitas adalah objek nyata yang datanya ingin kita simpan.

Contoh: Mahasiswa, Buku, Pegawai, Pesanan, Obat.

Dalam database → entitas akan berubah menjadi tabel.


2. Atribut

Atribut adalah data atau ciri-ciri dari entitas.

Contoh atribut pada Mahasiswa:

NIM

Nama

Alamat

Tanggal Lahir


Dalam tabel → atribut menjadi kolom.


3. Primary Key (PK)

Yaitu kolom yang NILAINYA unik dan tidak boleh sama.

Digunakan untuk membedakan tiap baris data.

Contoh: NIM mahasiswa, ID pegawai.


4. Foreign Key (FK)

Kolom yang menghubungkan satu tabel dengan tabel lain.

Digunakan untuk menunjukkan relasi antar tabel.

Foreign Key selalu menunjuk ke PK tabel lain.


5. Relasi

Relasi adalah hubungan antar entitas.

Bentuk relasi:

1 ke 1

1 ke banyak

banyak ke banyak




---

🔹 2. Aturan Konversi ERD ke Tabel

Bab 1 menjelaskan aturan konversi, karena tidak semua komponen ERD bisa langsung dijadikan tabel secara langsung.

Berikut ringkasannya:


1. Entitas Kuat → Jadi 1 Tabel

Contoh:

Karyawan (nip, nama, alamat, tgl_lahir)

Menjadi tabel: | Nip (PK) | Nama | Alamat | Tgl_lahir |



2. Atribut Komposit → Dipecah

Atribut komposit = atribut yang terdiri dari beberapa bagian.

Contoh: Alamat = Jalan, Kota, Provinsi, Kode Pos

Maka tabel karyawan akan memiliki kolom:

jalan

kota

provinsi

kode_pos



3. Atribut Multivalue → Jadi Tabel Baru

Jika 1 orang punya banyak nilai untuk atribut yang sama.

Contoh: Karyawan memiliki banyak hobi.

Maka:

Tabel Karyawan

Tabel Hobby_Karyawan (nip, hobby)


FK: nip


4. Atribut Turunan

Contoh: umur → dihitung dari tanggal lahir.

Boleh menjadi kolom, tapi biasanya dihitung otomatis.


5. Entitas Lemah → Jadi 2 Tabel

Entitas lemah tidak punya PK sendiri tanpa entitas lain.

Contoh: Tanggungan (anak, istri) dari Karyawan.

Maka tabel:

Tanggungan (nip (FK), nama_tanggungan, hubungan)


6. Relasi 1 ke 1 (One to One)

Foreign key diletakkan pada salah satu tabel yang paling tepat.

Contoh: 1 pegawai memiliki 1 kartu identitas.


7. Relasi 1 ke Banyak (One to Many)

FK diletakkan pada tabel yang banyak.

Contoh: 1 Karyawan → banyak Peminjaman.

Tabel Peminjaman menyimpan:

nip (FK)

8. Relasi Banyak ke Banyak (Many to Many)

Selalu menghasilkan tabel baru.

Contoh: Buku — dipinjam → Peminjaman

Tabel baru:

Detail_Peminjaman (kd_peminjaman, kd_buku, lama_pinjam)

9. Relasi Ternary (melibatkan 3 entitas)

Selalu menghasilkan 4 tabel:

Tabel A

Tabel B

Tabel C

Tabel relasi gabungan

10. Generalisasi / Spesialisasi (ISA)

Contoh: Pasien → Pasien BPJS & Pasien Non BPJS

Superclass (Pasien) → tabel
Subclass → tabel baru berisi PK dari superclass.

Contoh tabel:

PASIEN (id, nama, alamat)

PASIEN_BPJS (id, nik_bpjs, jenis_bpjs)

PASIEN_NON_BPJS (id, faskes)


🔹 3. Studi Kasus Apotik

ERD Apotik terdiri dari tabel:

Pasien

Obat

Resep

Pembayaran

Pegawai

Kategori_Obat

Detail_Obat

Retur


Total tabel = 13 tabel

Semua ini dikonversikan mengikuti aturan konversi di atas.


📘 RANGKUMAN BAB 2 – Pengantar Basis Data & DDL 

Bab 2 membahas pengenalan database, DBMS, MySQL, dan perintah dasar DDL seperti membuat database.


🔹 1. Pengertian Database

Database adalah kumpulan data yang terorganisir dan saling berhubungan, disimpan dalam komputer, dan dapat diakses dengan mudah.

Tujuan database:

Menyimpan data dengan aman

Menghindari duplikasi

Mengakses data dengan cepat

Memudahkan pencarian data


🔹 2. Pengertian DBMS (Database Management System)

DBMS adalah software yang digunakan untuk:

membuat database

mengelola data

mengupdate data

mengamankan data

menghapus data


Contoh DBMS:

MySQL

PostgreSQL

Oracle

SQL Server


🔹 3. MySQL

MySQL adalah DBMS yang paling populer karena:

gratis & open source

cepat

stabil

mendukung banyak OS

banyak digunakan di web development

menggunakan bahasa SQL


MySQL ada 2 bagian:

MySQL Server → tempat database disimpan

MySQL Client → tempat kita mengetik perintah SQL

🔹 4. Instalasi MySQL

Cara termudah adalah menggunakan XAMPP, karena di dalamnya sudah terdapat:

Apache

MySQL (atau MariaDB)

phpMyAdmin


Di Windows:

C:\xampp\mysql\bin

🔹 5. Mengakses MySQL via CMD

Masuk ke folder MySQL:

cd C:\xampp\mysql\bin

Login:

mysql -u root -p

Keluar:

\q


🔹 6. Struktur Penyimpanan Database

Lokasi file database tersimpan:

Windows: C:\xampp\mysql\data

Linux: /opt/lampp/var/mysql


🔹 7. Tipe Data MySQL

Tipe Data	Fungsi

INT	angka bulat
FLOAT	angka desimal
CHAR	teks tetap
VARCHAR	teks fleksibel
DATE	tanggal
DATETIME	tanggal & waktu
BLOB	file / data besar


🔹 8. Database Relational

Database berisi banyak tabel

Tabel berisi banyak kolom

Tabel terhubung melalui PK & FK


🔹 9. Perintah DDL (Data Definition Language)

1. Membuat database

create database praktikum;

2. Melihat semua database

show databases;

3. Menggunakan database

use praktikum;

4. Menghapus database

drop database praktikum;








