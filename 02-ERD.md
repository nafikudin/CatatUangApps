## 2. Entity-Relationship Diagram (ERD)

ERD ini mendefinisikan struktur database lokal (SQLite) untuk aplikasi.

```mermaid
erDiagram
    WALLETS {
        int id PK
        varchar name
        decimal initial_balance
    }

    CATEGORIES {
        int id PK
        varchar name
        varchar type
    }

    TRANSACTIONS {
        int id PK
        decimal amount
        varchar type
        date transaction_date
        varchar notes
        int wallet_id FK
        int category_id FK
    }

    WALLETS ||--|{ TRANSACTIONS : "memiliki"
    CATEGORIES ||--|{ TRANSACTIONS : "termasuk_dalam"

Penjelasan Entitas
WALLETS: Merepresentasikan sumber dana pengguna (contoh: 'Tunai', 'Rekening BCA').
CATEGORIES: Mengelompokkan transaksi (contoh: 'Makanan', 'Gaji'). Memiliki tipe 'Pemasukan' atau 'Pengeluaran'.
TRANSACTIONS: Entitas inti yang mencatat setiap aktivitas keuangan, menghubungkan WALLETS dan CATEGORIES.

```
