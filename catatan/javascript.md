# Javascript

## Website Asyik untuk Belajar Javascript 
1. <a href="https://bertzzie.com/knowledge/javascript/index.html" target="_blank">Javascript: Sebuah Pembedahan</a>
2. <a href="http://eloquentjavascript.net/" target="_blank">Eloquent JavaScript</a>

## Function
### Bindings dan Scopes
Binding yang dideklarasikan dengan `let` dan `const` menjadikan binding menjadi lokal pada lokasi dimana 
binding dideklarasikan. Sebagai contoh, jika kita mendeklarasikan binding pada looping, 
maka variabel yang diciptakan hanya bisa diakses di dalam looping tersebut (tidak bisa diakses dari
sebelum dan sesudah looping).
Pada JS sebelum 2015, hanya fungsi yang bisa membuat scope baru, 
oleh karenanya old-style bindings yang dilakukan dengan keyword `var` membuat variable menjadi tampak pada fungsi dimana dia diciptakan atau menjadi global jika dideklarasikan bukan pada sebuah fungsi.

```
let x = 10;
if (true) {
  let y = 20;
  var z = 30;
  console.log(x + y + z);
  // → 60
}
// y is not visible here
console.log(x + z);
// → 40
```

Coba cari solusi ini :
```
let ingredient = function(){
	console.log('Diluar');
}

ingredient();

const hummus = function(factor) {
  const ingredient = function(amount, unit, name) {
    let ingredientAmount = amount * factor;
    if (ingredientAmount > 1) {
      unit += "s";
    }
    console.log(`${ingredientAmount} ${unit} ${name}`);
  };
  ingredient(1, "can", "chickpeas");
  ingredient(0.25, "cup", "tahini");
  ingredient(0.25, "cup", "lemon juice");
  ingredient(1, "clove", "garlic");
  ingredient(2, "tablespoon", "olive oil");
  ingredient(0.5, "teaspoon", "cumin");
  
  // Akan jadi masalah jika kita ingin memanggil fungsi ingredient
  // yang dideklarasikan diluar.
  // ingredient();
  
};

hummus(1);
```

## Object

### Properties
Hampir semua value di JS memiliki `Properties`, terkecuali `null` dan `undefined`.
Untuk mengakses property, bisa menggunakan :
1. Tanda `[]` : `object[x]`. Nilai `x` merupakan sebuah ekspresi dan akan dievaluasi terlbih dahulu
2. Tnda titik `.` : `object.propertinya`. `propertinya` harus berupa valid identifier.

Tanda `{}` pada JS memiliki 2 arti:
1. Sebagai penanda object
2. Sebagai awal dari sebuah *block statemant*

#### Rangkuman object
- Membaca properti yang tidak ada pada objek akan mengembalikan nilai `undefined`.
- Operator `delete` berfungsi untuk menghapus sebuah properti pada objek. (`delete object.property`)
- Operator `in` berfungsi untuk mengecek apakah sebuah properti ada di sebuah objek. (`'left' in object'`)
- Untuk mendapatkan semua property pada sebuah objek, gunakan `Object.keys({x: 0, y: 0, z: 2})`
- Untuk meng-copy semua properti pada sebuah object ke object lain gunakan `Object.assign(objectYujuan, {b: 3, c: 4})`  
- `typeof []` akan menghasilkan *object*


### Muttability
- numbers, strings, dan Booleans, bersifat immutable
- Nilai/value dari tipe data yang immutable tidak bisa diubah.

### Destructuring
```
function phi(table) {
  return (table[3] * table[0] - table[2] * table[1]) /
    Math.sqrt((table[2] + table[3]) *
              (table[0] + table[1]) *
              (table[1] + table[3]) *
              (table[0] + table[2]));
}
```

bisa ditulis dengan

```
function phi([n00, n01, n10, n11]) {
  return (n11 * n00 - n10 * n01) /
    Math.sqrt((n10 + n11) * (n00 + n01) *
              (n01 + n11) * (n00 + n10));
}
```

Untuk mengambil nilai dari tertentu saja dari sebuh objek, bisa menggunkan sintaks seperti berikut:
```
let {name} = {name: "Faraji", age: 23};
console.log(name);
// → Faraji
```









 


