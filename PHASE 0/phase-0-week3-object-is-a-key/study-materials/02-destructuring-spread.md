# 🎁 Destructuring & Spread Operator

> *"Destructuring itu kayak bongkar kado — lo tau isinya apa aja, tinggal ambil yang lo mau langsung."*

---

## Kenapa Belajar Ini?

Lo udah bisa akses property pakai `obj.nama` atau `obj["nama"]`. Tapi kalau lo butuh banyak property sekaligus, kode-nya jadi repetitif:

```js
let siswa = { nama: "Andi", umur: 20, kota: "Jakarta", ipk: 3.75 };

// ❌ Repetitif banget
let nama = siswa.nama;
let umur = siswa.umur;
let kota = siswa.kota;
let ipk = siswa.ipk;
```

Destructuring bikin ini jadi **satu baris**:

```js
let siswa = { nama: "Andi", umur: 20, kota: "Jakarta", ipk: 3.8 };

// ✅ Clean!
let { nama, umur, kota, ipk } = siswa;
console.log(nama); // "Andi"
console.log(ipk);  // 3.75
```

---

## 🔓 Object Destructuring

### Basic Destructuring

```js
let makanan = {
  nama: "Nasi Goreng",
  harga: 25000,
  pedas: true
};

// "Bongkar" object, ambil property-nya langsung
let { nama, harga, pedas } = makanan;

console.log(nama);  // "Nasi Goreng"
console.log(harga); // 25000
console.log(pedas); // true
```

### Rename Saat Destructuring

Kadang nama property gak cocok sama yang lo mau. Bisa di-rename!

```js
let user = { name: "Andi", age: 20 };

// Rename: name jadi namaSiswa, age jadi umurSiswa
let { name: namaSiswa, age: umurSiswa } = user;

console.log(namaSiswa);  // "Andi"
console.log(umurSiswa);  // 20
// console.log(name);    // ❌ Error! yang ada itu namaSiswa
```

### Default Value

Kalau property gak ada, lo bisa kasih default value biar gak `undefined`.

```js
let config = { theme: "dark" };

let { theme, language = "id" } = config;
// theme ada di object → "dark"
// language GAK ada di object → pakai default "id"

console.log(theme);    // "dark"
console.log(language); // "id"
```

### Ambil Sebagian Aja

Gak harus ambil semua property — ambil yang lo butuh aja.

```js
let siswa = { nama: "Andi", umur: 20, kota: "Jakarta", ipk: 3.75 };

let { nama, ipk } = siswa; // cuma ambil 2
console.log(nama); // "Andi"
console.log(ipk);  // 3.75
```

---

## 📦 Array Destructuring

Bukan cuma object — array juga bisa di-destructure!

```js
let buah = ["apel", "mangga", "jeruk"];

// Destructure berdasarkan POSISI (bukan nama)
let [pertama, kedua, ketiga] = buah;

console.log(pertama); // "apel"
console.log(kedua);   // "mangga"
console.log(ketiga);  // "jeruk"
```

### Skip Elemen

```js
let angka = [1, 2, 3, 4, 5];

// Skip elemen ke-2 dan ke-4 pakai koma kosong
let [a, , c, , e] = angka;

console.log(a); // 1
console.log(c); // 3
console.log(e); // 5
```

### Swap Variabel (Trick Keren!)

```js
let x = 10;
let y = 20;

// Tanpa destructuring — butuh variabel temp
// let temp = x; x = y; y = temp;

// Dengan destructuring — satu baris!
[x, y] = [y, x];

console.log(x); // 20
console.log(y); // 10
```

---

## 🌊 Spread Operator (`...`)

Spread operator itu tiga titik `...` yang bisa "nyebarin" elemen array atau property object.

Analogi: Lo punya kotak LEGO. Spread itu kayak lo **tumpahkan semua LEGO-nya ke lantai** — dari satu wadah jadi terpisah-pisah.

### Spread di Array

```js
let depan = [1, 2, 3];
let belakang = [4, 5, 6];

// Gabungin array (alternatif .concat())
let gabungan = [...depan, ...belakang];
console.log(gabungan); // [1, 2, 3, 4, 5, 6]

// Sisipkan di tengah
let sisipan = [0, ...depan, 3.5, ...belakang, 7];
console.log(sisipan); // [0, 1, 2, 3, 3.5, 4, 5, 6, 7]

// Copy array (shallow copy)
let original = [1, 2, 3];
let copy = [...original];
copy.push(4);
console.log(original); // [1, 2, 3] — gak berubah!
console.log(copy);     // [1, 2, 3, 4]
```

### Spread di Object

```js
let defaultConfig = { theme: "light", lang: "en", fontSize: 14 };

// Copy object
let myConfig = { ...defaultConfig };
console.log(myConfig); // { theme: "light", lang: "en", fontSize: 14 }

// Copy + override beberapa property
let customConfig = { ...defaultConfig, theme: "dark", lang: "id" };
console.log(customConfig); // { theme: "dark", lang: "id", fontSize: 14 }

// Merge dua object
let biodata = { nama: "Andi", umur: 20 };
let akademik = { jurusan: "IF", ipk: 3.75 };
let lengkap = { ...biodata, ...akademik };
console.log(lengkap);
// { nama: "Andi", umur: 20, jurusan: "IF", ipk: 3.75 }
```

---

## 🧲 Rest Operator (`...`)

Syntax-nya sama kayak spread (`...`), tapi fungsinya **kebalikan** — mengumpulkan sisa elemen jadi satu.

Analogi: Spread = tumpahkan LEGO. Rest = **kumpulin sisa LEGO yang belum diambil**.

### Rest di Destructuring

```js
let angka = [1, 2, 3, 4, 5];

let [pertama, kedua, ...sisanya] = angka;
console.log(pertama); // 1
console.log(kedua);   // 2
console.log(sisanya);  // [3, 4, 5] — sisa dikumpulin!

// Object juga bisa!
let siswa = { nama: "Andi", umur: 20, kota: "Jakarta", ipk: 3.75 };

let { nama, ...lainnya } = siswa;
console.log(nama);     // "Andi"
console.log(lainnya);  // { umur: 20, kota: "Jakarta", ipk: 3.75 }
```

### Rest di Function Parameter

```js
// Terima berapa pun argument
function jumlahkan(...angka) {
  let total = 0;
  for (let num of angka) {
    total += num;
  }
  return total;
}

console.log(jumlahkan(1, 2, 3));       // 6
console.log(jumlahkan(10, 20, 30, 40)); // 100
```

---

## Spread vs Rest: Apa Bedanya?

```js
// SPREAD: "nyebar" dari satu ke banyak (di KANAN =)
let arr = [1, 2, 3];
let newArr = [...arr, 4, 5]; // spread arr jadi elemen-elemen terpisah

// REST: "ngumpulin" dari banyak ke satu (di KIRI =)
let [first, ...rest] = [1, 2, 3, 4, 5]; // kumpulin sisanya ke rest
```

| | Spread | Rest |
|---|--------|------|
| Posisi | Di kanan `=` atau di argument | Di kiri `=` atau di parameter |
| Fungsi | Nyebar elemen | Kumpulin sisa |
| Contoh | `[...arr]` | `let [...rest] = arr` |

---

## Latihan Mandiri

1. Destructure object `{ x: 10, y: 20, z: 30 }` dan ambil cuma `x` dan `z`
2. Pakai spread buat merge `{ a: 1, b: 2 }` dan `{ b: 3, c: 4 }` — apa nilai `b`?
3. Bikin fungsi `ambilPertama(arr)` yang return `{ first, rest }` pakai destructuring
4. Swap dua variabel tanpa variabel temporary

---

## Sumber Tambahan

- 📖 [MDN Destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- 📖 [MDN Spread Syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
