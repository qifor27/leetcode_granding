# 🔢 Two Sum — LeetCode #1

> **Difficulty:** Easy | **Pattern:** Hash Map | **Link:** [LeetCode](https://leetcode.com/problems/two-sum/)

---

## 📋 Deskripsi Soal

Diberikan array integer `nums` dan integer `target`, kembalikan **indeks dari dua angka** yang jika dijumlahkan hasilnya sama dengan `target`.

- Setiap input **pasti punya tepat satu solusi**
- Kamu **tidak boleh menggunakan elemen yang sama dua kali**
- Jawaban bisa dalam urutan apapun

### Contoh

```
Input:  nums = [2, 7, 11, 15], target = 9
Output: [0, 1]
Penjelasan: nums[0] + nums[1] = 2 + 7 = 9
```

```
Input:  nums = [3, 2, 4], target = 6
Output: [1, 2]
Penjelasan: nums[1] + nums[2] = 2 + 4 = 6
```

```
Input:  nums = [3, 3], target = 6
Output: [0, 1]
```

### Constraints
- `2 <= nums.length <= 10⁴`
- `-10⁹ <= nums[i] <= 10⁹`
- `-10⁹ <= target <= 10⁹`
- **Hanya ada satu jawaban yang valid**

---

## 🧠 Analisis & Cara Berpikir

### ❌ Pendekatan 1: Brute Force (Jangan Dipakai)

**Ide:** Cek semua pasangan angka.

```python
# ⚠️ Ini cara yang BURUK — hanya untuk memahami masalah
def twoSum(nums, target):
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] + nums[j] == target:
                return [i, j]
```

| Aspek | Nilai |
|-------|-------|
| Time Complexity | O(n²) — dua loop bersarang |
| Space Complexity | O(1) — tidak pakai memori tambahan |

**Kenapa buruk?** Kalau `nums` punya 10.000 elemen, kamu perlu ~50 juta operasi. Terlalu lambat!

---

### ✅ Pendekatan 2: Hash Map (Optimal)

**Ide Kunci:** Untuk setiap angka `num`, kita tahu pasangannya harus `target - num`. Kita bisa simpan angka yang sudah dilihat di **hash map** supaya bisa cek dalam O(1).

#### Alur Berpikir Step-by-Step

```
nums = [2, 7, 11, 15], target = 9

Langkah 1: num = 2
  → complement = 9 - 2 = 7
  → Apakah 7 ada di hash map? ❌ (hash map kosong)
  → Simpan: {2: 0}

Langkah 2: num = 7
  → complement = 9 - 7 = 2
  → Apakah 2 ada di hash map? ✅ (index 0!)
  → Return [0, 1] ✅
```

#### Kode Solusi

```python
def twoSum(nums, target):
    seen = {}  # hash map: nilai → index
    
    for i, num in enumerate(nums):
        complement = target - num
        
        if complement in seen:
            return [seen[complement], i]
        
        seen[num] = i
```

| Aspek | Nilai |
|-------|-------|
| Time Complexity | **O(n)** — satu kali loop |
| Space Complexity | **O(n)** — hash map menyimpan hingga n elemen |

---

## 🔑 Konsep yang Dipelajari

### 1. Hash Map (Dictionary)
Hash map menyimpan pasangan **key-value** dan memungkinkan lookup dalam **O(1)**.

```python
# Membuat hash map
d = {}

# Menyimpan nilai
d[key] = value

# Mengecek keberadaan key
if key in d:    # O(1) — sangat cepat!
    print(d[key])
```

### 2. Complement Pattern
Ini adalah pattern yang **sangat sering muncul** di soal-soal LeetCode:

> Daripada mencari dua elemen yang memenuhi kondisi, **hitung apa yang kamu butuhkan** dan cek apakah sudah pernah dilihat.

```
target = a + b
→ b = target - a   ← ini "complement"
```

### 3. Trade-off: Time vs Space
- Brute force: lambat (O(n²)) tapi hemat memori (O(1))
- Hash map: cepat (O(n)) tapi pakai memori lebih (O(n))

> 💡 Di dunia nyata dan interview, **kecepatan biasanya lebih penting** daripada memori.

---

## 🏋️ Latihan Mandiri

Sebelum melihat solusi, coba kerjakan sendiri:

1. **Buka** [Two Sum di LeetCode](https://leetcode.com/problems/two-sum/)
2. **Pilih** Python3
3. **Coba** brute force dulu, pastikan paham masalahnya
4. **Optimasi** ke hash map
5. **Submit** dan pastikan accepted

### Test Cases untuk Dicoba

```python
# Case 1: Normal
nums = [2, 7, 11, 15], target = 9  # → [0, 1]

# Case 2: Jawaban di tengah
nums = [3, 2, 4], target = 6       # → [1, 2]

# Case 3: Angka duplikat
nums = [3, 3], target = 6          # → [0, 1]

# Case 4: Angka negatif
nums = [-1, -2, -3, -4, -5], target = -8  # → [2, 4]
```

---

## 📌 Checklist

- [ ] Memahami masalah Two Sum
- [ ] Memahami kenapa brute force O(n²)
- [ ] Memahami cara kerja hash map
- [ ] Memahami complement pattern
- [ ] Submit solusi hash map di LeetCode
- [ ] Solusi diterima (Accepted) ✅

---

## 🔗 Soal Terkait (Setelah Two Sum)

| Soal | Konsep Baru |
|------|-------------|
| [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) | Two Pointer (array sudah sorted) |
| [15. 3Sum](https://leetcode.com/problems/3sum/) | Extend Two Sum ke 3 elemen |
| [1. Two Sum](https://leetcode.com/problems/two-sum/) variations | Hash Map pattern |

---

## ✍️ Solusi Saya

```python
class Solution(object):
    def twoSum(self, nums, target):
        num_map = {}
        for i, num in enumerate(nums):
            complement = target - num
            if complement in num_map:
                return [num_map[complement], i]
            num_map[num] = i
```

### Penjelasan Baris per Baris

| Baris | Kode | Penjelasan |
|-------|------|------------|
| 1 | `num_map = {}` | Membuat **hash map kosong** untuk menyimpan `{angka: index}` |
| 2 | `for i, num in enumerate(nums):` | Loop array — `i` = index, `num` = nilai elemen |
| 3 | `complement = target - num` | Hitung **pasangan yang dibutuhkan** (`target - num`) |
| 4 | `if complement in num_map:` | Cek apakah complement **sudah pernah dilihat** (O(1) lookup) |
| 5 | `return [num_map[complement], i]` | **Ketemu!** Kembalikan index complement dan index saat ini |
| 6 | `num_map[num] = i` | Belum ketemu → simpan angka sekarang untuk iterasi berikutnya |

### 🔍 Simulasi Detail

---

#### Contoh 1: `nums = [2, 7, 11, 15], target = 9`

**Iterasi 1** — `i = 0`, `num = 2`
```
num_map sebelum: {}

complement = 9 - 2 = 7
Apakah 7 ada di num_map?  ❌ Tidak ada

→ Simpan num ke map: num_map[2] = 0

num_map sesudah: {2: 0}
```

**Iterasi 2** — `i = 1`, `num = 7`
```
num_map sebelum: {2: 0}

complement = 9 - 7 = 2
Apakah 2 ada di num_map?  ✅ ADA! (index = 0)

→ Return [num_map[2], 1] = [0, 1] 🎯
```

> **Hasil: `[0, 1]`** — nums[0] + nums[1] = 2 + 7 = 9 ✅

---

#### Contoh 2: `nums = [3, 2, 4], target = 6`

**Iterasi 1** — `i = 0`, `num = 3`
```
num_map sebelum: {}

complement = 6 - 3 = 3
Apakah 3 ada di num_map?  ❌ Tidak ada

→ Simpan: num_map[3] = 0

num_map sesudah: {3: 0}
```

**Iterasi 2** — `i = 1`, `num = 2`
```
num_map sebelum: {3: 0}

complement = 6 - 2 = 4
Apakah 4 ada di num_map?  ❌ Tidak ada

→ Simpan: num_map[2] = 1

num_map sesudah: {3: 0, 2: 1}
```

**Iterasi 3** — `i = 2`, `num = 4`
```
num_map sebelum: {3: 0, 2: 1}

complement = 6 - 4 = 2
Apakah 2 ada di num_map?  ✅ ADA! (index = 1)

→ Return [num_map[2], 2] = [1, 2] 🎯
```

> **Hasil: `[1, 2]`** — nums[1] + nums[2] = 2 + 4 = 6 ✅

---

#### Contoh 3: `nums = [3, 3], target = 6` (kasus angka duplikat)

**Iterasi 1** — `i = 0`, `num = 3`
```
num_map sebelum: {}

complement = 6 - 3 = 3
Apakah 3 ada di num_map?  ❌ Tidak ada (map masih kosong!)

→ Simpan: num_map[3] = 0

num_map sesudah: {3: 0}
```

**Iterasi 2** — `i = 1`, `num = 3`
```
num_map sebelum: {3: 0}

complement = 6 - 3 = 3
Apakah 3 ada di num_map?  ✅ ADA! (index = 0)

→ Return [num_map[3], 1] = [0, 1] 🎯
```

> **Hasil: `[0, 1]`** — nums[0] + nums[1] = 3 + 3 = 6 ✅
>
> 💡 **Kenapa ini berhasil?** Karena kita **cek dulu baru simpan**. Jadi angka yang sama tidak menimpa dirinya sendiri. Urutan `if → simpan` sangat penting!

### Kompleksitas

| | Nilai |
|---|---|
| **Time** | **O(n)** — satu kali loop |
| **Space** | **O(n)** — hash map menyimpan max n elemen |

> ✅ **Verdict:** Solusi ini sudah **100% optimal** — persis yang diharapkan di interview!

---

> 💡 **Ingat:** Two Sum bukan hanya soal pertama di LeetCode — pattern **"complement + hash map"** muncul di banyak soal lain. Kuasai ini dan kamu punya fondasi kuat!
