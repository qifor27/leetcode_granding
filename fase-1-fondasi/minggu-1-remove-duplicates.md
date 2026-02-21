# 🔢 Remove Duplicates from Sorted Array — LeetCode #26

> **Difficulty:** Easy | **Pattern:** Two Pointer | **Link:** [LeetCode](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

---

## 📋 Deskripsi Soal

Diberikan array integer `nums` yang sudah **diurutkan secara ascending** (non-decreasing). Hapus semua duplikat **secara in-place** sehingga setiap elemen unik muncul **tepat satu kali**. Kembalikan jumlah elemen unik `k`.

### Aturan Penting
- Kamu harus memodifikasi array **di tempat (in-place)** — tidak boleh membuat array baru
- `k` elemen pertama dari `nums` harus berisi elemen-elemen unik sesuai urutan aslinya
- Elemen setelah `k` **tidak penting** (bisa apa saja)
- Kembalikan `k` (jumlah elemen unik)

### Contoh

```
Input:  nums = [1, 1, 2]
Output: k = 2, nums = [1, 2, _]

Penjelasan: Fungsi mengembalikan k = 2.
Dua elemen pertama nums adalah [1, 2].
Underscore (_) artinya tidak penting nilainya apa.
```

```
Input:  nums = [0, 0, 1, 1, 1, 2, 2, 3, 3, 4]
Output: k = 5, nums = [0, 1, 2, 3, 4, _, _, _, _, _]

Penjelasan: Fungsi mengembalikan k = 5.
Lima elemen pertama nums adalah [0, 1, 2, 3, 4].
```

### Constraints
- `1 <= nums.length <= 3 × 10⁴`
- `-100 <= nums[i] <= 100`
- `nums` sudah diurutkan secara **non-decreasing** (ascending)

---

## 🎓 Kerangka Berpikir — Seperti Dosen Mendiktekan

> Bayangkan kamu baru pertama kali melihat soal ini. Begini cara kamu **harus** berpikir, langkah demi langkah:

### Langkah 1: Baca Soal — Tangkap Kata Kunci 🔍

Baca soal pelan-pelan. Garis bawahi kata-kata penting:

- **"sorted array"** → ⚡ Array sudah terurut! Ini BESAR. Artinya duplikat pasti **bersebelahan**
- **"in-place"** → ❌ Tidak boleh buat array baru. Harus modifikasi array yang ada
- **"return k"** → Kita harus kembalikan **jumlah** elemen unik, bukan array baru
- **"elemen setelah k tidak penting"** → Kita tidak perlu menghapus sisa elemen, cukup **taruh elemen unik di depan**

> 🗣️ *"Oke, jadi saya tidak menghapus apa-apa. Saya hanya perlu **menyusun ulang** elemen unik ke bagian depan array."*

### Langkah 2: Visualisasikan dengan Contoh Kecil ✏️

Ambil kertas. Tulis contoh sederhana:

```
nums = [1, 1, 2, 3, 3]

Yang saya mau:   [1, 2, 3, _, _]  → return k = 3
```

> 🗣️ *"Saya perlu 'menyapu' array dari kiri ke kanan. Setiap kali saya ketemu angka yang BARU (belum pernah muncul), saya taruh di depan."*

### Langkah 3: Pikirkan — Butuh Berapa Pointer? 🤔

Tanya ke diri sendiri: **"Saya perlu melacak apa saja?"**

1. **Posisi tulis** → dimana saya harus menaruh elemen unik berikutnya (ini **slow pointer**)
2. **Posisi baca** → elemen mana yang sedang saya periksa sekarang (ini **fast pointer**)

> 🗣️ *"Aha! Saya butuh DUA pointer. Satu untuk membaca, satu untuk menulis. Ini namanya pattern **Two Pointer**!"*

### Langkah 4: Tentukan Aturan Pergerakan Pointer 📏

Tanya: **"Kapan slow pointer bergerak, kapan diam?"**

- **Fast pointer** → SELALU maju 1 langkah setiap iterasi (dia menjelajahi semua elemen)
- **Slow pointer** → hanya maju **kalau fast pointer menemukan elemen BARU** yang berbeda dari elemen di posisi slow

```
Aturan sederhana:
  JIKA nums[fast] ≠ nums[slow] → pindahkan slow maju, tulis nilai baru
  JIKA nums[fast] = nums[slow] → skip, fast maju terus
```

> 🗣️ *"Jadi slow pointer itu seperti 'penjaga gerbang'. Dia hanya membuka pintu untuk elemen yang benar-benar baru."*

### Langkah 5: Simulasikan di Kertas — JANGAN LANGSUNG KODING! 📝

```
nums = [1, 1, 2, 3, 3]
        s  f              → nums[f]=1 == nums[s]=1 → skip
        s     f           → nums[f]=2 != nums[s]=1 → s maju! nums[1]=2
           s     f        → nums[f]=3 != nums[s]=2 → s maju! nums[2]=3
              s     f     → nums[f]=3 == nums[s]=3 → skip

Hasil: [1, 2, 3, 3, 3]  →  k = s+1 = 3 ✅
        -------
        bagian ini yang penting
```

> 🗣️ *"Bagus! Simulasi saya cocok dengan jawaban yang diinginkan. Sekarang saya yakin logika saya benar. Baru sekarang boleh mulai ngoding."*

### Langkah 6: Tulis Kode — Terjemahkan Logika ke Python 💻

```python
def removeDuplicates(nums):
    k = 0                              # slow pointer, mulai di index 0
    for i in range(1, len(nums)):      # fast pointer, mulai di index 1
        if nums[i] != nums[k]:        # elemen baru?
            k += 1                     # geser slow pointer
            nums[k] = nums[i]          # tulis elemen baru
    return k + 1                       # jumlah elemen unik
```

### Langkah 7: Verifikasi — Cek Edge Cases 🧪

Sebelum submit, tanyakan:

| Pertanyaan | Jawaban |
|------------|---------|
| Bagaimana kalau array cuma 1 elemen? | `k=0`, loop tidak jalan, return `1` ✅ |
| Bagaimana kalau semua elemen sama? | fast selalu skip, `k` tidak pernah naik, return `1` ✅ |
| Bagaimana kalau tidak ada duplikat? | Setiap elemen baru, `k` naik terus, return `len(nums)` ✅ |

> 🗣️ *"Semua edge case tercakup. Sekarang baru boleh submit!"*

### 📌 Ringkasan Kerangka Berpikir

```
┌─────────────────────────────────────────────────┐
│  1. Baca soal → tangkap kata kunci              │
│  2. Visualisasikan dengan contoh kecil          │
│  3. Tentukan berapa pointer yang dibutuhkan     │
│  4. Tentukan aturan pergerakan setiap pointer   │
│  5. Simulasikan di kertas (JANGAN LANGSUNG KOD) │
│  6. Baru tulis kode                             │
│  7. Verifikasi dengan edge cases                │
└─────────────────────────────────────────────────┘
```

> 💡 **Ingat:** Kerangka berpikir ini berlaku untuk SEMUA soal Two Pointer, bukan hanya soal ini!

---

## 🧠 Analisis & Cara Berpikir

### Kenapa Soal Ini Penting?

Soal ini mengajarkan **Two Pointer pattern** — salah satu teknik paling sering muncul di interview. Idenya: gunakan dua pointer untuk membandingkan dan memanipulasi array tanpa memori tambahan.

### ❌ Pendekatan 1: Menggunakan Set (Tidak Sesuai Aturan)

**Ide:** Masukkan semua elemen ke set, lalu tulis kembali ke array.

```python
# ⚠️ Ini TIDAK memenuhi syarat in-place karena pakai memori tambahan O(n)
def removeDuplicates(nums):
    unique = sorted(set(nums))
    for i in range(len(unique)):
        nums[i] = unique[i]
    return len(unique)
```

| Aspek | Nilai |
|-------|-------|
| Time Complexity | O(n log n) — karena sorting |
| Space Complexity | O(n) — set menyimpan semua elemen unik |

**Kenapa tidak ideal?** Soal meminta solusi **in-place** dengan memori tambahan O(1). Menggunakan set melanggar batasan ini.

---

### ✅ Pendekatan 2: Two Pointer (Optimal)

**Ide Kunci:** Karena array sudah **sorted**, semua duplikat pasti **bersebelahan**. Kita gunakan dua pointer:
- **Slow pointer (`k`)** — menandai posisi terakhir elemen unik
- **Fast pointer (`i`)** — menjelajahi seluruh array

Setiap kali fast pointer menemukan elemen yang **berbeda** dari elemen di posisi slow, kita pindahkan elemen tersebut ke posisi slow+1.

#### Alur Berpikir Step-by-Step

```
nums = [0, 0, 1, 1, 1, 2, 2, 3, 3, 4]
        k              → slow pointer (posisi elemen unik terakhir)
           i           → fast pointer (penjelajah)

Langkah 1: k=0, i=1 → nums[1]=0 == nums[0]=0 → DUPLIKAT, skip
Langkah 2: k=0, i=2 → nums[2]=1 != nums[0]=0 → BARU! k=1, nums[1]=1
Langkah 3: k=1, i=3 → nums[3]=1 == nums[1]=1 → DUPLIKAT, skip
Langkah 4: k=1, i=4 → nums[4]=1 == nums[1]=1 → DUPLIKAT, skip
Langkah 5: k=2, i=5 → nums[5]=2 != nums[1]=1 → BARU! k=2, nums[2]=2
Langkah 6: k=2, i=6 → nums[6]=2 == nums[2]=2 → DUPLIKAT, skip
Langkah 7: k=3, i=7 → nums[7]=3 != nums[2]=2 → BARU! k=3, nums[3]=3
Langkah 8: k=3, i=8 → nums[8]=3 == nums[3]=3 → DUPLIKAT, skip
Langkah 9: k=4, i=9 → nums[9]=4 != nums[3]=3 → BARU! k=4, nums[4]=4

Hasil: k+1 = 5, nums = [0, 1, 2, 3, 4, ...]
```

#### Kode Solusi

```python
def removeDuplicates(nums):
    if not nums:
        return 0
    
    k = 0  # slow pointer — posisi elemen unik terakhir
    
    for i in range(1, len(nums)):  # fast pointer mulai dari index 1
        if nums[i] != nums[k]:    # elemen baru ditemukan!
            k += 1                # geser slow pointer
            nums[k] = nums[i]     # tulis elemen baru
    
    return k + 1  # jumlah elemen unik = index terakhir + 1
```

| Aspek | Nilai |
|-------|-------|
| Time Complexity | **O(n)** — satu kali loop |
| Space Complexity | **O(1)** — hanya pakai dua variabel pointer |

---

## 🔑 Konsep yang Dipelajari

### 1. Two Pointer Pattern
Two pointer adalah teknik menggunakan dua index pointer untuk memproses array secara efisien.

```
Variasi Two Pointer:
1. Slow & Fast  → soal ini! Satu lambat, satu cepat
2. Left & Right → bergerak dari kedua ujung ke tengah
3. Two Arrays   → masing-masing pointer di array berbeda
```

> 💡 **Kapan pakai Two Pointer?** Ketika array sudah sorted DAN kamu perlu memproses elemen secara in-place.

### 2. In-Place Modification
Mengubah array **tanpa membuat array baru**. Ini hemat memori (O(1) space) dan sering diminta di soal interview.

```python
# ❌ BUKAN in-place (membuat array baru)
result = [x for x in nums if ...]

# ✅ In-place (modifikasi langsung)
nums[k] = nums[i]
```

### 3. Sorted Array Advantage
Ketika array sudah sorted, kamu mendapat keuntungan besar:
- Elemen duplikat **selalu bersebelahan**
- Bisa menggunakan **binary search** (O(log n))
- Bisa menggunakan **two pointer** secara efektif

> 💡 Selalu tanyakan: **"Apakah input sudah sorted?"** — ini bisa mengubah pendekatan secara drastis!

---

## 🏋️ Latihan Mandiri

Sebelum melihat solusi, coba kerjakan sendiri:

1. **Buka** [Remove Duplicates from Sorted Array di LeetCode](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
2. **Pilih** Python3
3. **Gambar** dua pointer di kertas, simulasikan dengan contoh kecil
4. **Tulis** kode — pikirkan kapan slow pointer bergerak
5. **Submit** dan pastikan accepted

### Test Cases untuk Dicoba

```python
# Case 1: Array kecil dengan duplikat
nums = [1, 1, 2]                          # → k=2, nums=[1, 2, ...]

# Case 2: Banyak duplikat
nums = [0, 0, 1, 1, 1, 2, 2, 3, 3, 4]   # → k=5, nums=[0, 1, 2, 3, 4, ...]

# Case 3: Tidak ada duplikat
nums = [1, 2, 3, 4, 5]                    # → k=5, nums=[1, 2, 3, 4, 5]

# Case 4: Semua sama
nums = [1, 1, 1, 1]                       # → k=1, nums=[1, ...]

# Case 5: Satu elemen
nums = [42]                               # → k=1, nums=[42]
```

---

## 📌 Checklist

- [ ] Memahami masalah Remove Duplicates from Sorted Array
- [ ] Memahami kenapa array sorted membuat masalah lebih mudah
- [ ] Memahami cara kerja two pointer (slow & fast)
- [ ] Memahami in-place modification
- [ ] Submit solusi two pointer di LeetCode
- [ ] Solusi diterima (Accepted) ✅

---

## 🔗 Soal Terkait

| Soal | Konsep Baru |
|------|-------------|
| [27. Remove Element](https://leetcode.com/problems/remove-element/) | Two Pointer — hapus elemen tertentu (bukan duplikat) |
| [80. Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/) | Variasi: boleh max 2 duplikat |
| [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/) | Two Pointer — pindahkan semua 0 ke akhir |

---

## ✍️ Solusi Saya

```python
class Solution(object):
    def removeDuplicates(self, nums):
        k = 0  # slow pointer — posisi elemen unik terakhir
        
        for i in range(1, len(nums)):  # fast pointer
            if nums[i] != nums[k]:    # elemen baru yang belum ada
                k += 1                # majukan slow pointer
                nums[k] = nums[i]     # tulis elemen baru di posisi k
        
        return k + 1  # jumlah elemen unik
```

### Penjelasan Baris per Baris

| Baris | Kode | Penjelasan |
|-------|------|------------|
| 1 | `k = 0` | Inisialisasi **slow pointer** di index 0 (elemen pertama pasti unik) |
| 2 | `for i in range(1, len(nums)):` | **Fast pointer** mulai dari index 1, jelajahi seluruh array |
| 3 | `if nums[i] != nums[k]:` | Bandingkan elemen fast dengan elemen unik terakhir di slow |
| 4 | `k += 1` | Elemen baru ditemukan → geser slow pointer ke depan |
| 5 | `nums[k] = nums[i]` | Tulis elemen baru ke posisi slow pointer |
| 6 | `return k + 1` | Kembalikan jumlah elemen unik (index terakhir + 1) |

### 🔍 Simulasi Detail

---

#### Contoh 1: `nums = [1, 1, 2]`

**Iterasi 1** — `i = 1`, `num = 1`
```
k = 0
nums = [1, 1, 2]
        k  i

nums[1] = 1 == nums[0] = 1 → DUPLIKAT, skip

k tetap 0
```

**Iterasi 2** — `i = 2`, `num = 2`
```
k = 0
nums = [1, 1, 2]
        k     i

nums[2] = 2 != nums[0] = 1 → ELEMEN BARU!

k = 0 + 1 = 1
nums[1] = nums[2] = 2

nums = [1, 2, 2]
           k  i
```

> **Hasil: `k + 1 = 2`** — nums[:2] = [1, 2] ✅

---

#### Contoh 2: `nums = [0, 0, 1, 1, 1, 2, 2, 3, 3, 4]`

| Step | i | nums[i] | nums[k] | Sama? | Aksi | k | Array (k elemen pertama) |
|------|---|---------|---------|-------|------|---|--------------------------|
| 1 | 1 | 0 | 0 | ✅ | Skip | 0 | [0] |
| 2 | 2 | 1 | 0 | ❌ | k=1, tulis | 1 | [0, 1] |
| 3 | 3 | 1 | 1 | ✅ | Skip | 1 | [0, 1] |
| 4 | 4 | 1 | 1 | ✅ | Skip | 1 | [0, 1] |
| 5 | 5 | 2 | 1 | ❌ | k=2, tulis | 2 | [0, 1, 2] |
| 6 | 6 | 2 | 2 | ✅ | Skip | 2 | [0, 1, 2] |
| 7 | 7 | 3 | 2 | ❌ | k=3, tulis | 3 | [0, 1, 2, 3] |
| 8 | 8 | 3 | 3 | ✅ | Skip | 3 | [0, 1, 2, 3] |
| 9 | 9 | 4 | 3 | ❌ | k=4, tulis | 4 | [0, 1, 2, 3, 4] |

> **Hasil: `k + 1 = 5`** — nums[:5] = [0, 1, 2, 3, 4] ✅

### Kompleksitas

| | Nilai |
|---|---|
| **Time** | **O(n)** — satu kali loop, setiap elemen diproses tepat sekali |
| **Space** | **O(1)** — hanya pakai variabel `k` dan `i` |

> ✅ **Verdict:** Solusi ini sudah **100% optimal** — tidak bisa lebih cepat dari O(n) karena harus melihat setiap elemen minimal sekali!

---

> 💡 **Ingat:** Pattern **slow & fast pointer** di sorted array ini akan muncul lagi di soal #27 (Remove Element) dan #283 (Move Zeroes). Kuasai pattern ini sekarang!
