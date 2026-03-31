# Contributing Guide

Terima kasih sudah berkontribusi ke project **Big Data Analytics & Use Case (Decision-Oriented System)**.
Panduan ini dibuat agar kontribusi tetap konsisten, mudah direview, dan aman untuk dijalankan.

## Ruang Lingkup Project
Project ini mencakup 2 use case utama:
- **E-Commerce Analytics**: batch pipeline, streaming, analytics layer, dan dashboard.
- **Smart Transportation**: streaming trip, alerting, analytics, dan dashboard real-time.

## Prasyarat Kontributor
Pastikan environment lokal siap sebelum membuat perubahan:
- Python 3.10+ (disarankan 3.12)
- Java 8/11+ (untuk Spark)
- Virtual environment aktif (`.venv`)
- Dependency utama: `pyspark`, `streamlit`, `pandas`, `pyarrow`

Setup cepat:
```bash
python -m venv .venv
source .venv/bin/activate
pip install pyspark streamlit pandas pyarrow
```

## Struktur Folder yang Perlu Diperhatikan
- `scripts/` untuk pipeline utama (batch/streaming).
- `analytics/` untuk fungsi analitik yang reusable.
- `alerts/` untuk rule alert.
- `dashboard/` untuk UI Streamlit.
- `data/` untuk raw/clean/curated/serving/checkpoints.
- `logs/` untuk file log pipeline.

## Alur Kontribusi
1. Sync branch terbaru dari `main`.
2. Buat branch baru dengan nama deskriptif.
3. Lakukan perubahan kecil dan fokus per topik.
4. Jalankan validasi minimal (lihat bagian Testing).
5. Commit dengan pesan jelas.
6. Buat Pull Request berisi ringkasan perubahan, dampak, dan cara verifikasi.

## Konvensi Branch & Commit
Format branch yang disarankan:
- `feature/<nama-fitur>`
- `fix/<nama-perbaikan>`
- `docs/<nama-dokumen>`

Format commit message yang disarankan:
- `feat: tambah streaming layer transportation`
- `fix: perbaiki parsing timestamp pada analytics`
- `docs: rapikan struktur README`

## Standar Kode
- Gunakan Python yang konsisten dan mudah dibaca.
- Nama variabel/fungsi harus deskriptif.
- Tambahkan komentar hanya jika logika tidak langsung jelas.
- Hindari hardcoded path di luar struktur project.
- Pertahankan kompatibilitas dengan path yang sudah dipakai pipeline saat ini.

## Testing yang Wajib Sebelum PR
Jalankan pengecekan minimal sesuai area perubahan:

### Jika mengubah batch pipeline
```bash
python scripts/batch_pipeline_enterprise.py
python scripts/analytics_layer.py
```
Pastikan output terbuat di:
- `data/clean/parquet/`
- `data/curated/...`
- `data/serving/total_revenue`, `top_products`, `category_revenue`, `avg_transaction`

### Jika mengubah streaming e-commerce
Jalankan di terminal terpisah:
```bash
python scripts/transaction_generator.py
python scripts/streaming_layer.py
streamlit run dashboard/dashboard_streamlit.py
```
Pastikan data masuk ke `data/serving/stream` dan dashboard ter-update.

### Jika mengubah transportation use case
Jalankan di terminal terpisah:
```bash
python scripts/transportation/trip_generator.py
python scripts/transportation/streaming_trip_layer.py
streamlit run dashboard/dashboard_transportation.py
```
Pastikan data masuk ke `data/serving/transportation`, alert berfungsi, dan chart tampil normal.

## Aturan Data & File Besar
- Jangan commit data hasil generate yang sangat besar jika tidak diperlukan.
- Hindari commit file sementara atau cache (`__pycache__`, temp logs, dsb).
- Gunakan `.gitignore` untuk file yang bersifat lokal.

## Checklist Pull Request
Sebelum mengirim PR, pastikan:
- Perubahan sesuai scope issue/tugas.
- Script yang terdampak sudah berhasil dijalankan lokal.
- README diperbarui jika ada perubahan alur/struktur.
- Tidak ada file sensitif (credential, token, secret) yang ikut ter-commit.

## Pelaporan Bug
Saat melaporkan bug, sertakan:
- Langkah reproduksi.
- Script/file yang terdampak.
- Error log penting.
- Ekspektasi vs hasil aktual.

---
Terima kasih atas kontribusinya. Kontribusi kecil yang konsisten akan sangat membantu kualitas project ini.
