# Dataset-Narkotika_450_476

Dataset putusan pengadilan perkara **Narkotika dan Psikotropika** dari **Pengadilan Negeri Jambi**,
dikumpulkan untuk tugas UTS mata kuliah **Temu Kembali Informasi** (Information Retrieval),
Program Studi Informatika, Universitas Muhammadiyah Malang, Semester Ganjil 2026/2027.

## Anggota Kelompok

| Nama | NIM |
|------|-----|
| Ananda Deftafio B.P. | 202310370311450 |
| Eka Danang P.H. | 202310370311476 |

## Isi Repositori

~~~
Dataset-Narkotika_450_476/
├── Dataset/
│   └── Narkotika.zip      # 50 dokumen putusan (*.pdf)
├── Overview/
│   └── Overview.xlsx      # ringkasan 50 putusan
└── README.md
~~~

## Ringkasan Dataset

- **Sumber:** Direktori Putusan Mahkamah Agung RI (https://putusan3.mahkamahagung.go.id/direktori.html)
- **Kategori:** Pidana Khusus, klasifikasi Narkotika dan Psikotropika
- **Pengadilan:** PN Jambi
- **Jumlah dokumen:** 50 putusan berformat PDF
- **Status putusan:** bukan putusan berkekuatan hukum tetap
- **Bahasa:** Indonesia
- **Rata-rata panjang kolom Amar Putusan:** sekitar 1733 karakter

Sebaran tahun perkara:

| Tahun | Jumlah Putusan |
|-------|----------------|
| 2025 | 4 |
| 2026 | 46 |

## Struktur Overview.xlsx

| Kolom | Isi |
|-------|-----|
| No | Nomor urut data |
| No Putusan | Nomor perkara, contoh `37/Pid.Sus/2026/PN Jmb` |
| Lembaga Peradilan | Pengadilan yang memutus perkara |
| Barang Bukti | Daftar barang bukti yang ditetapkan dalam amar putusan |
| Amar Putusan | Bunyi vonis majelis hakim, dari kata *MENGADILI* sampai sebelum penutup putusan |

## Cara Memakai

~~~python
import zipfile
import pandas as pd

df = pd.read_excel("Overview/Overview.xlsx")
print(df.head())

with zipfile.ZipFile("Dataset/Narkotika.zip") as z:
    print(len(z.namelist()), "berkas PDF")
~~~

## Cara Dataset Disusun

1. Putusan diunduh manual dari direktori Mahkamah Agung sesuai ketentuan tugas.
2. Teks tiap PDF diekstrak dengan `pdfplumber` (Python). Setiap halaman PDF memuat *watermark* berukuran
   besar dan teks hiasan yang menyisip di tengah kalimat, sehingga huruf watermark disaring berdasarkan
   warna, ukuran, dan jenis fontnya sebelum teks dipakai.
3. Kolom Amar Putusan diambil dengan pola *regular expression* mulai dari kata *MENGADILI*.
   Kolom Barang Bukti diambil dari kalimat *barang bukti berupa* di dalam amar putusan.
4. Hasilnya diperiksa dan disimpan ke Overview.xlsx.

## Catatan

- Hasil ekstraksi otomatis dapat memuat kesalahan kecil, misalnya kata yang menempel pada PDF tertentu.
- Dokumen putusan bersifat terbuka untuk publik dan bukan objek hak kekayaan intelektual.
  Dataset ini dipakai untuk keperluan pembelajaran.
