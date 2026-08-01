# 🎯 Callback & Higher-Order Functions

> *"Lo pernah pesen GoFood? Lo kasih INSTRUKSI ke driver: 'beliin nasi goreng di warung X'. Lo gak masak sendiri — lo kasih tugas ke orang lain. Itu callback."*

---

## Kenapa Belajar Ini?

Ini jembatan ke Phase 1. Di Phase 1, lo bakal ketemu callback di mana-mana — event handler, asynchronous programming, API calls. Kalau lo gak paham callback sekarang, Phase 1 bakal kerasa 10x lebih berat.

Fun fact: lo **udah pakai callback** tanpa sadar! `.forEach()`, `.map()`, `.filter()`, `.reduce()` — function yang lo pass ke dalamnya itu **callback function**.

```js
// Lo udah pakai callback ini selama Week 2!
let angka = [1, 2, 3, 4, 5];
angka.forEach(function(num) {  // ← INI callback function
  console.log(num);
});
```

---

## Apa Itu Callback?

**Callback = function yang dikirim sebagai ARGUMENT ke function lain.**

Lo gak langsung panggil function-nya — lo "titip" function itu ke function lain, dan biar function lain yang panggil di waktu yang tepat.

```js
// Function biasa
function spikeSkill() {
  console.log("Makan! 🍕");
}

// Function yang nerima callback
function lakukanSetelah3Detik(callback) {
  console.log("Nunggu 3 detik...");
  // Simulasi nunggu (di real-world pakai setTimeout)
  callback(); // panggil function yang dititipin
}

// Kirim function "spikeSkill" sebagai argument
lakukanSetelah3Detik(spikeSkill);
// "Nunggu 3 detik..."
// "Makan! 🍕"
```

### Kenapa Bisa Kirim Function Sebagai Argument?

Karena di JavaScript, **function itu first-class citizen** — artinya function bisa:
1. Disimpen di variabel
2. Dikirim sebagai argument
3. Di-return dari function lain

```js
// 1. Simpen function di variabel
let spikeSkill = function() { console.log("Hello!"); };

// 2. Kirim function sebagai argument
function jalankan(fn) {
  fn(); // panggil function yang dikirim
}
jalankan(spikeSkill); // "Hello!"

// 3. Return function dari function lain
function bikinGreeting(nama) {
  return function() {
    console.log("Halo, " + nama + "!");
  };
}
let greetAndi = bikinGreeting("Andi");
greetAndi(); // "Halo, Andi!"
```

---

## Apa Itu Higher-Order Function (HOF)?

**Higher-Order Function = function yang MENERIMA function sebagai parameter, ATAU me-return function.**

```js
// Ini Higher-Order Function — nerima callback
function ulangi(kali, aksi) {
  for (let i = 0; i < kali; i++) {
    aksi(i); // panggil callback, kirim index
  }
}

ulangi(3, function(i) {
  console.log("Iterasi ke-" + i);
});
// Iterasi ke-0
// Iterasi ke-1
// Iterasi ke-2
```

**Array methods yang udah lo kenal = Higher-Order Functions!**

```js
let angka = [1, 2, 3, 4, 5];

// .map() = Higher-Order Function
// function(n) { return n * 2 } = Callback
let doubled = angka.map(function(n) { return n * 2; });
```

---

## Bikin Higher-Order Function Sendiri

### Contoh 1: Custom forEach

```js
function myForEach(arr, callback) {
  for (let i = 0; i < arr.length; i++) {
    callback(arr[i], i, arr); // kirim elemen, index, dan array
  }
}

let buah = ["apel", "mangga", "jeruk"];
myForEach(buah, function(item, index) {
  console.log(index + ": " + item);
});
// 0: apel
// 1: mangga
// 2: jeruk
```

### Contoh 2: Custom map

```js
function myMap(arr, callback) {
  let result = [];
  for (let i = 0; i < arr.length; i++) {
    result.push(callback(arr[i], i));
  }
  return result;
}

let angka = [1, 2, 3, 4, 5];
let kuadrat = myMap(angka, function(n) {
  return n * n;
});
console.log(kuadrat); // [1, 4, 9, 16, 25]
```

### Contoh 3: Custom filter

```js
function myFilter(arr, callback) {
  let result = [];
  for (let i = 0; i < arr.length; i++) {
    if (callback(arr[i], i)) {  // kalau callback return true, masukin
      result.push(arr[i]);
    }
  }
  return result;
}

let angka = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let genap = myFilter(angka, function(n) {
  return n % 2 === 0;
});
console.log(genap); // [2, 4, 6, 8, 10]
```

---

## Callback dengan Logika Berbeda

Power dari callback: **satu function, bisa dipake buat banyak hal** tergantung callback yang lo kirim.

```js
function prosesArray(arr, callback) {
  let result = [];
  for (let i = 0; i < arr.length; i++) {
    result.push(callback(arr[i]));
  }
  return result;
}

let angka = [1, 2, 3, 4, 5];

// Callback 1: kaliin 2
let doubled = prosesArray(angka, function(n) { return n * 2; });
console.log(doubled); // [2, 4, 6, 8, 10]

// Callback 2: kuadrat
let squared = prosesArray(angka, function(n) { return n * n; });
console.log(squared); // [1, 4, 9, 16, 25]

// Callback 3: jadiin string
let strings = prosesArray(angka, function(n) { return "Angka: " + n; });
console.log(strings); // ["Angka: 1", "Angka: 2", ...]

// SATU function prosesArray, TIGA kegunaan berbeda. Itu power-nya callback!
```

---

## Function yang Return Function

```js
function kaliDengan(pengali) {
  return function(angka) {
    return angka * pengali;
  };
}

let kaliDua = kaliDengan(2);   // return function yang kaliin 2
let kaliTiga = kaliDengan(3);  // return function yang kaliin 3

console.log(kaliDua(5));   // 10
console.log(kaliTiga(5));  // 15

// Bisa langsung dipakai tanpa variabel
console.log(kaliDengan(10)(7)); // 70
```

---

## Kenapa Ini Penting buat Phase 1?

Di Phase 1, lo bakal ketemu pattern kayak gini setiap hari:

```js
// Event handler (callback!)
button.addEventListener("click", function() {
  console.log("Button diklik!");
});

// Fetch API (callback!)
fetch("https://api.example.com/data")
  .then(function(response) {
    return response.json();
  })
  .then(function(data) {
    console.log(data);
  });

// setTimeout (callback!)
setTimeout(function() {
  console.log("3 detik udah lewat!");
}, 3000);
```

Semua itu pakai **callback pattern**. Kalau lo paham sekarang, Phase 1 bakal smooth.

---

## Latihan Mandiri

1. Bikin `myReduce(arr, callback, initialValue)` yang kerja kayak `.reduce()`
2. Bikin function `operasi(a, b, callback)` yang nerima 2 angka dan callback. Test dengan callback tambah, kurang, kali, bagi
3. Bikin function `bikinGreeter(spikeSkill)` yang return function greeting. Contoh: `bikinGreeter("Halo")("Andi")` → "Halo, Andi!"
4. Bikin `compose(fn1, fn2)` yang return function baru: `compose(double, addOne)(5)` → `double(addOne(5))` → 12

---

## Sumber Tambahan

- 📖 [MDN Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
- 📹 [Callback Functions Explained](https://youtu.be/cNjIUSDnb9k)
- 📖 [JavaScript.info — Function Expressions](https://javascript.info/function-expressions)
