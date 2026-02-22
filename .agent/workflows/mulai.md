---
description: Membuat file materi untuk soal LeetCode berikutnya yang belum dikerjakan
---

# Workflow: Mulai Materi Baru

Ketika user mengatakan "mulai", lakukan langkah-langkah berikut:

## 1. Cek Progress

Buka `README.md` dan cari soal yang belum di-checklist (`- [ ]`). Identifikasi soal **pertama yang belum dikerjakan** berdasarkan urutan di roadmap.

## 2. Identifikasi Tier dan Minggu

Tentukan soal tersebut berada di:
- **Tier** berapa (1-3)
- **Minggu** berapa
- **Folder** yang sesuai:
  - Tier 1 (Minggu 1-6) → `tier-1-foundation/`
  - Tier 2 (Minggu 7-11) → `tier-2-core/`
  - Tier 3 (Minggu 12-16) → `tier-3-advanced/`

## 3. Buat File Materi

Buat file markdown di folder tier yang sesuai dengan format nama:
- `minggu-{N}-{nama-soal}.md` (contoh: `minggu-1-two-sum.md`)

File harus berisi:
1. **Judul** — Nama soal, difficulty, pattern, link LeetCode
2. **Deskripsi Soal** — Penjelasan lengkap dalam Bahasa Indonesia
3. **Contoh** — Semua contoh dari soal dengan penjelasan
4. **Constraints** — Batasan input
5. **Kerangka Berpikir** — Langkah-langkah berpikir **seperti dosen mendiktekan**, meliputi:
   - Tangkap kata kunci dari soal
   - Visualisasikan dengan contoh kecil
   - Tentukan strategi/pattern yang dibutuhkan
   - Tentukan aturan/mekanisme (misalnya aturan pergerakan pointer)
   - Simulasikan di kertas (JANGAN langsung koding)
   - Baru tulis kode
   - Verifikasi dengan edge cases
   - Ringkasan kerangka berpikir dalam bentuk diagram/box
6. **Analisis & Cara Berpikir** — Pendekatan dari brute force ke optimal, langkah demi langkah
7. **Kode Solusi** — Dalam Python3 dengan komentar
8. **Kompleksitas** — Time & Space complexity untuk setiap pendekatan
9. **Konsep yang Dipelajari** — Teori dan konsep kunci
10. **Latihan Mandiri** — Instruksi untuk mengerjakan sendiri + test cases
11. **Checklist** — Progress tracking untuk soal ini
12. **Soal Terkait** — Soal-soal serupa untuk latihan tambahan

## 4. Bahasa

- Semua penjelasan ditulis dalam **Bahasa Indonesia**
- Kode ditulis dalam **Python3**
- Gunakan emoji untuk navigasi visual

## 5. Konfirmasi

Beritahu user file apa yang dibuat dan soal apa yang harus dikerjakan.
