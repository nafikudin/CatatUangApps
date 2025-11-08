
# Dokumen SRS (Software Requirements Specification) - CatatUang

**Versi:** 1.0
**Tanggal:** 8 November 2025
**Penulis:** [Tim Pengembang CatatUang]

---

## 1. Pendahuluan

*   **1.1. Tujuan Dokumen**
    Dokumen ini merinci persyaratan fungsional dan non-fungsional untuk aplikasi mobile "CatatUang". Tujuannya adalah untuk menjadi panduan teknis yang jelas bagi tim pengembangan, penguji, dan pemangku kepentingan lainnya, memastikan pemahaman yang seragam tentang apa yang akan dibangun.
*   **1.2. Lingkup Produk**
    CatatUang adalah aplikasi mobile pencatatan keuangan pribadi yang dirancang untuk platform iOS dan Android. Aplikasi ini akan membantu pengguna dalam melacak pemasukan dan pengeluaran harian, mengelola berbagai sumber dana (dompet), dan memahami kebiasaan finansial mereka melalui antarmuka yang intuitif dan minimalis.
*   **1.3. Definisi, Akronim, dan Singkatan**
    *   **PRD:** Product Requirement Document
    *   **SRS:** Software Requirements Specification
    *   **SDD:** Software Design Document
    *   **MVP:** Minimum Viable Product
    *   **UI:** User Interface
    *   **UX:** User Experience
    *   **CRUD:** Create, Read, Update, Delete
    *   **SQLite:** Sistem manajemen database relasional yang digunakan untuk penyimpanan lokal.
*   **1.4. Referensi**
    *   Dokumen PRD - CatatUang, Versi 1.0, 8 November 2025.
    *   Dokumen ERD - CatatUang, Versi 1.0, 8 November 2025.
    *   Dokumen SDD - CatatUang, Versi 1.0, 8 November 2025.

---

## 2. Deskripsi Umum

*   **2.1. Perspektif Produk**
    CatatUang adalah aplikasi *standalone* mobile yang beroperasi secara *offline-first* dengan penyimpanan data lokal. Saat ini tidak ada integrasi dengan sistem eksternal lain.
*   **2.2. Fungsi Produk**
    Aplikasi ini akan memungkinkan pengguna untuk:
    *   Membuat, melihat, mengedit, dan menghapus transaksi (pemasukan & pengeluaran).
    *   Membuat, melihat, mengedit, dan menghapus dompet (sumber dana).
    *   Membuat, melihat, mengedit, dan menghapus kategori transaksi.
    *   Melihat ringkasan keuangan (total pemasukan, pengeluaran, saldo) di dasbor.
    *   Melihat laporan visual sederhana (contoh: grafik lingkaran pengeluaran).
    *   Mengatur tema aplikasi (Light/Dark Mode).
*   **2.3. Karakteristik Pengguna**
    *   **Pengguna Pemula:** Pelajar, mahasiswa, atau pekerja muda yang mencari aplikasi pencatatan keuangan yang sederhana, cepat, dan mudah digunakan tanpa fitur akuntansi yang rumit.
    *   **Pengguna Lanjutan (Iterasi Berikutnya):** Menginginkan fitur-fitur seperti budgeting, pencatatan utang-piutang, sinkronisasi cloud, dan laporan yang lebih mendalam.
*   **2.4. Batasan Umum**
    *   Platform: Android & iOS.
    *   Tidak ada fitur autentikasi/akun pengguna di MVP.
    *   Data disimpan secara lokal di perangkat pengguna.
    *   Penggunaan bahasa Indonesia sebagai bahasa utama di MVP.
    *   Tidak ada integrasi API eksternal di MVP.

---

## 3. Persyaratan Fungsional (Functional Requirements)

Persyaratan fungsional diuraikan berdasarkan modul atau fitur utama.

*   **3.1. Manajemen Transaksi**
    *   **FR.TRN.1.001 - Menambahkan Transaksi Baru:**
        *   Deskripsi: Pengguna harus dapat menambahkan catatan transaksi baru.
        *   Input: Jumlah (wajib), Tipe (Pemasukan/Pengeluaran, wajib), Kategori (wajib), Dompet (wajib), Tanggal (wajib), Catatan (opsional).
        *   Output: Transaksi baru tersimpan dan muncul di daftar riwayat.
        *   Validasi: Jumlah harus berupa angka dan lebih besar dari nol.
    *   **FR.TRN.1.002 - Melihat Daftar Transaksi:**
        *   Deskripsi: Sistem harus menampilkan semua transaksi yang ada di halaman Riwayat, diurutkan dari yang terbaru.
        *   Aksi: Menyediakan filter untuk melihat transaksi berdasarkan periode (bulan dan tahun).
        *   Output: Daftar transaksi yang terorganisir.
    *   **FR.TRN.1.003 - Mengedit Transaksi:**
        *   Deskripsi: Pengguna harus dapat mengubah detail transaksi yang sudah ada.
        *   Input: Semua field pada transaksi yang dipilih.
        *   Output: Detail transaksi diperbarui di database dan UI.
    *   **FR.TRN.1.004 - Menghapus Transaksi:**
        *   Deskripsi: Pengguna harus dapat menghapus transaksi yang sudah ada.
        *   Aksi: Menampilkan dialog konfirmasi untuk mencegah penghapusan yang tidak disengaja.
        *   Output: Transaksi dihapus dari database dan UI, saldo dompet terkait diperbarui.
*   **3.2. Manajemen Dompet**
    *   **FR.WLT.1.001 - Menambahkan Dompet Baru:**
        *   Deskripsi: Pengguna harus dapat membuat dompet baru untuk memisahkan sumber dana.
        *   Input: Nama dompet (wajib), Saldo Awal (wajib).
        *   Output: Dompet baru tersimpan dan tersedia untuk dipilih saat transaksi.
    *   **FR.WLT.1.002 - Melihat Daftar Dompet:**
        *   Deskripsi: Sistem harus menampilkan daftar semua dompet yang ada beserta saldo terkini yang dihitung secara dinamis.
        *   Output: Daftar dompet dan saldonya.
    *   **FR.WLT.1.003 - Menghapus Dompet:**
        *   Deskripsi: Pengguna harus dapat menghapus dompet.
        *   Aksi: Menampilkan dialog konfirmasi yang memberitahu bahwa semua transaksi terkait akan ikut terhapus (`ON DELETE CASCADE`).
        *   Output: Dompet dan semua transaksinya terhapus.
*   **3.3. Manajemen Kategori**
    *   **FR.CAT.1.001 - Menambahkan Kategori Baru:**
        *   Deskripsi: Pengguna harus dapat membuat kategori transaksi sendiri.
        *   Input: Nama Kategori (wajib), Tipe (Pemasukan/Pengeluaran, wajib).
        *   Output: Kategori baru tersimpan dan tersedia untuk dipilih.
    *   **FR.CAT.1.002 - Menghapus Kategori:**
        *   Deskripsi: Pengguna dapat menghapus kategori yang telah dibuat.
        *   Batasan: Sistem akan menolak penghapusan jika kategori tersebut masih digunakan oleh transaksi (`ON DELETE RESTRICT`).
*   **3.4. Dasbor dan Laporan**
    *   **FR.REP.1.001 - Melihat Dasbor Ringkasan:**
        *   Deskripsi: Halaman utama aplikasi (Dasbor) harus menampilkan ringkasan keuangan untuk periode bulan berjalan.
        *   Output: Tampilan total pemasukan, total pengeluaran, dan saldo akhir bulan ini.
    *   **FR.REP.1.002 - Melihat Laporan Visual:**
        *   Deskripsi: Sistem harus menyediakan halaman laporan yang menampilkan grafik lingkaran (pie chart) untuk memvisualisasikan persentase pengeluaran berdasarkan kategori.
        *   Aksi: Pengguna dapat memfilter laporan berdasarkan periode waktu (misal: bulan ini, bulan lalu).
*   **3.5. Pengaturan**
    *   **FR.SET.1.001 - Mengatur Tema Aplikasi:**
        *   Deskripsi: Pengguna harus dapat memilih antara Light Mode atau Dark Mode.
        *   Input: Pilihan "Light", "Dark", atau "System Default".
        *   Output: Tema UI aplikasi berubah sesuai pilihan dan preferensi disimpan.

---

## 4. Persyaratan Non-Fungsional (Non-Functional Requirements)

*   **4.1. Kinerja (Performance)**
    *   **NFR.PER.1.001 - Kecepatan Respon UI:** Aplikasi harus merespon interaksi pengguna (misalnya, menyimpan transaksi) dalam waktu kurang dari 500 ms.
    *   **NFR.PER.1.002 - Waktu Loading:** Waktu *startup* aplikasi (cold start) tidak boleh lebih dari 3 detik pada perangkat kelas menengah.
    *   **NFR.PER.1.003 - Kinerja Database:** Operasi CRUD pada database lokal (SQLite) harus diselesaikan dalam waktu kurang dari 200 ms untuk hingga 5000 entri transaksi.
*   **4.2. Keamanan (Security)**
    *   **NFR.SEC.1.001 - Perlindungan Data Lokal:** Data keuangan pengguna yang disimpan secara lokal harus dilindungi dari akses tidak sah oleh aplikasi lain, sesuai dengan standar keamanan platform iOS dan Android (*sandboxing*).
*   **4.3. Keandalan (Reliability)**
    *   **NFR.REL.1.001 - Penanganan Crash:** Aplikasi harus dapat menangani error dengan baik untuk meminimalkan kehilangan data.
    *   **NFR.REL.1.002 - Konsistensi Data:** Perhitungan saldo pada dompet dan laporan harus selalu akurat dan konsisten setelah setiap operasi CRUD transaksi.
*   **4.4. Kemampuan Pemeliharaan (Maintainability)**
    *   **NFR.MNT.1.001 - Arsitektur Bersih:** Aplikasi harus dibangun mengikuti prinsip-prinsip arsitektur yang bersih (misal: MVVM) untuk memastikan kode yang modular dan mudah diubah.
    *   **NFR.MNT.1.002 - Dokumentasi Kode:** Kode sumber harus didokumentasikan dengan baik untuk memfasilitasi pemeliharaan di masa mendatang.
*   **4.5. Portabilitas (Portability)**
    *   **NFR.POR.1.001 - Kompatibilitas Platform:** Aplikasi harus berfungsi dengan baik di berbagai versi OS (misalnya, Android 6.0+ dan iOS 13+).
    *   **NFR.POR.1.002 - Ukuran Layar:** UI aplikasi harus beradaptasi secara responsif dengan berbagai ukuran layar perangkat mobile.
*   **4.6. Kegunaan (Usability)**
    *   **NFR.USA.1.001 - Desain Minimalis:** Antarmuka pengguna harus bersih, tidak berantakan, dan fokus pada fungsi inti pencatatan.
    *   **NFR.USA.1.002 - Navigasi Intuitif:** Pengguna harus dapat memahami dan menavigasi aplikasi dengan mudah tanpa perlu panduan.
    *   **NFR.USA.1.003 - Konsistensi UI:** Elemen UI dan pola interaksi harus konsisten di seluruh aplikasi.

---

## 5. Model Data (Berdasarkan ERD)

*   **5.1. Entitas `Wallet`**
    *   `id` (int): Primary Key, Auto Increment
    *   `name` (String): Nama dompet
    *   `initial_balance` (double): Saldo awal dompet
*   **5.2. Entitas `Category`**
    *   `id` (int): Primary Key, Auto Increment
    *   `name` (String): Nama kategori
    *   `type` (String): 'Pemasukan' atau 'Pengeluaran'
    *   `color` (String?): Warna hex untuk representasi UI (opsional)
*   **5.3. Entitas `Transaction`**
    *   `id` (int): Primary Key, Auto Increment
    *   `amount` (double): Jumlah uang
    *   `type` (String): 'Pemasukan' atau 'Pengeluaran'
    *   `transaction_date` (DateTime): Tanggal transaksi
    *   `notes` (String?): Catatan tambahan (opsional)
    *   `walletId` (int): Foreign Key ke Wallet.id
    *   `categoryId` (int): Foreign Key ke Category.id
    *   `createdAt` (DateTime): Waktu pembuatan
    *   `updatedAt` (DateTime): Waktu terakhir diubah

---

## 6. Lampiran

*   Wireframes/Mockup (Akan ditambahkan)
*   User Stories (Akan ditambahkan)
