# 🌿 Git Branch — Kolaborasi Tanpa Konflik

> *"Bayangin lo lagi gambar di satu kertas bareng temen. Tanpa branch, lo berdua gambar di kertas yang SAMA — pasti nabrak. Dengan branch, masing-masing punya kertas sendiri, nanti digabungin."*

---

## Kenapa Branch Penting?

Sampai sekarang, lo udah push ke GitHub — tapi semua di branch `main` (atau `master`). Ini works kalau lo kerja sendiri, tapi begitu lo **kolaborasi** atau mau **coba fitur baru tanpa rusak kode utama**, lo butuh **branch**.

Branch itu kayak **timeline alternatif**. Lo bisa:
- Bikin fitur baru tanpa ganggu kode utama
- Eksperimen tanpa takut rusak
- Kerja bareng tim tanpa saling timpa

---

## Konsep Branch

```
main:     A --- B --- C --- D --- E
                        \
feature:                 F --- G --- H
```

- `main` = branch utama (production-ready code)
- `feature` = branch baru yang lo bikin buat develop fitur
- Setelah fitur selesai, lo **merge** branch `feature` ke `main`

---

## 🔧 Command Git Branch

### Lihat Branch yang Ada

```bash
# Lihat semua branch lokal
git branch

# Lihat semua branch (lokal + remote)
git branch -a
```

Output:
```
* main           ← bintang = branch yang aktif sekarang
  feature-login
  fix-bug-123
```

### Bikin Branch Baru

```bash
# Bikin branch baru (tapi BELUM pindah ke sana)
git branch nama-branch-baru

# Bikin branch baru DAN langsung pindah (PALING SERING DIPAKAI)
git checkout -b nama-branch-baru

# Cara modern (sama aja)
git switch -c nama-branch-baru
```

### Pindah Branch

```bash
# Pindah ke branch lain
git checkout nama-branch

# Cara modern
git switch nama-branch
```

### Hapus Branch

```bash
# Hapus branch lokal (yang udah di-merge)
git branch -d nama-branch

# Hapus branch lokal (paksa, meskipun belum di-merge)
git branch -D nama-branch
```

---

## 📝 Workflow Lengkap

### Step 1: Pastikan lo di Branch Main dan Up-to-date

```bash
git checkout main
git pull origin main
```

### Step 2: Bikin Branch Baru

```bash
git checkout -b feature-form-login
# Sekarang lo ada di branch "feature-form-login"
```

### Step 3: Kerjain Fitur, Commit Seperti Biasa

```bash
# Edit file...
git add .
git commit -m "tambah form login"

# Edit lagi...
git add .
git commit -m "tambah validasi email"
```

### Step 4: Push Branch ke GitHub

```bash
git push origin feature-form-login
```

### Step 5: Merge ke Main (Setelah Fitur Selesai)

```bash
# Pindah ke main dulu
git checkout main

# Pull update terbaru
git pull origin main

# Merge branch fitur ke main
git merge feature-form-login

# Push main yang udah di-merge
git push origin main
```

### Step 6: Hapus Branch yang Udah Di-merge

```bash
git branch -d feature-form-login
```

---

## ⚔️ Merge Conflict

Kadang, pas merge, Git bingung karena **file yang sama diedit di dua branch**. Ini namanya **merge conflict**.

```
<<<<<<< HEAD
let greeting = "Halo Dunia";    ← versi di branch main
=======
let greeting = "Hello World";   ← versi di branch feature
>>>>>>> feature-form-login
```

### Cara Resolve Conflict

1. Buka file yang conflict
2. Pilih versi yang mau lo keep (atau gabungin keduanya)
3. Hapus marker `<<<<<<<`, `=======`, `>>>>>>>`
4. Save, add, commit

```bash
# Setelah resolve conflict:
git add .
git commit -m "resolve merge conflict"
```

---

## 🏷️ Naming Convention

Branch name yang baik itu **deskriptif dan konsisten**:

```bash
# ✅ Good
feature-login-page
fix-bug-form-validation
improvement-performance

# ❌ Bad
branch1
test
asdfgh
coba-coba
```

---

## 📊 Visualisasi Git Flow

```
main:     A --- B --- C --------- M --- N
                \               /
feature:         D --- E --- F

A = initial commit
B-C = development di main
D-E-F = development fitur di branch terpisah
M = merge commit (gabungin feature ke main)
N = development lanjut di main
```

---

## Cheat Sheet

| Command | Fungsi |
|---------|--------|
| `git branch` | Lihat semua branch |
| `git branch nama` | Bikin branch baru |
| `git checkout -b nama` | Bikin + pindah ke branch baru |
| `git checkout nama` | Pindah ke branch |
| `git merge nama` | Merge branch ke branch aktif |
| `git branch -d nama` | Hapus branch |
| `git push origin nama` | Push branch ke remote |

---

## Latihan Mandiri

1. Bikin branch baru `latihan-branch`
2. Buat file `test.js` di branch itu, commit dan push
3. Pindah balik ke `main`
4. Merge `latihan-branch` ke `main`
5. Hapus branch `latihan-branch`

---

## Sumber Tambahan

- 📖 [Git Branch — Petani Kode](https://www.petanikode.com/git-branch/)
- 📖 [Git Branching — Atlassian](https://www.atlassian.com/git/tutorials/using-branches)
- 🎮 [Learn Git Branching (Interactive)](https://learngitbranching.js.org/)
