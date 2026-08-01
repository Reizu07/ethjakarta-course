# 🏗️ Nested Object & Complex Data

> *"Data di dunia nyata itu gak pernah flat. Profile Instagram lo aja ada nama, bio, followers (array), posts (array of objects) — berlapis-lapis."*

---

## Kenapa Nested Object Penting?

Sampai sejauh ini, lo udah belajar object sederhana. Tapi di real-world, data itu **kompleks dan berlapis**. API yang lo hit nanti (di Phase 1+) bakal return data kayak gini:

```js
let user = {
  id: 1,
  username: "andikoding",
  profile: {
    nama: "Andi Wijaya",
    bio: "Belajar coding di ETHJKT 🚀",
    avatar: "https://cdn.ethjkt.dev/andi.jpg"
  },
  stats: {
    followers: 150,
    following: 89,
    posts: 42
  },
  recentPosts: [
    { id: 101, caption: "Hello World!", likes: 25 },
    { id: 102, caption: "Belajar JavaScript", likes: 42 }
  ]
};
```

Lo HARUS bisa navigate data kayak gini.

---

## Akses Nested Object

Pakai **chain dot notation** atau **chain bracket notation**.

```js
let siswa = {
  nama: "Andi",
  alamat: {
    jalan: "Jl. Sudirman No. 10",
    kota: "Jakarta",
    provinsi: "DKI Jakarta",
    kodePos: "10110"
  },
  nilai: {
    matematika: 85,
    bahasa: 90,
    ipa: 78
  }
};

// Akses nested property
console.log(siswa.alamat.kota);        // "Jakarta"
console.log(siswa.nilai.matematika);   // 85
console.log(siswa.alamat.kodePos);     // "10110"

// Bracket notation juga bisa
console.log(siswa["alamat"]["jalan"]); // "Jl. Sudirman No. 10"

// Mix dot dan bracket
let subject = "ipa";
console.log(siswa.nilai[subject]);     // 78 — dynamic key!
```

---

## Ubah Nested Property

```js
let config = {
  app: {
    name: "MyApp",
    version: "1.0.0"
  },
  database: {
    host: "localhost",
    port: 5432
  }
};

// Ubah nested value
config.app.version = "2.0.0";
config.database.host = "db.ethjkt.dev";

console.log(config.app.version);    // "2.0.0"
console.log(config.database.host);  // "db.ethjkt.dev"

// Tambah nested property baru
config.app.author = "ETHJKT";
console.log(config.app.author);     // "ETHJKT"
```

---

## Array of Objects (PALING SERING DIPAKAI!)

Ini pattern yang bakal lo temuin **setiap hari** sebagai developer.

```js
let students = [
  { nama: "Andi", umur: 20, nilai: 85, kota: "Jakarta" },
  { nama: "Budi", umur: 22, nilai: 72, kota: "Bandung" },
  { nama: "Cici", umur: 21, nilai: 95, kota: "Jakarta" },
  { nama: "Dodi", umur: 23, nilai: 60, kota: "Surabaya" },
  { nama: "Eka",  umur: 20, nilai: 88, kota: "Jakarta" }
];
```

### Loop dan Akses

```js
let students = [
  { nama: "Andi", umur: 20, nilai: 85, kota: "Jakarta" },
  { nama: "Budi", umur: 22, nilai: 72, kota: "Bandung" },
  { nama: "Cici", umur: 21, nilai: 95, kota: "Jakarta" },
  { nama: "Dodi", umur: 23, nilai: 60, kota: "Surabaya" },
  { nama: "Eka",  umur: 20, nilai: 88, kota: "Jakarta" }
];

// Cetak semua nama dan nilai
for (let i = 0; i < students.length; i++) {
  console.log(students[i].nama + ": " + students[i].nilai);
}

// Atau pakai forEach (lebih clean)
students.forEach(function(s) {
  console.log(s.nama + ": " + s.nilai);
});
```

### Filter Array of Objects

```js
let students = [
  { nama: "Andi", umur: 20, nilai: 85, kota: "Jakarta" },
  { nama: "Budi", umur: 22, nilai: 72, kota: "Bandung" },
  { nama: "Cici", umur: 21, nilai: 95, kota: "Jakarta" },
  { nama: "Dodi", umur: 23, nilai: 60, kota: "Surabaya" },
  { nama: "Eka",  umur: 20, nilai: 88, kota: "Jakarta" }
];

// Cari siswa dari Jakarta yang nilainya > 80
let jakartaPintar = students.filter(function(s) {
  return s.kota === "Jakarta" && s.nilai > 80;
});

console.log(jakartaPintar);
// [
//   { nama: "Andi", umur: 20, nilai: 85, kota: "Jakarta" },
//   { nama: "Cici", umur: 21, nilai: 95, kota: "Jakarta" },
//   { nama: "Eka",  umur: 20, nilai: 88, kota: "Jakarta" }
// ]
```

### Map Array of Objects

```js
let students = [
  { nama: "Andi", umur: 20, nilai: 85, kota: "Jakarta" },
  { nama: "Budi", umur: 22, nilai: 72, kota: "Bandung" },
  { nama: "Cici", umur: 21, nilai: 95, kota: "Jakarta" },
  { nama: "Dodi", umur: 23, nilai: 60, kota: "Surabaya" },
  { nama: "Eka",  umur: 20, nilai: 88, kota: "Jakarta" }
];

// Ambil nama aja
let namaSiswa = students.map(function(s) {
  return s.nama;
});
console.log(namaSiswa); // ["Andi", "Budi", "Cici", "Dodi", "Eka"]

// Bikin format baru
let rapor = students.map(function(s) {
  return {
    nama: s.nama,
    status: s.nilai >= 75 ? "LULUS" : "REMEDIAL"
  };
});
console.log(rapor);
// [
//   { nama: "Andi", status: "LULUS" },
//   { nama: "Budi", status: "REMEDIAL" },
//   ...
// ]
```

### Reduce Array of Objects

```js
let students = [
  { nama: "Andi", umur: 20, nilai: 85, kota: "Jakarta" },
  { nama: "Budi", umur: 22, nilai: 72, kota: "Bandung" },
  { nama: "Cici", umur: 21, nilai: 95, kota: "Jakarta" },
  { nama: "Dodi", umur: 23, nilai: 60, kota: "Surabaya" },
  { nama: "Eka",  umur: 20, nilai: 88, kota: "Jakarta" }
];

// Hitung rata-rata nilai
let totalNilai = students.reduce(function(total, s) {
  return total + s.nilai;
}, 0);
let rataRata = totalNilai / students.length;
console.log("Rata-rata: " + rataRata); // 80

// Kelompokkan siswa per kota
let perKota = students.reduce(function(acc, s) {
  if (!acc[s.kota]) {
    acc[s.kota] = []; // bikin array baru kalau belum ada
  }
  acc[s.kota].push(s.nama);
  return acc;
}, {});

console.log(perKota);
// {
//   Jakarta: ["Andi", "Cici", "Eka"],
//   Bandung: ["Budi"],
//   Surabaya: ["Dodi"]
// }
```

---

## Object di Dalam Array di Dalam Object 🤯

Ya, ini bisa berlapis-lapis. Tetep tenang, akses-nya tinggal chain aja.

```js
let sekolah = {
  nama: "SMA ETHJKT",
  kelas: [
    {
      nama: "XII-A",
      waliKelas: "Pak Budi",
      siswa: [
        { nama: "Andi", nilai: 85 },
        { nama: "Cici", nilai: 92 }
      ]
    },
    {
      nama: "XII-B",
      waliKelas: "Bu Sari",
      siswa: [
        { nama: "Dodi", nilai: 78 },
        { nama: "Eka", nilai: 88 }
      ]
    }
  ]
};

// Akses nama siswa pertama di kelas pertama
console.log(sekolah.kelas[0].siswa[0].nama); // "Andi"

// Akses wali kelas XII-B
console.log(sekolah.kelas[1].waliKelas); // "Bu Sari"

// Loop semua siswa di semua kelas
for (let i = 0; i < sekolah.kelas.length; i++) {
  let kelas = sekolah.kelas[i];
  console.log("=== " + kelas.nama + " ===");
  
  for (let j = 0; j < kelas.siswa.length; j++) {
    let s = kelas.siswa[j];
    console.log("  " + s.nama + ": " + s.nilai);
  }
}
```

---

## ⚠️ Hati-Hati: Undefined Chain

Kalau lo akses nested property yang gak ada, lo dapet error!

```js
let user = { nama: "Andi" };

// ❌ Error!
// console.log(user.alamat.kota);
// TypeError: Cannot read properties of undefined (reading 'kota')

// ✅ Cek dulu
if (user.alamat) {
  console.log(user.alamat.kota);
} else {
  console.log("Alamat belum diisi");
}

// ✅ Optional chaining (modern JS)
console.log(user.alamat?.kota); // undefined (gak error!)
```

---

## Konversi: Array ↔ Object

### Array 2D → Object

```js
let data = [["nama", "Andi"], ["umur", 20], ["kota", "Jakarta"]];
let obj = {};

for (let i = 0; i < data.length; i++) {
  let key = data[i][0];
  let value = data[i][1];
  obj[key] = value;
}

console.log(obj); // { nama: "Andi", umur: 20, kota: "Jakarta" }

// Atau pakai Object.fromEntries (lebih singkat)
let obj2 = Object.fromEntries(data);
```

### Array of Arrays → Array of Objects

```js
let raw = [
  ["Andi", 85],
  ["Budi", 92],
  ["Cici", 78]
];

let result = raw.map(function(item) {
  return {
    nama: item[0],
    nilai: item[1]
  };
});

console.log(result);
// [{ nama: "Andi", nilai: 85 }, { nama: "Budi", nilai: 92 }, ...]
```

---

## Latihan Mandiri

1. Dari data `sekolah` di atas, cari siswa dengan nilai tertinggi di semua kelas
2. Bikin fungsi `countByCity(students)` yang return object `{ "Jakarta": 3, "Bandung": 1, ... }`
3. Akses data berlapis: bikin object `toko` dengan property `departemen` (array of objects), setiap departemen punya `produk` (array of objects). Cetak semua produk di semua departemen.

---

## Sumber Tambahan

- 📖 [MDN Working with Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)
- 📖 [Optional Chaining (?.) MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)
