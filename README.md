![image](https://github.com/user-attachments/assets/57437fb4-e041-4738-8bd0-d18591925743)
![image](https://github.com/user-attachments/assets/23e7900e-31fb-4db7-9bc9-21de33159df0)
![image](https://github.com/user-attachments/assets/bb6ff3dc-4651-4cab-909c-77fe086c7e85)
![image](https://github.com/user-attachments/assets/a50e4688-fc5c-436a-a3bb-5775673949de)
![image](https://github.com/user-attachments/assets/0f478819-29cb-4e34-aafe-c466edfbf942)
![image](https://github.com/user-attachments/assets/3d1ecb32-e8ff-4155-8490-cb979eb1fdf7)

Penjelasan CRUD:

1. READ (Membaca Data)
- Menggunakan fungsi getMahasiswa() untuk menampilkan seluruh data mahasiswa
- Fungsi ini dijalankan saat komponen pertama kali diinisialisasi (ngOnInit)
- Data diambil melalui ApiService dengan endpoint tampil.php
- Data yang berhasil diambil akan disimpan ke variable dataMahasiswa untuk ditampilkan di view

2. CREATE (Menambah Data)
- Proses tambah data menggunakan fungsi tambahMahasiswa()
- Sebelum data ditambah, dilakukan validasi dimana nama dan jurusan tidak boleh kosong
- Data yang akan ditambah berupa objek dengan properti nama dan jurusan
- Pengiriman data melalui ApiService ke endpoint tambah.php
- Setelah berhasil menambah:
  - Form input dibersihkan
  - Data mahasiswa di-refresh
  - Modal form ditutup

3. UPDATE (Mengubah Data)
- Proses update terdiri dari 2 tahap:
  1. Mengambil data yang akan diedit menggunakan fungsi ambilMahasiswa()
     - Data diambil berdasarkan ID melalui endpoint lihat.php
     - Data yang diambil akan ditampilkan di form edit
  2. Mengirim data yang sudah diubah menggunakan fungsi editMahasiswa()
     - Data dikirim dalam bentuk objek berisi id, nama, dan jurusan
     - Pengiriman melalui endpoint edit.php
- Setelah berhasil update:
  - Form input dibersihkan
  - Data mahasiswa di-refresh
  - Modal form ditutup

4. DELETE (Menghapus Data)
- Menggunakan fungsi hapusMahasiswa()
- Sebelum menghapus, ditampilkan dialog konfirmasi
- Jika user mengkonfirmasi:
  - Data dihapus berdasarkan ID melalui endpoint hapus.php
  - Setelah berhasil, data mahasiswa di-refresh
- Jika user membatalkan, proses hapus dibatalkan

Fitur Pendukung:
1. Manajemen Modal
- Terdapat fungsi untuk membuka modal tambah (openModalTambah)
- Fungsi untuk membuka modal edit (openModalEdit) 
- Fungsi untuk menutup modal (cancel)
- Fungsi untuk membersihkan form input (resetModal)

2. Error Handling
- Setiap operasi CRUD memiliki penanganan untuk kondisi sukses dan gagal
- Pesan error/sukses ditampilkan di console

3. State Management
- Menggunakan property untuk menyimpan state seperti:
  - dataMahasiswa: menyimpan data seluruh mahasiswa
  - modalTambah: status modal tambah
  - modalEdit: status modal edit
  - id, nama, jurusan: untuk menyimpan data form

Implementasi CRUD ini sudah cukup baik karena:
- Menggunakan service terpisah untuk komunikasi dengan backend
- Memiliki validasi input
- Menggunakan modal untuk form input/edit
- Ada konfirmasi sebelum menghapus data
- Selalu melakukan refresh data setelah operasi CRUD
- Memiliki error handling
- Interface yang user-friendly dengan modal dan alert dialog

Penjelasan terkait alert koonfirmasi hapus mahasiswa:

1. Struktur Alert Konfirmasi
- Alert dibuat menggunakan AlertController dari Ionic Angular
- Alert memiliki beberapa komponen:
  - Header: menampilkan judul "Konfirmasi"
  - Message: menampilkan pesan konfirmasi "Apakah Data ingin dihapus?"
  - Buttons: terdapat 2 tombol untuk pilihan user

2. Tombol-tombol Alert
- Tombol "Tidak":
  - Berfungsi untuk membatalkan proses hapus
  - Memiliki role 'cancel'
  - Ketika diklik hanya akan menampilkan pesan di console bahwa hapus dibatalkan
  - Alert akan tertutup otomatis

- Tombol "Ya":
  - Berfungsi untuk melanjutkan proses hapus
  - Ketika diklik akan:
    - Memanggil API hapus dengan mengirimkan ID mahasiswa
    - Jika berhasil, data mahasiswa akan di-refresh
    - Menampilkan pesan sukses di console
    - Alert tertutup otomatis

3. Proses Alert
- Alert dibuat secara asynchronous menggunakan async/await
- Alur prosesnya:
  1. Alert dibuat dengan AlertController.create()
  2. Alert ditampilkan dengan alert.present()
  3. User memilih salah satu tombol
  4. Tindakan sesuai tombol yang dipilih dijalankan

4. Keuntungan Menggunakan Alert Konfirmasi
- Mencegah penghapusan data yang tidak disengaja
- Memberikan kesempatan user untuk membatalkan aksi
- Meningkatkan user experience dengan feedback yang jelas
- Mengikuti best practice UI/UX dalam penanganan aksi kritis

5. Integrasi dengan CRUD
- Alert ini terintegrasi dalam proses DELETE pada CRUD
- Menjadi lapisan keamanan sebelum data benar-benar dihapus
- Tetap mempertahankan flow refresh data setelah penghapusan berhasil

Implementasi alert konfirmasi ini menunjukkan perhatian terhadap user experience dan keamanan data, dimana user tidak bisa langsung menghapus data tanpa konfirmasi terlebih dahulu.
  

