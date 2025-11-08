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
