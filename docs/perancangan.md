# Dokumen Perancangan Admin Panel (Back-Office)

**Sistem Informasi Penerimaan Peserta Didik Baru (PPDB Online)**

*Milestone 1 - Perencanaan Menu, Arsitektur UI, & ER-D*

## 1. Identitas & Tema Visual UI

* **Topik Sistem:** Sistem Informasi Penerimaan Peserta Didik Baru (PPDB Online)

* **Tema Estetika UI:** **Glassmorphism**

* **Karakteristik Visual:**

  * Latar belakang menggunakan *Soft Gradient* gabungan warna Slate, Blue, dan Indigo (`from-slate-100 via-blue-50 to-indigo-100`).

  * Penggunaan kartu (*cards*) dan kontainer dengan efek transparansi putih (`rgba(255, 255, 255, 0.65)`).

  * Pengaplikasian efek *blur* latar belakang (`backdrop-filter: blur(16px)`).

  * Penggunaan *border* semi-transparan yang halus (`1px solid rgba(255, 255, 255, 0.5)`) untuk memisahkan bidang visual secara elegan.

## 2. Arsitektur Informasi & Hirarki Menu

Struktur navigasi Admin Panel dirancang untuk mempermudah alur kerja Panitia PPDB dalam memproses data pendaftar dari tahap awal hingga seleksi akhir.

```
[ ADMIN PANEL BACK-OFFICE ]
 ├── 1. Dashboard (Utama)
 │    ├── Ringkasan Statistik (Total Pendaftar, Verified, Pending, Rejected)
 │    ├── Grafik Pendaftar Per Jalur (Bar Chart)
 │    └── Tren Pendaftaran Harian (Line Chart)
 │
 ├── 2. Data Master
 │    ├── Data Pendaftar (Master Table)
 │    │    ├── Filter berdasarkan Jalur
 │    │    ├── Pencarian NISN / Nama
 │    │    └── Aksi Data (Tambah, Edit, Hapus / Modal Konfirmasi)
 │    └── Data Jalur Pendaftaran (Zonasi, Prestasi, Afirmasi, Pindah OT)
 │
 ├── 3. Kelola Pendaftaran & Verifikasi
 │    ├── Form Input / Edit Pendaftar (dengan Validasi JS Client-Side)
 │    └── Verifikasi Berkas & Dokumen
 │
 └── 4. Laporan & Pengumuman
      ├── Laporan Rekapitulasi PPDB (Siap Cetak / Print Mode)
      └── Pengumuman Hasil Seleksi

```

## 3. Entitas Relasi Data (ER-D)

Berikut adalah rancangan struktur data *mockup* menggunakan sintaks **Mermaid.js**:

```
erDiagram
    PANITIA ||--o{ VERIFIKASI_BERKAS : "memeriksa"
    PENDAFTAR ||--|| VERIFIKASI_BERKAS : "memiliki"
    PENDAFTAR }|--|| JALUR_PENDAFTARAN : "memilih"
    PENDAFTAR ||--o{ LAPORAN_DETAIL : "dicatat pada"

    PANITIA {
        string panitia_id PK
        string nama_panitia
        string email
        string role
    }

    JALUR_PENDAFTARAN {
        string jalur_id PK
        string nama_jalur
        int kuota
    }

    PENDAFTAR {
        int id PK
        string no_registrasi UK
        string nama_lengkap
        string nisn UK
        string jalur_id FK
        string status_verifikasi
    }

    VERIFIKASI_BERKAS {
        string verifikasi_id PK
        int pendaftar_id FK
        string panitia_id FK
        string status
        string catatan
    }

    LAPORAN_DETAIL {
        string laporan_id PK
        int pendaftar_id FK
        string tgl_cetak
    }

```

## 4. Design System Specification

### A. Color Palette

| Peruntukan | Kode Warna / Value | Tampilan CSS | 
 | ----- | ----- | ----- | 
| **Primary Accent** | `#2563eb` (Blue 600) | Accent Utama (Button, Active Link) | 
| **Glass Card Bg** | `rgba(255, 255, 255, 0.65)` | Permukaan Kartu / Container | 
| **Glass Border** | `rgba(255, 255, 255, 0.50)` | Garis Tepi Komponen Glass | 
| **Text Primary** | `#0f172a` (Slate 900) | Judul & Teks Utama | 
| **Text Secondary** | `#64748b` (Slate 500) | Subtitle & Label | 
| **Status Verified** | `#10b981` (Emerald 500) | Badge Diterima / Verified | 
| **Status Pending** | `#f59e0b` (Amber 500) | Badge Menunggu Verifikasi | 
| **Status Rejected** | `#f43f5e` (Rose 500) | Badge Ditolak / Perbaikan | 

### B. Tipografi

* **Font Family:** *Plus Jakarta Sans* atau *Inter* (Google Fonts)

* **Scale:**

  * Header / Page Title: `20px` (Bold)

  * Card Title / Section: `14px` (Bold)

  * Body Text: `12px` / `13px` (Regular / Medium)

  * Small / Badge Text: `10px` / `11px` (Semi-Bold)

### C. Komponen UI Reusable

* **Glass Card:** `background: rgba(255,255,255,0.65); backdrop-filter: blur(16px); border: 1px solid rgba(255,255,255,0.5); border-radius: 1rem;`

* **Input Field:** Rounded-xl dengan latar transparan `bg-white/70`, border halus, dan penanda fokus `ring-2 ring-blue-500`.

* **Primary Button:** Rounded-xl dengan gradien/solid Blue 600, teks putih, serta bayangan halus `shadow-blue-500/20`.

## 5. Tautan Prototyping & Wireframe

* **Tautan Publik Figma (Design System & High-Fidelity UI):**

  `https://www.figma.com/make/clNixpc9lXTr2X7nCXEaQn/Design-File?t=zNjsWYgkeWvRyh61-1` 

* **Tautan / Wireframe Stitch By Google:**

  `https://stitch.withgoogle.com/preview/18061454768093240502?node-id=b7f7dc7a5db34ce6aabf86a9b0b46c5e` 
  

### Tangkapan Layar Rancangan UI (Low/Mid-Fidelity)

#### 1. Dashboard Layout Wireframe

#### 2. Data Master Table Wireframe
