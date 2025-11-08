# CatatUang - ERD (Entity-Relationship Diagram)

**Versi:** 1.0
**Tanggal:** 8 November 2025
**Penulis:** [Pengembang Aplikasi CatatUang]

---

## Gambaran Umum

ERD ini menggambarkan struktur database relasional untuk aplikasi CatatUang, dengan fokus pada entitas utama: `Wallets` (Dompet), `Categories` (Kategori), dan `Transactions` (Transaksi), serta hubungan di antara mereka. Pada MVP awal, aplikasi tidak memerlukan entitas `Users` karena semua data disimpan secara lokal di perangkat pengguna.

---

## Entitas:

### 1. Wallets (Dompet)
*   **id** (INTEGER, PRIMARY KEY, AUTOINCREMENT)
*   **name** (TEXT, NOT NULL) - Nama dompet yang mudah dikenali pengguna (misal: 'Tunai', 'Rekening BCA').
*   **initial_balance** (REAL, NOT NULL, DEFAULT 0) - Saldo awal saat dompet dibuat, untuk kalkulasi saldo total.

### 2. Categories (Kategori)
*   **id** (INTEGER, PRIMARY KEY, AUTOINCREMENT)
*   **name** (TEXT, NOT NULL) - Nama kategori transaksi (misal: 'Makanan', 'Gaji').
*   **type** (TEXT, NOT NULL, CHECK(type IN ('Pemasukan', 'Pengeluaran'))) - Menentukan jenis kategori.
*   **color** (TEXT, NULLABLE) - Opsional, untuk representasi warna kategori di UI (misal: hex code '#RRGGBB').

### 3. Transactions (Transaksi)
*   **id** (INTEGER, PRIMARY KEY, AUTOINCREMENT)
*   **amount** (REAL, NOT NULL) - Jumlah uang dari transaksi.
*   **type** (TEXT, NOT NULL, CHECK(type IN ('Pemasukan', 'Pengeluaran'))) - Jenis transaksi, harus sesuai dengan tipe kategori.
*   **transaction_date** (INTEGER, NOT NULL) - Tanggal terjadinya transaksi (disimpan sebagai Unix timestamp).
*   **notes** (TEXT, NULLABLE) - Catatan atau deskripsi tambahan untuk transaksi.
*   **wallet_id** (INTEGER, NOT NULL) - Foreign Key ke `Wallets.id`. Setiap transaksi harus berasal dari atau masuk ke satu dompet.
*   **category_id** (INTEGER, NOT NULL) - Foreign Key ke `Categories.id`. Setiap transaksi harus memiliki satu kategori.
*   **created_at** (INTEGER, NOT NULL) - Timestamp saat entri transaksi dibuat.
*   **updated_at** (INTEGER, NOT NULL) - Timestamp saat entri transaksi terakhir diubah.

---

## Hubungan (Relationships):

*   **Wallets (1) : (Many) Transactions**
    *   **Kardinalitas:** Satu dompet dapat memiliki banyak transaksi. Setiap transaksi hanya dimiliki oleh satu dompet.
    *   **Kunci Asing:** `Transactions.wallet_id` mereferensikan `Wallets.id`.
    *   **Aksi Saat Hapus:** `ON DELETE CASCADE` (jika sebuah dompet dihapus, semua transaksi yang terkait dengan dompet tersebut akan otomatis ikut terhapus untuk menjaga konsistensi data).

*   **Categories (1) : (Many) Transactions**
    *   **Kardinalitas:** Satu kategori dapat digunakan oleh banyak transaksi. Setiap transaksi hanya memiliki satu kategori.
    *   **Kunci Asing:** `Transactions.category_id` mereferensikan `Categories.id`.
    *   **Aksi Saat Hapus:** `ON DELETE RESTRICT` (sebuah kategori tidak dapat dihapus jika masih ada setidaknya satu transaksi yang menggunakannya. Ini untuk mencegah transaksi menjadi "yatim piatu" tanpa kategori).

---

## Diagram Visual (Konseptual):

+----------------+ +-------------------+ +----------------+
| Wallets | | Transactions | | Categories |
+----------------+ +-------------------+ +----------------+
| PK id | | PK id | | PK id |
| name | 1--M | amount | M--1 | name |
| initial_balance|------>| type |<------| type |
+----------------+ | transaction_date | | color |
| notes | +----------------+
| FK wallet_id |
| FK category_id |
| created_at |
| updated_at |
+-------------------+

---
