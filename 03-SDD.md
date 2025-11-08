# 📘 Software Design Document (SDD) — CatatUang

**Versi:** 1.0  
**Tanggal:** 8 November 2025  
**Author:** Tim Pengembang CatatUang

---

### **1.Pendahuluan**

### 1.1 Tujuan Dokumen
Dokumen Desain Perangkat Lunak (SDD) ini menyediakan deskripsi teknis tentang desain arsitektur dan komponen perangkat lunak untuk aplikasi mobile "CatatUang". Dokumen ini bertujuan untuk memandu tim pengembangan dalam implementasi sistem, memastikan semua persyaratan fungsional dan non-fungsional dari dokumen SRS terpenuhi, serta menjaga konsistensi arsitektur.

### 1.2 Lingkup Sistem
CatatUang adalah aplikasi pencatatan keuangan pribadi yang dikembangkan menggunakan Flutter. Desain ini mencakup struktur arsitektur Clean Code, modul-modul utama (Manajemen Transaksi, Dompet, Kategori, Laporan, Pengaturan), serta detail tentang bagaimana lapisan-lapisan dan komponen-komponen berinteraksi untuk mencapai fungsionalitas yang ditentukan dalam PRD dan SRS.

Aplikasi dikembangkan untuk platform Android & iOS menggunakan Flutter dengan penyimpanan lokal (offline-first).

### 1.3 Definisi dan Singkatan

| Istilah | Definisi |
|--------|---------|
| MVP | Minimum Viable Product |
| CRUD | Create, Read, Update, Delete |
| SQLite | Sistem database relasional untuk penyimpanan lokal |
| MVVM | Model-View-ViewModel, pola arsitektur UI |
| Repository | Pola desain untuk abstraksi akses data |

### 1.4 Referensi
- 01_PRD_CatatUang.md
- 02_ERD_CatatUang.md
- 03_SRS_CatatUang.md

---

### **2.Desain Arsitektur Sistem**

### 2.1 Tinjauan Arsitektur ✔ Clean Architecture
Arsitektur yang diadopsi adalah Clean Architecture untuk memastikan pemisahan tanggung jawab (Separation of Concerns) yang jelas antar lapisan.


Tentu, ini adalah Software Design Document (SDD) untuk aplikasi CatatUang yang disusun mengikuti format yang Anda berikan.
code
Md
# 📘 Software Design Document (SDD) — CatatUang

**Versi:** 1.0  
**Tanggal:** 8 November 2025  
**Author:** Tim Pengembang CatatUang

---

### **1.Pendahuluan**

### 1.1 Tujuan Dokumen
Dokumen Desain Perangkat Lunak (SDD) ini menyediakan deskripsi teknis tentang desain arsitektur dan komponen perangkat lunak untuk aplikasi mobile "CatatUang". Dokumen ini bertujuan untuk memandu tim pengembangan dalam implementasi sistem, memastikan semua persyaratan fungsional dan non-fungsional dari dokumen SRS terpenuhi, serta menjaga konsistensi arsitektur.

### 1.2 Lingkup Sistem
CatatUang adalah aplikasi pencatatan keuangan pribadi yang dikembangkan menggunakan Flutter. Desain ini mencakup struktur arsitektur Clean Code, modul-modul utama (Manajemen Transaksi, Dompet, Kategori, Laporan, Pengaturan), serta detail tentang bagaimana lapisan-lapisan dan komponen-komponen berinteraksi untuk mencapai fungsionalitas yang ditentukan dalam PRD dan SRS.

Aplikasi dikembangkan untuk platform Android & iOS menggunakan Flutter dengan penyimpanan lokal (offline-first).

### 1.3 Definisi dan Singkatan

| Istilah | Definisi |
|--------|---------|
| MVP | Minimum Viable Product |
| CRUD | Create, Read, Update, Delete |
| SQLite | Sistem database relasional untuk penyimpanan lokal |
| MVVM | Model-View-ViewModel, pola arsitektur UI |
| Repository | Pola desain untuk abstraksi akses data |

### 1.4 Referensi
- 01_PRD_CatatUang.md
- 02_ERD_CatatUang.md
- 03_SRS_CatatUang.md

---

### **2.Desain Arsitektur Sistem**

### 2.1 Tinjauan Arsitektur ✔ Clean Architecture
Arsitektur yang diadopsi adalah Clean Architecture untuk memastikan pemisahan tanggung jawab (Separation of Concerns) yang jelas antar lapisan.


+---------------------------------------------------------+
| Presentation Layer |
| (Flutter Widgets, State Management [e.g., Riverpod]) |
+---------------------------------------------------------+
|
V
+---------------------------------------------------------+
| Domain Layer |
| (Entities, UseCases, Abstract Repositories) |
+---------------------------------------------------------+
|
V
+---------------------------------------------------------+
| Data Layer |
| (Repository Impl, SQLite DB, Local Data Sources) |
+---------------------------------------------------------+


## 2.2 Deskripsi Lapisan

### 📍 Presentation Layer
- **Komponen:** Screens (Halaman), Widgets (Komponen UI), Providers (State Management).
- **Tanggung Jawab:** Menampilkan data ke pengguna dan menangkap input. Tidak mengandung logika bisnis. Meneruskan aksi pengguna ke Domain Layer melalui Use Cases.

### 🧠 Domain Layer
- **Komponen:** Entities (Model bisnis inti), Use Cases (Logika bisnis), Interfaces/Contracts Repository.
- **Tanggung Jawab:** Menjadi pusat dari semua logika bisnis aplikasi. Tidak bergantung pada detail implementasi UI maupun database.

### 🗄️ Data Layer
- **Komponen:** Implementasi Repository, Data Sources (Lokal), Model Data (DTO).
- **Tanggung Jawab:** Mengelola pengambilan dan penyimpanan data dari database lokal (SQLite). Mengimplementasikan kontrak repository yang didefinisikan di Domain Layer.

---

### **3.Desain Komponen Rinci**

### 3.1 Presentation Layer
📌 **Halaman Utama (Screens):**
- `DashboardScreen` → Menampilkan ringkasan keuangan.
- `AddEditTransactionScreen` → Formulir untuk menambah/mengedit transaksi.
- `HistoryScreen` → Daftar semua transaksi dengan filter.
- `WalletScreen` → Pengelolaan dompet (CRUD).
- `CategoryScreen` → Pengelolaan kategori (CRUD).
- `SettingsScreen` → Pengaturan tema aplikasi.

📌 **State Management:**
- Menggunakan state management solution seperti Riverpod atau Bloc untuk mengelola state UI secara efisien dan reaktif.

📌 **Routing (Navigasi):**
- Menggunakan package seperti `go_router` untuk menangani navigasi antar halaman secara terstruktur.
| Route | Halaman (Page) |
|------|------|
| `/` | DashboardScreen |
| `/add-transaction` | AddEditTransactionScreen |
| `/history` | HistoryScreen |
| `/wallets` | WalletScreen |
| `/categories` | CategoryScreen |
| `/settings` | SettingsScreen |

---

### 3.2 Domain Layer

#### **Entities:**
- `TransactionEntity`
- `WalletEntity`
- `CategoryEntity`

#### **Use Cases (Contoh):**
| Use Case | Fungsi |
|---------|--------|
| `AddTransaction` | Menangani logika untuk menambah transaksi baru. |
| `UpdateTransaction` | Menangani logika untuk mengedit transaksi. |
| `DeleteTransaction` | Menangani logika untuk menghapus transaksi. |
| `GetDashboardSummary` | Menghitung total pemasukan, pengeluaran, dan saldo. |
| `GetAllWallets` | Mengambil daftar semua dompet beserta saldo terkininya. |
| `AddWallet` | Menangani logika untuk membuat dompet baru. |

---

### **4. Desain Data (Database)**

*   **Implementasi:** Skema database yang telah dirancang dalam ERD akan diimplementasikan menggunakan ORM seperti `Drift` atau `Moor` (untuk Flutter), atau langsung menggunakan `sqflite`.
*   **Relasi:** Relasi `FOREIGN KEY` antara `Transactions` ke `Wallets` dan `Categories` akan didefinisikan dalam model tabel.
*   **Aturan Integritas:**
    *   `ON DELETE CASCADE` pada `Transactions.wallet_id` akan diimplementasikan untuk memastikan semua transaksi terhapus jika dompetnya dihapus.
    *   `ON DELETE RESTRICT` pada `Transactions.category_id` akan diimplementasikan untuk mencegah penghapusan kategori yang sedang digunakan.
*   **Migrasi:** Skema migrasi database akan dikelola oleh tools yang dipilih (misalnya, Drift) untuk menangani perubahan struktur tabel di versi aplikasi mendatang.

### **5. Strategi Penanganan Error (Error Handling)**

*   **Konsep:** Menggunakan pendekatan fungsional untuk penanganan error (misalnya, `Either` type dari package seperti `fpdart`) untuk memisahkan alur sukses dan alur gagal secara eksplisit.
*   **Alur:**
    1.  **Data Layer:** Setiap fungsi di Repository yang bisa gagal (misalnya, query database) akan mengembalikan `Future<Either<Failure, T>>`. Jika gagal, kembalikan `Left(DatabaseFailure("Pesan Error"))`. Jika sukses, kembalikan `Right(data)`.
    2.  **Domain Layer:** Use cases akan menerima dan meneruskan `Either` ini ke atas.
    3.  **Presentation Layer:** State management (Provider) akan mengelola state berdasarkan hasil `Either`. Widget akan me-render UI yang sesuai:
        *   Jika `Right`, tampilkan data.
        *   Jika `Left`, tampilkan widget error atau `SnackBar` dengan pesan yang relevan.
*   **Tipe `Failure`:**
    *   `abstract class Failure {}`
    *   `class DatabaseFailure extends Failure { final String message; }`

### **6.Struktur Proyek**

Struktur direktori akan mengikuti prinsip Clean Architecture dan modularisasi per fitur.
```
lib/
└── src/
├── core/ # Kode umum & utilitas
│ ├── error/ # Failure & Exception handling
│ ├── themes/ # Tema Light & Dark
│ └── utils/ # Helper, formatter, dll.
│
├── data/ # Data Layer
│ ├── datasources/ # Akses langsung ke SQLite
│ ├── models/ # Model data untuk tabel database
│ └── repositories/ # Implementasi Repository Domain
│
├── domain/ # Domain/Business Logic Layer
│ ├── entities/ # Model inti aplikasi
│ ├── repositories/ # Kontrak/Interface Repository
│ └── usecases/ # Logika bisnis per kasus penggunaan
│
└── presentation/ # UI Layer
├── features/ # Modular per fitur aplikasi
│ ├── dashboard/ # Fitur Dasbor
│ │ ├── screens/
│ │ └── widgets/
│ │
│ ├── transaction/ # Fitur Transaksi (form, riwayat)
│ │ ├── screens/
│ │ ├── widgets/
│ │ └── providers/
│ │
│ ├── wallet/ # Fitur Manajemen Dompet
│ │ ├── screens/
│ │ └── providers/
│ │
│ └── settings/ # Fitur Pengaturan
│ └── screens/
│
├── global_widgets/ # Widget yang digunakan di banyak fitur
└── routing/ # Konfigurasi navigasi (GoRouter)
└── app_router.dart
```
