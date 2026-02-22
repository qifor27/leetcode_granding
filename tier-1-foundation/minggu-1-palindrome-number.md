# 🔢 9. Palindrome Number

| Info | Detail |
|------|--------|
| **Soal** | [9. Palindrome Number](https://leetcode.com/problems/palindrome-number/) |
| **Difficulty** | 🟢 Easy |
| **Pattern** | Math |
| **Tier** | 1 — Foundation |
| **Minggu** | 1 |

---

## 📖 Deskripsi Soal

Diberikan sebuah bilangan bulat (integer) `x`, tentukan apakah `x` adalah **palindrome** (bilangan yang dibaca dari depan dan belakang sama).

**Palindrome** artinya nilainya sama ketika dibalik.

> **Follow-up:** Bisakah kamu menyelesaikan ini **tanpa mengkonversi integer ke string**?

---

## 📋 Contoh

### Contoh 1
```
Input: x = 121
Output: true
Penjelasan: 121 dibaca dari kiri ke kanan: 121
             121 dibaca dari kanan ke kiri: 121
             Sama! → Palindrome ✅
```

### Contoh 2
```
Input: x = -121
Output: false
Penjelasan: Dari kiri ke kanan: -121
             Dari kanan ke kiri: 121-
             Berbeda! → Bukan palindrome ❌
             (Bilangan negatif TIDAK PERNAH palindrome karena tanda minus)
```

### Contoh 3
```
Input: x = 10
Output: false
Penjelasan: Dari kiri ke kanan: 10
             Dari kanan ke kiri: 01
             Berbeda! → Bukan palindrome ❌
```

### Contoh 4 (Edge Case)
```
Input: x = 0
Output: true
Penjelasan: 0 dibalik tetap 0 → Palindrome ✅
```

---

## 🔒 Constraints

- `-2³¹ <= x <= 2³¹ - 1`

---

## 🧠 Kerangka Berpikir

> 💡 Bayangkan kamu seorang dosen yang mendiktekan langkah-langkah berpikir ke mahasiswa...

### Langkah 1: Tangkap Kata Kunci
- **"palindrome"** → dibaca sama dari depan dan belakang
- **"integer"** → bilangan bulat, bukan string
- **"-121 → false"** → bilangan negatif SELALU bukan palindrome
- **"tanpa konversi ke string"** → tantangan: gunakan pendekatan matematika

### Langkah 2: Eliminasi Kasus Sederhana
Sebelum mikir solusi, pikirkan kasus yang **langsung bisa dijawab**:
- ❌ Bilangan **negatif** → PASTI bukan palindrome (ada tanda `-`)
- ❌ Bilangan yang **berakhiran 0** (selain 0 itu sendiri) → PASTI bukan palindrome
  - Contoh: 10, 100, 1230 → dibalik jadi 01, 001, 0321 → tidak valid
- ✅ Bilangan **satu digit** (0-9) → PASTI palindrome

### Langkah 3: Tentukan Strategi
Kita punya **2 pendekatan**:

| Pendekatan | Cara | Kelebihan |
|-----------|------|-----------|
| **String** | Konversi ke string, bandingkan dengan string terbalik | Simpel, mudah dipahami |
| **Math** | Balik setengah angka, bandingkan | Tanpa extra memory |

### Langkah 4: Visualisasi Pendekatan Math (Setengah Balik)

> Ide kunci: kita **tidak perlu membalik SELURUH angka**. Cukup balik **setengahnya** lalu bandingkan.

```
Contoh: x = 1221

Langkah 1: reversed = 0, x = 1221
  → digit terakhir = 1221 % 10 = 1
  → reversed = 0 * 10 + 1 = 1
  → x = 1221 / 10 = 122

Langkah 2: reversed = 1, x = 122
  → digit terakhir = 122 % 10 = 2
  → reversed = 1 * 10 + 2 = 12
  → x = 122 / 10 = 12

STOP! reversed (12) >= x (12)
Bandingkan: x == reversed → 12 == 12 → TRUE ✅
```

```
Contoh: x = 12321 (ganjil digit)

Langkah 1: reversed = 0, x = 12321
  → reversed = 1, x = 1232

Langkah 2: reversed = 12, x = 123

Langkah 3: reversed = 123, x = 12

STOP! reversed (123) >= x (12)
Bandingkan: x == reversed // 10 → 12 == 123 // 10 → 12 == 12 → TRUE ✅
(Buang digit tengah dengan // 10)
```

### Langkah 5: Simulasikan di Kertas

```
x = 1001

Langkah 1: reversed = 1, x = 100
Langkah 2: reversed = 10, x = 10
STOP! reversed (10) >= x (10)
x == reversed → 10 == 10 → TRUE ✅
```

```
x = 1234

Langkah 1: reversed = 4, x = 123
Langkah 2: reversed = 43, x = 12
STOP! reversed (43) >= x (12)
x == reversed? → 12 ≠ 43 → FALSE ❌
x == reversed // 10? → 12 ≠ 4 → FALSE ❌
```

### Langkah 6: Ringkasan Kerangka Berpikir

```
┌──────────────────────────────────────────────┐
│          PALINDROME NUMBER                    │
├──────────────────────────────────────────────┤
│                                              │
│  1. x < 0 → return False (negatif)          │
│  2. x > 0 dan x % 10 == 0 → return False   │
│     (berakhir 0 tapi bukan 0)               │
│                                              │
│  3. Balik setengah angka:                    │
│     reversed_half = 0                        │
│     while x > reversed_half:                 │
│         reversed_half = reversed_half*10     │
│                       + x % 10              │
│         x = x // 10                          │
│                                              │
│  4. Bandingkan:                              │
│     x == reversed_half (genap digit)         │
│     ATAU                                     │
│     x == reversed_half // 10 (ganjil digit)  │
│                                              │
└──────────────────────────────────────────────┘
```

---

## 🔍 Analisis & Cara Berpikir

### Pendekatan 1: Konversi ke String ⭐ (Paling Simpel)
> "Kalau boleh pakai string, kenapa tidak?"

**Ide:** Konversi angka jadi string, lalu bandingkan dengan string terbalik.

```python
def isPalindrome(self, x: int) -> bool:
    s = str(x)
    return s == s[::-1]
```

| Aspek | Analisis |
|-------|---------|
| **Time** | O(n) — n = jumlah digit |
| **Space** | O(n) — membuat string baru |
| **Pro** | Sangat simpel, 1 baris |
| **Con** | Menggunakan extra memory untuk string |

---

### Pendekatan 2: Balik Seluruh Angka (Math)
> "Balik seluruh angka, lalu bandingkan"

**Ide:** Balik seluruh angka menggunakan operasi modulo dan pembagian.

```python
def isPalindrome(self, x: int) -> bool:
    # Bilangan negatif dan bilangan berakhir 0 (kecuali 0) bukan palindrome
    if x < 0 or (x > 0 and x % 10 == 0):
        return False
    
    original = x
    reversed_num = 0
    
    while x > 0:
        digit = x % 10          # Ambil digit terakhir
        reversed_num = reversed_num * 10 + digit  # Tambahkan ke reversed
        x = x // 10             # Hapus digit terakhir
    
    return original == reversed_num
```

| Aspek | Analisis |
|-------|---------|
| **Time** | O(n) — n = jumlah digit |
| **Space** | O(1) — hanya variabel biasa |
| **Pro** | Tanpa extra memory |
| **Con** | Potensi integer overflow (di bahasa lain, Python aman) |

---

### Pendekatan 3: Balik Setengah Angka ⭐⭐ (Optimal)
> "Kenapa harus balik semua? Cukup setengah saja!"

**Ide:** Hanya balik **setengah bagian belakang** angka, lalu bandingkan dengan setengah depan.
Ini menghindari masalah overflow dan lebih efisien.

```python
def isPalindrome(self, x: int) -> bool:
    # Edge cases
    # Negatif → bukan palindrome
    # Berakhir 0 (tapi bukan 0 sendiri) → bukan palindrome
    if x < 0 or (x > 0 and x % 10 == 0):
        return False
    
    reversed_half = 0
    
    # Balik setengah angka
    while x > reversed_half:
        reversed_half = reversed_half * 10 + x % 10
        x = x // 10
    
    # Genap digit: x == reversed_half
    # Ganjil digit: x == reversed_half // 10 (buang digit tengah)
    return x == reversed_half or x == reversed_half // 10
```

**Trace untuk x = 12321:**
```
Iterasi 1: reversed_half = 1,   x = 1232  (1232 > 1 → lanjut)
Iterasi 2: reversed_half = 12,  x = 123   (123 > 12 → lanjut)
Iterasi 3: reversed_half = 123, x = 12    (12 > 123? TIDAK → stop)

Cek: x == reversed_half // 10 → 12 == 123 // 10 → 12 == 12 → TRUE ✅
```

| Aspek | Analisis |
|-------|---------|
| **Time** | O(n/2) → O(n) — hanya proses setengah digit |
| **Space** | O(1) — tidak ada alokasi tambahan |
| **Pro** | Paling efisien, tanpa overflow risk |
| **Con** | Logika sedikit lebih rumit |

---

## 📊 Perbandingan Semua Pendekatan

| Pendekatan | Time | Space | Difficulty | Rekomendasi |
|-----------|------|-------|------------|-------------|
| String Conversion | O(n) | O(n) | ⭐ | Untuk interview cepat |
| Full Reverse | O(n) | O(1) | ⭐⭐ | Baik untuk latihan |
| **Half Reverse** | **O(n/2)** | **O(1)** | ⭐⭐ | **Optimal — impress interviewer** |

---

## 📚 Konsep yang Dipelajari

### 1. Operasi Modulo (%) dan Floor Division (//)
```python
x = 12321

x % 10   # → 1 (digit terakhir)
x // 10  # → 1232 (hapus digit terakhir)
```

Ini adalah **dua operasi fundamental** untuk mengekstrak digit dari angka:
- `% 10` = ambil digit paling kanan
- `// 10` = buang digit paling kanan

### 2. Membangun Angka dari Digit
```python
reversed = 0
reversed = reversed * 10 + digit  # "Geser kiri dan tambah"
```
Ini pattern untuk **membangun angka digit per digit** — sering muncul di soal Math.

### 3. Edge Case Handling
Selalu pikirkan kasus spesial **sebelum menulis solusi**:
- Bilangan negatif
- Nol
- Bilangan yang berakhir dengan 0
- Bilangan satu digit

### 4. Optimasi: Proses Setengah
> "Kalau kita hanya perlu membandingkan dua bagian, kenapa harus memproses seluruhnya?"

Ini pola berpikir yang **sering berguna** di soal lain — selalu tanya: *"Bisa tidak saya berhenti lebih awal?"*

---

## ✍️ Latihan Mandiri

### Instruksi
1. **Tutup file ini** atau jangan lihat kode solusi
2. Buka [LeetCode #9](https://leetcode.com/problems/palindrome-number/)
3. Coba kerjakan sendiri dengan urutan:
   - Pertama: gunakan pendekatan **string** (paling gampang)
   - Kedua: gunakan pendekatan **full reverse** tanpa string
   - Ketiga: gunakan pendekatan **half reverse** (optimal)
4. **Target waktu:** 10-15 menit untuk semua pendekatan

### Test Cases untuk Verifikasi
```python
# Basic cases
assert isPalindrome(121) == True
assert isPalindrome(-121) == False
assert isPalindrome(10) == False

# Edge cases
assert isPalindrome(0) == True       # Single digit
assert isPalindrome(5) == True       # Single digit
assert isPalindrome(9) == True       # Single digit
assert isPalindrome(-1) == False     # Negatif

# Genap digit
assert isPalindrome(1221) == True
assert isPalindrome(1234) == False
assert isPalindrome(1001) == True

# Ganjil digit
assert isPalindrome(12321) == True
assert isPalindrome(12345) == False

# Berakhir 0
assert isPalindrome(100) == False
assert isPalindrome(10) == False
```

---

## ✅ Checklist Progress

- [ ] Baca dan pahami deskripsi soal
- [ ] Pahami kerangka berpikir
- [ ] Simulasikan di kertas (minimal 3 contoh)
- [ ] Kerjakan sendiri — Pendekatan String
- [ ] Kerjakan sendiri — Pendekatan Full Reverse
- [ ] Kerjakan sendiri — Pendekatan Half Reverse (optimal)
- [ ] Submit ke LeetCode dan Accepted ✅
- [ ] Review konsep yang dipelajari
- [ ] Kerjakan soal terkait (minimal 1)

---

## 🔗 Soal Terkait

| Soal | Difficulty | Pattern | Kenapa Terkait |
|------|-----------|---------|---------------|
| [7. Reverse Integer](https://leetcode.com/problems/reverse-integer/) | Medium | Math | Sama-sama membalik digit angka |
| [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) | Easy | Two Pointer | Palindrome tapi untuk string |
| [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) | Easy | Fast & Slow | Palindrome di Linked List |
| [680. Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/) | Easy | Two Pointer | Palindrome dengan 1 delete |

---

> 💡 **Takeaway:** Soal ini mengajarkan bahwa kadang **solusi yang paling sederhana** (string conversion) sudah cukup baik, tapi **memahami solusi yang lebih dalam** (half reverse) menunjukkan penguasaan yang lebih tinggi di interview.
