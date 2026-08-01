# 📖 Soft Skill: Membaca Dokumentasi

> *"Programmer yang jago bukan yang hafal semua syntax — tapi yang bisa CARI jawaban dengan cepat. Dan jawaban itu ada di dokumentasi."*

---

## Cerita Dulu: Kenapa Ini Penting?

Lo pernah gak lagi ngoding, terus bingung method apa yang harus dipake? Terus lo buka Google, ketik "javascript how to..." dan berakhir di StackOverflow? Itu works, tapi ada cara yang **lebih reliable dan lebih cepat**: baca dokumentasi resmi.

Senior developer yang lo kagumi? Mereka **baca docs setiap hari**. Gak ada yang hafal semua method. Yang penting lo tau **di mana carinya**.

---

## 🌐 Sumber Dokumentasi Utama

### 1. MDN Web Docs (Mozilla Developer Network)

**THE BIBLE untuk web developer.** Ini sumber paling lengkap dan akurat.

🔗 [developer.mozilla.org](https://developer.mozilla.org/en-US/)

Contoh: Lo mau tau gimana `.filter()` bekerja:
1. Buka MDN
2. Search "Array filter"
3. Baca: syntax, parameter, return value, contoh

### 2. W3Schools

Lebih simpel, cocok buat pemula. Tapi kurang detail dibanding MDN.

🔗 [w3schools.com](https://www.w3schools.com/js/)

### 3. JavaScript.info

Tutorial yang sangat detail dengan penjelasan step-by-step.

🔗 [javascript.info](https://javascript.info/)

---

## 🔍 Cara Baca Dokumentasi MDN

Kita ambil contoh: baca docs untuk `Array.prototype.map()`.

### 1. Syntax

```
Array.prototype.map(callbackFn)
Array.prototype.map(callbackFn, thisArg)
```

Ini ngasih tau: `.map()` nerima **satu parameter wajib** (callbackFn) dan **satu parameter opsional** (thisArg).

### 2. Parameters

```
callbackFn: Function yang dipanggil untuk setiap elemen.
  - element: Elemen array yang sedang diproses
  - index: Index elemen saat ini
  - array: Array yang dipanggil map
```

Ini ngasih tau: callback function lo dapet 3 parameter — elemen, index, dan array asli.

### 3. Return Value

```
A new array with each element being the result of the callback function.
```

Ini ngasih tau: `.map()` return **array baru**.

### 4. Examples

Di MDN selalu ada contoh kode yang bisa lo copy-paste dan coba sendiri.

---

## 🎯 Tips Baca Docs

### Tip 1: Fokus ke Syntax dan Examples Dulu

Jangan baca dari atas ke bawah. Langsung scroll ke **Syntax** dan **Examples**. Kalau masih bingung, baru baca penjelasan detailnya.

### Tip 2: Coba di Console

Baca docs itu HARUS sambil nyoba. Buka terminal atau browser console, terus ketik contoh-nya sendiri.

```js
// Baca di MDN bahwa String.repeat() mengulang string
// Langsung coba:
console.log("ha".repeat(3));  // "hahaha"
console.log("🔥".repeat(5)); // "🔥🔥🔥🔥🔥"
```

### Tip 3: Perhatiin Return Value

Ini PENTING. Setiap method punya return value yang beda:
- `.push()` return **panjang array baru** (bukan array-nya!)
- `.pop()` return **elemen yang dihapus**
- `.map()` return **array baru**
- `.forEach()` return **undefined**

```js
let arr = [1, 2, 3];

// Banyak yang salah paham:
let hasil = arr.push(4); // hasil = 4 (length!), BUKAN [1,2,3,4]
console.log(hasil); // 4

// Yang bener:
arr.push(4);
console.log(arr); // [1, 2, 3, 4]
```

### Tip 4: Cek "See Also" Section

Di bawah setiap halaman MDN, ada **See Also** — link ke method/topic yang berhubungan. Ini goldmine buat discover method baru!

### Tip 5: Bookmark Halaman yang Sering Dipakai

Bikin bookmark folder "JS Docs" dan simpen halaman yang sering lo buka:
- Array methods
- String methods
- Object methods
- Math object

---

## 📝 Cara Google yang Efektif

Kalau lo stuck dan mau cari di Google, ini template-nya:

```
javascript [apa yang mau lo lakuin]

Contoh:
- "javascript remove duplicate from array"
- "javascript check if object has property"
- "javascript convert string to number"
- "javascript sort array of objects by property"
```

### Prioritas Hasil Google

1. **MDN** — Paling reliable ✅
2. **StackOverflow** — Jawaban dari komunitas, cek yang paling banyak upvote
3. **JavaScript.info** — Tutorial detail
4. **Blog/Medium** — Kadang bagus, kadang outdated ⚠️

---

## 🧪 Latihan: Cari Sendiri!

Tanpa liat materi sebelumnya, cari di MDN dan jawab pertanyaan ini:

1. Apa return value dari `Array.prototype.splice()`?
2. Apa bedanya `String.slice()` sama `String.substring()`?
3. Gimana cara convert `"123"` (string) jadi `123` (number)?
4. Method apa yang bisa cek apakah suatu string **dimulai** dengan kata tertentu?
5. Apa itu `Array.prototype.find()` dan apa bedanya sama `filter()`?

**Jawabannya gak gue kasih di sini.** Lo harus buka MDN dan cari sendiri. Itu intinya skill ini. 💪

---

## 💡 Mindset

> "Gue gak hafal semua method JavaScript. Tapi gue tau cara carinya dalam 30 detik."

Ini mindset yang lo harus punya. Programming itu bukan soal hafalan — tapi soal **problem solving** + **kemampuan cari resource**.

Lo gak perlu malu buka docs. Lo gak perlu malu Google. **Semua developer melakukannya, setiap hari.**

---

## Sumber Tambahan

- 📖 [MDN Web Docs](https://developer.mozilla.org/en-US/)
- 📖 [JavaScript.info](https://javascript.info/)
- 📖 [DevDocs.io](https://devdocs.io/) — Semua docs dalam satu tempat
- 📖 [W3Schools](https://www.w3schools.com/js/)
