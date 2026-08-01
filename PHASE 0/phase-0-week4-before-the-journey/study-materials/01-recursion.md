# 🔄 Recursion — Function yang Manggil Dirinya Sendiri

> *"Lo pernah liat efek cermin di depan cermin? Bayangan di dalam bayangan, di dalam bayangan... Itu recursion."*

---

## Cerita Dulu: Kenapa Recursion?

Lo udah jago looping. `for`, `while`, semua bisa. Tapi ada beberapa masalah yang **lebih natural diselesaikan dengan recursion** — function yang manggil dirinya sendiri.

Bayangin lo lagi buka matryoshka (boneka Rusia yang isinya boneka lagi). Lo buka boneka pertama → di dalamnya ada boneka lagi → buka lagi → ada lagi → sampe akhirnya ketemu boneka terkecil yang gak bisa dibuka lagi. **Itu recursion.**

---

## Apa Itu Recursion?

Recursion = **fungsi yang memanggil dirinya sendiri**, dengan **kondisi berhenti** (base case).

```js
function hitung(n) {
  // BASE CASE: kondisi berhenti
  if (n === 0) {
    console.log("Selesai!");
    return;
  }

  // RECURSIVE CASE: manggil diri sendiri
  console.log(n);
  hitung(n - 1); // panggil hitung lagi, tapi n berkurang
}

hitung(5);
// 5
// 4
// 3
// 2
// 1
// Selesai!
```

### 2 Komponen Wajib Recursion

1. **Base Case** — kapan berhenti? (WAJIB ADA! Kalau gak, infinite loop!)
2. **Recursive Case** — panggil diri sendiri dengan parameter yang BERUBAH

```js
// ❌ TANPA base case = infinite recursion = CRASH!
function forever(n) {
  console.log(n);
  forever(n); // n gak berubah, gak pernah berhenti!
}
// RangeError: Maximum call stack size exceeded 💥
```

---

## Contoh Klasik: Penjumlahan 1 Sampai N

```js
// Hitung 1 + 2 + 3 + ... + n
function jumlah(n) {
  if (n === 1) return 1;           // base case: kalau n=1, return 1
  return n + jumlah(n - 1);        // recursive: n + jumlah sisanya
}

console.log(jumlah(5)); // 15
// Kenapa 15? → 5 + 4 + 3 + 2 + 1 = 15
```

### Bedah Step by Step

```
jumlah(5) = 5 + jumlah(4)
                jumlah(4) = 4 + jumlah(3)
                                jumlah(3) = 3 + jumlah(2)
                                                jumlah(2) = 2 + jumlah(1)
                                                                jumlah(1) = 1  ← BASE CASE!

Balik ke atas:
jumlah(2) = 2 + 1 = 3
jumlah(3) = 3 + 3 = 6
jumlah(4) = 4 + 6 = 10
jumlah(5) = 5 + 10 = 15 ✅
```

---

## Contoh: Factorial (n!)

Factorial: `5! = 5 × 4 × 3 × 2 × 1 = 120`

```js
function factorial(n) {
  if (n === 0 || n === 1) return 1;  // base case: 0! = 1, 1! = 1
  return n * factorial(n - 1);        // n * factorial sisanya
}

console.log(factorial(5)); // 120
console.log(factorial(0)); // 1
console.log(factorial(1)); // 1
```

### Perbandingan: Loop vs Recursion

```js
// Factorial pakai LOOP
function factorialLoop(n) {
  let result = 1;
  for (let i = 1; i <= n; i++) {
    result *= i;
  }
  return result;
}

// Factorial pakai RECURSION
function factorialRec(n) {
  if (n <= 1) return 1;
  return n * factorialRec(n - 1);
}

// Dua-duanya hasilnya sama!
console.log(factorialLoop(5)); // 120
console.log(factorialRec(5));  // 120
```

Recursion lebih **elegan dan singkat**, tapi loop lebih **hemat memory**.

---

## Contoh: Perpangkatan (Power)

```js
// Hitung base^exponent tanpa pakai **
function power(base, exponent) {
  if (exponent === 0) return 1;  // base case: apapun^0 = 1
  return base * power(base, exponent - 1);
}

console.log(power(2, 3)); // 8  (2 × 2 × 2)
console.log(power(3, 4)); // 81 (3 × 3 × 3 × 3)
console.log(power(5, 0)); // 1
```

### Visualisasi

```
power(2, 3) = 2 × power(2, 2)
                  = 2 × power(2, 1)
                        = 2 × power(2, 0)
                              = 1          ← BASE CASE

Balik: 2 × 1 = 2
       2 × 2 = 4
       2 × 4 = 8 ✅
```

---

## Contoh: Fibonacci

Deret Fibonacci: 0, 1, 1, 2, 3, 5, 8, 13, 21, ...
Setiap angka = jumlah 2 angka sebelumnya.

```js
function fibonacci(n) {
  if (n === 0) return 0;      // base case 1
  if (n === 1) return 1;      // base case 2
  return fibonacci(n - 1) + fibonacci(n - 2); // jumlah 2 sebelumnya
}

console.log(fibonacci(0)); // 0
console.log(fibonacci(1)); // 1
console.log(fibonacci(6)); // 8
console.log(fibonacci(10)); // 55
```

---

## Contoh: Reverse String

```js
function reverseString(str) {
  if (str.length <= 1) return str;  // base case: string 1 huruf atau kosong
  return reverseString(str.slice(1)) + str[0]; // sisa + huruf pertama di belakang
}

console.log(reverseString("hello")); // "olleh"
console.log(reverseString("ETHJKT")); // "TKJHTE"
```

### Bedah

```
reverseString("hello")
= reverseString("ello") + "h"
= (reverseString("llo") + "e") + "h"
= ((reverseString("lo") + "l") + "e") + "h"
= (((reverseString("o") + "l") + "l") + "e") + "h"
= ((("o" + "l") + "l") + "e") + "h"     ← BASE CASE
= "ol" + "l" + "e" + "h"
= "olleh" ✅
```

---

## Contoh: Cek Palindrome

```js
function isPalindrome(str) {
  if (str.length <= 1) return true;  // base case
  if (str[0] !== str[str.length - 1]) return false; // huruf depan ≠ belakang
  return isPalindrome(str.slice(1, -1)); // cek tanpa huruf depan & belakang
}

console.log(isPalindrome("racecar")); // true
console.log(isPalindrome("hello"));   // false
console.log(isPalindrome("katak"));   // true
```

---

## ⚠️ Kapan Pakai Recursion vs Loop?

| Situasi | Pakai |
|---------|-------|
| Masalah bisa dipecah jadi sub-masalah yang sama | Recursion ✅ |
| Tree/graph traversal | Recursion ✅ |
| Simple iteration | Loop ✅ |
| Performance critical | Loop ✅ |
| Code readability lebih penting | Recursion ✅ |

> **Pro tip:** Hampir semua recursion bisa diconvert ke loop, dan sebaliknya. Pilih yang bikin kode lo paling **readable**.

---

## Latihan Mandiri

1. Bikin `sumDigits(n)` yang jumlahkan semua digit. Contoh: `sumDigits(1234)` → 10
2. Bikin `countDown(n)` yang print n sampai 0 secara rekursif
3. Bikin `flattenArray(arr)` yang ratakan nested array pakai recursion
4. Bikin `power(base, exp)` tapi yang handle exponent negatif juga

---

## Sumber Tambahan

- 📹 [Recursion Explained (YouTube)](https://youtu.be/LteNqj4DFD8)
- 📖 [MDN Functions - Recursion](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#recursion)
