# SQL to Excel Converter

Script Python untuk mengkonversi file SQL dump menjadi file Excel (.xlsx) dengan format dokumentasi database yang rapi dan terstruktur.

## Fitur

- ✅ Mengkonversi semua file `.sql` dalam folder secara otomatis
- ✅ Mengekstrak struktur tabel dari `CREATE TABLE` statements
- ✅ Format Excel profesional dengan styling (warna, border, alignment)
- ✅ Preservasi tipe data kompleks seperti `decimal(10, 2)` dan `enum('a','b','c')`
- ✅ Pembersihan otomatis metadata SQL (NOT NULL, CHARACTER SET, COLLATE, DEFAULT, dll)
- ✅ Setiap tabel ditampilkan dengan format:
  - **Nama Tabel** (header dengan background kuning muda)
  - **Kolom**: No | Type Data | Description

## Instalasi

### 1. Clone Repository
```bash
git clone https://github.com/muflifadla38/sql-to-excel.git
cd sql-to-excel
```

### 2. Buat Virtual Environment (Opsional tapi Direkomendasikan)

```bash
python -m venv venv
```

Aktifkan virtual environment:

**Windows (Git Bash/MINGW64):**

```bash
source venv/Scripts/activate
```

**Windows (CMD):**

```cmd
venv\Scripts\activate.bat
```

**Linux/Mac:**

```bash
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

## Cara Penggunaan

### 1. Persiapan

Pastikan file SQL Anda berada dalam folder yang sama dengan `main.py`.

### 2. Jalankan Script

```bash
python main.py
```

### 3. Hasil

Script akan:

- Mencari semua file `.sql` di folder saat ini
- Mengekstrak struktur tabel dari setiap file
- Membuat file Excel dengan nama yang sama (contoh: `database.sql` → `database.xlsx`)

## Contoh Output

Untuk setiap tabel, Excel akan menampilkan:

```
┌─────────────────────────────────────────────────┐
│              banks                              │ (Background: Kuning Muda)
├──────────────┬─────────────────┬────────────────┤
│ No           │ Type Data       │ Description    │ (Background: Orange)
├──────────────┼─────────────────┼────────────────┤
│ id           │ bigint unsigned │                │
│ name         │ varchar(255)    │                │
│ image        │ varchar(255)    │                │
│ deleted_at   │ timestamp       │                │
│ created_at   │ timestamp       │                │
│ updated_at   │ timestamp       │                │
│ file_size    │ varchar(255)    │                │
│ description  │ longtext        │                │
└──────────────┴─────────────────┴────────────────┘
```

## Pembersihan Data Otomatis

Script akan otomatis membersihkan metadata SQL berikut:

- `NOT NULL` → dihapus
- `NULL` → dihapus
- `CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci` → dihapus
- `CHARACTER SET utf8mb4 COLLATE utf8mb4_bin` → dihapus
- `AUTO_INCREMENT` → dihapus
- `DEFAULT ...` → dihapus
- `COMMENT ...` → dihapus
- `ON UPDATE ...` → dihapus

## Preservasi Tipe Data Kompleks

Script memastikan tipe data dengan koma dan karakter khusus tetap utuh:

- ✅ `decimal(10, 2)` → Tetap `decimal(10, 2)` (tidak terpotong menjadi `decimal(10`)
- ✅ `enum('active','inactive','pending')` → Tetap utuh dengan semua nilai

Ini dicapai dengan menggunakan format text (`@`) pada kolom "Type Data" di Excel.

## Dependencies

- Python 3.7+
- openpyxl 3.1.2

## Struktur Project

```
sql-to-excel/
├── main.py              # Script utama
├── requirements.txt     # Dependencies Python
├── README.md           # Dokumentasi
└── *.sql               # File SQL input Anda
```

## Troubleshooting

### Error: Permission denied saat menyimpan Excel

**Penyebab:** File Excel sedang terbuka di Excel/program lain.

**Solusi:** Tutup file Excel tersebut terlebih dahulu, kemudian jalankan ulang script.

### Tipe data terpotong di Excel

**Penyebab:** Excel menginterpretasi koma sebagai pemisah.

**Solusi:** Script sudah menangani ini dengan format text (`@`). Pastikan menggunakan versi terbaru dari script.

### Tidak ada file SQL ditemukan

**Penyebab:** File `.sql` tidak berada di folder yang sama dengan `main.py`.

**Solusi:** Pindahkan file SQL ke folder yang sama atau ubah working directory.

## Contoh Penggunaan

```bash
# Contoh dengan satu file
$ ls
main.py  database.sql  requirements.txt

$ python main.py
Found 1 SQL file(s)
--------------------------------------------------

Processing: database.sql
  Found 45 table(s)
✓ Created: database.xlsx

==================================================
All SQL files have been converted to Excel!
==================================================

# Contoh dengan multiple files
$ ls
main.py  db1.sql  db2.sql  db3.sql  requirements.txt

$ python main.py
Found 3 SQL file(s)
--------------------------------------------------

Processing: db1.sql
  Found 30 table(s)
✓ Created: db1.xlsx

Processing: db2.sql
  Found 25 table(s)
✓ Created: db2.xlsx

Processing: db3.sql
  Found 40 table(s)
✓ Created: db3.xlsx

==================================================
All SQL files have been converted to Excel!
==================================================
```

## Lisensi

MIT License - Bebas digunakan untuk keperluan personal maupun komersial.

## Author

Script ini dibuat untuk memudahkan dokumentasi struktur database dari file SQL dump.
