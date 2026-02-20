---
description: Membuat file materi untuk soal LeetCode berikutnya yang belum dikerjakan
---

# Workflow: Mulai Materi Baru

Ketika user mengatakan "mulai", lakukan langkah-langkah berikut:

## 1. Cek Progress

Buka `README.md` dan cari soal yang belum di-checklist (`- [ ]`). Identifikasi soal **pertama yang belum dikerjakan** berdasarkan urutan di roadmap.

## 2. Identifikasi Fase dan Minggu

Tentukan soal tersebut berada di:
- **Fase** berapa (1-7)
- **Minggu** berapa
- **Folder** yang sesuai (fase-1-fondasi, fase-2-array-string, dst.)

## 3. Buat File Materi

Buat file markdown di folder fase yang sesuai dengan format nama:
- `minggu-{N}-{nama-soal}.md` (contoh: `minggu-1-two-sum.md`)

File harus berisi:
1. **Judul** — Nama soal, difficulty, pattern, link LeetCode
2. **Deskripsi Soal** — Penjelasan lengkap dalam Bahasa Indonesia
3. **Contoh** — Semua contoh dari soal dengan penjelasan
4. **Constraints** — Batasan input
5. **Analisis & Cara Berpikir** — Pendekatan dari brute force ke optimal, langkah demi langkah
6. **Kode Solusi** — Dalam Python3 dengan komentar
7. **Kompleksitas** — Time & Space complexity untuk setiap pendekatan
8. **Konsep yang Dipelajari** — Teori dan konsep kunci
9. **Latihan Mandiri** — Instruksi untuk mengerjakan sendiri + test cases
10. **Checklist** — Progress tracking untuk soal ini
11. **Soal Terkait** — Soal-soal serupa untuk latihan tambahan

## 4. Bahasa

- Semua penjelasan ditulis dalam **Bahasa Indonesia**
- Kode ditulis dalam **Python3**
- Gunakan emoji untuk navigasi visual

## 5. Konfirmasi

Beritahu user file apa yang dibuat dan soal apa yang harus dikerjakan.
