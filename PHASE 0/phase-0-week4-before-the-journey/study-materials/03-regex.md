# 🔎 Regex — Regular Expressions yang Powerful

> *"Regex itu kayak cheat code buat nyari pola di text. Mau cari semua email di 1000 baris? Regex solve itu dalam 1 baris kode."*

---

## Apa Itu Regex?

Regex (Regular Expressions) adalah **pola/pattern** yang dipakai buat mencari, mencocokkan, atau memanipulasi teks. Lo bisa bilang regex itu "Find & Replace on steroids".

Contoh simpel — cari semua kata "far" di paragraph:

```js
let paragraph = `far far away, behind the word mountains, far from the countries 
Vokalia and Consonantia, there live the blind texts!`;

console.log(paragraph.match(/far/g)); // ["far", "far", "far"]
// 3 kata "far" ditemukan!
```

---

## Cara Menulis Regex

Ada 2 cara:

```js
// Cara 1: Regex literal (PALING SERING DIPAKAI)
let regex1 = /abc/;

// Cara 2: RegExp constructor
let regex2 = new RegExp("abc");

// Dua-duanya sama aja, tapi literal lebih singkat
```

---

## 🧩 Simbol-Simbol Penting

Ini yang harus lo hafal. Gak banyak, tapi powerful banget.

### Karakter Dasar

| Simbol | Arti | Contoh |
|--------|------|--------|
| `.` | Karakter APA AJA (kecuali newline) | `/h.t/` match "hat", "hot", "hit" |
| `\d` | Digit (0-9) | `/\d\d/` match "42", "07" |
| `\w` | Word character (a-z, A-Z, 0-9, _) | `/\w+/` match "hello", "code_123" |
| `\s` | Whitespace (spasi, tab, newline) | `/\s/` match " " |
| `\D` | BUKAN digit | `/\D/` match "a", "!" |
| `\W` | BUKAN word character | `/\W/` match "!", " " |
| `\S` | BUKAN whitespace | `/\S/` match "a", "1" |

### Quantifier (Berapa Kali)

| Simbol | Arti | Contoh |
|--------|------|--------|
| `*` | 0 atau lebih | `/go*/` match "g", "go", "gooo" |
| `+` | 1 atau lebih | `/go+/` match "go", "gooo" (bukan "g") |
| `?` | 0 atau 1 (opsional) | `/colou?r/` match "color" dan "colour" |
| `{n}` | Tepat n kali | `/\d{3}/` match "123" |
| `{n,m}` | Antara n sampai m kali | `/\d{2,4}/` match "12", "123", "1234" |

### Anchor (Posisi)

| Simbol | Arti | Contoh |
|--------|------|--------|
| `^` | Awal string | `/^Hello/` match "Hello World" tapi bukan "Say Hello" |
| `$` | Akhir string | `/World$/` match "Hello World" tapi bukan "World Cup" |

### Character Class

| Simbol | Arti | Contoh |
|--------|------|--------|
| `[abc]` | Salah satu dari a, b, atau c | `/[aeiou]/` match huruf vokal |
| `[a-z]` | Range a sampai z | `/[a-zA-Z]/` match huruf apa aja |
| `[^abc]` | BUKAN a, b, atau c | `/[^0-9]/` match bukan angka |

### Flag

| Flag | Arti |
|------|------|
| `g` | Global — cari SEMUA kemunculan |
| `i` | Case insensitive — gak peduli besar/kecil |
| `m` | Multiline — ^ dan $ berlaku per baris |

```js
// Tanpa flag g — cuma cari yang pertama
console.log("hello hello".match(/hello/));  // ["hello"] (cuma 1)

// Dengan flag g — cari semua
console.log("hello hello".match(/hello/g)); // ["hello", "hello"] (2)

// Dengan flag i — case insensitive
console.log("Hello HELLO".match(/hello/gi)); // ["Hello", "HELLO"]
```

---

## 🛠️ Method yang Pakai Regex

### `.test()` — Return true/false

```js
let email = "andi@gmail.com";
let pattern = /\w+@\w+\.\w+/;

console.log(pattern.test(email));           // true
console.log(pattern.test("bukan-email"));   // false
```

### `.match()` — Return array hasil match

```js
let str = "Saya punya 3 kucing dan 2 anjing";

// Cari semua angka
console.log(str.match(/\d+/g)); // ["3", "2"]

// Cari semua kata
console.log(str.match(/\w+/g)); 
// ["Saya", "punya", "3", "kucing", "dan", "2", "anjing"]
```

### `.replace()` — Ganti yang cocok

```js
let str = "Regex itu sangat susah!";
let result = str.replace(/susah/, "mudah");
console.log(result); // "Regex itu sangat mudah!"

// Replace semua (pakai flag g)
let str2 = "ha ha ha";
console.log(str2.replace(/ha/g, "hi")); // "hi hi hi"
```

### `.split()` — Pecah string berdasarkan pattern

```js
let csv = "Andi,Budi,Cici,Dodi";
console.log(csv.split(/,/)); // ["Andi", "Budi", "Cici", "Dodi"]

let str = "belajar   regex    itu   seru";
console.log(str.split(/\s+/)); // ["belajar", "regex", "itu", "seru"]
// \s+ = satu atau lebih spasi
```

---

## 📝 Contoh Praktis

### Validasi Nomor HP Indonesia

```js
function validasiHP(nomor) {
  // Mulai 08, diikuti 9-12 digit
  let pattern = /^08\d{9,12}$/;
  return pattern.test(nomor);
}

console.log(validasiHP("081234567890")); // true
console.log(validasiHP("0812345"));      // false (terlalu pendek)
console.log(validasiHP("12345678901"));  // false (gak mulai 08)
```

### Cari dan Hapus Simbol/Punctuation

```js
let kalimat = "Wah! Regex itu @keren #banget, bro!!!";
let bersih = kalimat.match(/[a-zA-Z]+/gi);
console.log(bersih); // ["Wah", "Regex", "itu", "keren", "banget", "bro"]
```

### Extract Angka dari String

```js
let str = "Harga: Rp 150.000 diskon 20% jadi Rp 120.000";
let angka = str.match(/\d+/g);
console.log(angka); // ["150", "000", "20", "120", "000"]
```

### Censor Kata

```js
let chat = "Anjing lo bego banget sih tolol";
let censored = chat.replace(/anjing|bego|tolol/gi, "***");
console.log(censored); // "*** lo *** banget sih ***"
```

---

## ⚠️ Hati-Hati: `.match()` Return null

Kalau pattern gak ketemu, `.match()` return **null** (bukan array kosong!).

```js
let str = "tidak ada angka di sini";
let result = str.match(/\d+/g);
console.log(result); // null

// ❌ Error kalau langsung akses .length
// console.log(result.length); // TypeError!

// ✅ Cek dulu
if (result) {
  console.log("Ditemukan " + result.length + " angka");
} else {
  console.log("Gak ada angka");
}
```

Analogi: Array kosong = gelas tanpa air. Null = **gak ada gelas sama sekali**.

---

## Latihan Mandiri

1. Bikin regex yang match email valid (format: xxx@xxx.xxx)
2. Bikin fungsi yang hitung berapa kali huruf vokal muncul di string
3. Bikin fungsi `censorBadWords(str, badWords)` yang ganti kata-kata di array `badWords` jadi "***"
4. Bikin regex yang validasi password: minimal 8 karakter, ada huruf besar, huruf kecil, dan angka

---

## Sumber Tambahan

- 🎮 [RegExr — Latihan Regex Interactive](https://regexr.com)
- 📖 [MDN Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
- 🎮 [Regex101 — Test & Debug](https://regex101.com)
