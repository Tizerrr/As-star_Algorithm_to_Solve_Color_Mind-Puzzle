# A* Algorithm to Solve Color Mind Puzzle


Implementasi algoritma **A\*** untuk menyelesaikan puzzle **Color Mind**, dibuat menggunakan **Python + NumPy**.

## 📌 Deskripsi Project

Color Mind adalah permainan puzzle berbasis pencampuran warna, di mana pemain harus menyusun blok-blok warna agar menghasilkan **susunan warna target**.

Setiap blok dapat:
- diletakkan di board
- diputar (rotasi 90°, 180°, 270°)
- digabungkan warnanya sesuai aturan permainan

Solver ini menggunakan **A\* Search Algorithm** untuk mencari urutan langkah terbaik menuju target.

---

## 🎯 Objective

Tujuan solver adalah mencari:

- **blok mana** yang harus digunakan
- **rotasi blok**
- **koordinat peletakan**
- **urutan langkah optimal**

agar board akhir sama dengan target.

---

## 🎨 Aturan Kombinasi Warna

Solver mengikuti aturan kombinasi warna Color Mind:

- `Y + B = G`
- `R + Y = O`
- `B + R = P`

Selain kombinasi di atas dianggap **tidak valid**.

---

## 🧠 Pendekatan A*

A\* digunakan dengan fungsi evaluasi:

```text
f(n) = g(n) + h(n)
````

### `g(n)` → Cost

Jumlah block yang sudah digunakan.

### `h(n)` → Heuristic Offset

Estimasi jarak board saat ini menuju target.

### Heuristic Scoring

Untuk setiap cell:

* `+2` → warna sama persis dengan target
* `+1` → warna merupakan warna dasar target
* `+0` → kosong atau salah total

Semakin kecil nilai offset, semakin dekat ke solusi.

---

## 🏗️ Struktur Class

### `Matrix`

Base class representasi matriks puzzle menggunakan `numpy.ndarray`.

### `InputMatrix`

Membaca input target atau block dari user.

### `Block`

Representasi block puzzle + seluruh kemungkinan rotasinya.

### `Game`

Berisi:

* aturan kombinasi warna
* validasi move
* simulasi peletakan block
* heuristic function

### `Node`

Representasi state untuk A*:

* board saat ini
* block yang sudah dipakai
* koordinat langkah
* heuristic value

### `GameSolver`

Core A* solver:

* generate initial state
* priority queue expansion
* eksplorasi state
* replay animasi solusi

---

## ⚙️ Requirements

Install dependency:

```bash
pip install numpy
```

Library bawaan Python yang digunakan:

* `queue`
* `time`
* `os`

---

## ▶️ Cara Menjalankan

Jalankan file notebook / script:

```bash
python HSP_232300333.py
```

atau jika menggunakan notebook:

```python
GameSolver()
```

---

## 📝 Format Input Target

Gunakan singkatan warna berikut:

| Kode | Warna  |
| ---- | ------ |
| Y    | Yellow |
| B    | Blue   |
| R    | Red    |
| G    | Green  |
| O    | Orange |
| P    | Purple |
| .    | Empty  |

Contoh target:

```text
G B B G
G B B G
Y . . Y
```

Kosongkan input untuk mengakhiri baris.

---

## 🧩 Format Input Block

Contoh block:

```text
Y B Y
```

atau block 2x2:

```text
B B
Y B
```

Program otomatis membuat seluruh kemungkinan **rotasi block**.

---

## 🧪 Contoh Test Case

Beberapa level sample tersedia pada file:

```text
HSP_test_cases.txt
```

Contoh **Level 1**:

```text
Target:
G B B G
G B B G
Y . . Y

Blocks:
Y B Y
Y Y Y
B B
Y B
B B
B B
```

---

## 🔍 Alur Algoritma

1. Input target matrix
2. Auto-generate board kosong
3. Input seluruh block
4. Generate rotasi block
5. Jalankan A*
6. Pilih node dengan heuristic terbaik
7. Expand semua move valid
8. Stop saat target tercapai
9. Tampilkan replay solusi

---

## 📈 Kompleksitas

Worst case dari pencarian:

```text
O(n^n * max(width,height)^2)
```

dengan:

* `n` = jumlah block yang mungkin digunakan
* faktor matriks berasal dari proses copy board tiap node

Walaupun worst case tinggi, heuristic A* secara signifikan lebih cepat dibanding BFS.

---

## 🎬 Output Solver

Jika solusi ditemukan, program menampilkan:

* jumlah trial
* execution time
* replay langkah demi langkah
* block yang digunakan
* posisi block

Contoh:

```text
Step 1: Put Block 3 Rotated Once to (1, 3)
Step 2: Put Block 1 Rotated Once to (1, 4)
...
```
