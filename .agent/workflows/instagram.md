---
description: Generate 4+ slide Instagram carousel dari soal LeetCode yang dikerjakan hari ini
---

# Workflow: Generate Instagram Carousel

Ketika user mengatakan "instagram", lakukan langkah-langkah berikut:

## 1. Identifikasi Soal Hari Ini

Cari file materi LeetCode **terakhir yang dikerjakan** di folder `fase-*`. Baca file tersebut untuk mendapatkan:
- Nama soal & nomor
- Difficulty & pattern
- Kode solusi user (bagian "✍️ Solusi Saya")
- Konsep kunci yang dipelajari
- Kompleksitas (Time & Space)

## 2. Generate 4+ Slide dengan generate_image

Buat **minimal 4 slide** Instagram carousel (format square 1080x1080) menggunakan tool `generate_image`. Semua slide harus memiliki style yang **konsisten dan premium**.

> **KUALITAS TINGGI:** Setiap prompt `generate_image` HARUS menyertakan instruksi: "high quality, sharp details, crisp text, 1080x1080 square format, professional design, no blur, clean edges". Jangan generate gambar yang buram atau low-res.

### Style Guide (Seperti @frontendjoe)
- **Background:** Dark theme, warna gelap (#0D1117 atau #1A1A2E) dengan subtle gradient atau glassmorphism
- **Font:** Modern sans-serif (Poppins, Inter, atau SF Pro) — bold untuk judul, regular untuk body
- **Warna aksen:** Vibrant gradient (ungu-biru, hijau-cyan, atau oranye-kuning)
- **Code block:** Dark editor theme dengan syntax highlighting (seperti VS Code dark theme), window dots (merah, kuning, hijau) di atas
- **Layout:** Clean, banyak whitespace, elemen tersusun rapi
- **Branding:** Setiap slide ada tag `#leetcode_granding` dan `@rofiqsukamieayam` di bagian bawah

### Struktur Slide

**Slide 1 — Cover/Hook:**
- Logo/ikon pattern (contoh: ikon Python, ikon Hash Map)
- Nama soal besar dan bold
- Difficulty badge (Easy/Medium/Hard dengan warna)
- Pattern yang digunakan
- Nomor soal LeetCode
- Tag & username di bawah

**Slide 2 — Deskripsi & Contoh:**
- Penjelasan singkat soal dalam Bahasa Indonesia
- Satu contoh input/output dengan visual yang jelas
- Highlight constraint penting
- Tag & username di bawah

**Slide 3 — Langkah Berpikir / Kerangka:**
- Visualisasi cara berpikir (step-by-step)
- Diagram atau flowchart sederhana
- Highlight pattern yang digunakan
- Tag & username di bawah

**Slide 4 — Kode Solusi:**
- Screenshot kode solusi user dalam style VS Code dark theme
- Window dots (merah, kuning, hijau) di atas
- Syntax highlighting Python
- Complexity badge (Time & Space) di bawah kode
- Tag & username di bawah

**Slide 5 (Opsional) — Tips & CTA:**
- Konsep kunci yang dipelajari
- Tips singkat
- Call to action: "Save untuk nanti! 🔖"
- Tag & username di bawah

## 2.5. Error Recovery

Jika terjadi **error saat generate_image** (misalnya timeout, rate limit, atau gagal lainnya):

1. **Jangan panik.** Tunggu sebentar lalu coba lagi.
2. **Setelah pulih, CEK slide terakhir yang berhasil di-generate.** Lihat di folder artifacts apakah file gambar slide sebelumnya sudah ada.
3. **Lanjutkan dari slide yang belum ter-generate.** Jangan ulangi slide yang sudah berhasil, kecuali kualitasnya buruk.
4. **Verifikasi kualitas setiap gambar** — jika gambar terlihat buram, terpotong, atau kualitasnya rendah, **generate ulang slide tersebut** dengan prompt yang sama ditambah penekanan "high quality, ultra sharp, crisp details".
5. **Pastikan semua slide lengkap** sebelum lanjut ke langkah berikutnya.

## 3. Pindahkan ke Downloads

Setelah semua slide di-generate, copy semua file gambar ke folder `C:\Users\TOSHIBA\Downloads\` dengan nama:
- `slide-1-cover.png`
- `slide-2-problem.png`
- `slide-3-thinking.png`
- `slide-4-code.png`
- `slide-5-tips.png` (jika ada)

## 4. Konfirmasi

Beritahu user:
- Berapa slide yang dibuat
- Preview singkat isi setiap slide
- Lokasi file di folder Downloads
