# Belajar Kotlin
## Type Data dan Variable
Membutuhkan kata kunci **var** atau **val**
Penulisannya : 
```kotlin
var judul: String = "Type data & Variable"
```
> **judul => identifier**
>  **String => type data**

penulisannya bisa juga :
```kotlin
val judul = "Type Data & Variable"
```
>**var** untuk nilai yang dapat berubah ketika sudah diinisialisasikan
>**val** untuk nilai yang tidak dapat berubah

## Function
Fungsi dapat digunakan untuk mengembalikan nilai. Pemanggilan fungsi bisa diberi argumen atau tidak.
Penulisannya : 
```kotlin
1.  fun functionName(param1:  Type1, param2:  Type2,  ...):  ReturnType  {
2.  	return result
3.  }
```
>**functionName => Nama sebuah function**
>**param1=>Parameter 1**
>**Type1=>Type data dari parameter 1**
>**param2=>Parameter 2**
>**Type2=>Type data dari parameter 2**
>**ReturnType=>Nilai kembalian (return)**

contoh : 
```kotlin
fun dataUser(nama: String, umur: Int): String {
	return "My Name is $name, I'm $age years old"
}
```
nilai yang akan dikembalikan diikuti oleh kata kunci **return**
Pemanggilan fungsi, bisa dilakukan dengan pendekatan tradisional seperti berikut:
```kotlin
fun main() {
	val user = dataUser("Randy Wiratama", 27)
	println(user)
}

fun dataUser(nama: String, umur: Int): String {
	return "My Name is $name, I'm $age years old"
}
```

## If Expression
If expression direpresentasikan dengan kata kunci if. If akan mengeksekusi sebuah _statement_ atau _expression_ jika hasil evaluasi dari _expressions_ yang diberikan pada blok if bernilai **true**. Sebaliknya, jika bernilai **false** maka proses yang ditentukan akan dilewatkan.
Penulisan : 
```kotlin
val openHours = 7
val now = 7
val office: String

if(now > openHours) {
	office = "Office already open"
} else if (now == openHours) {
	"Wait a minute, office will be open"
} else {
	"Office is closed"
}
```

## Arrays
Array adalah tipe data yang memungkinkan kita untuk menyimpan beberapa objek didalam sebuah variable. Array di kotlin direpresentasikan oleh kelas **Array** yang memiliki fungsi **set** dan **get** serta properti **size**. Untuk membuat sebuah array, kita dapat memanfaatkan library function **_arrayOf()_**
Penulisan :
```kotlin
val dataArray = arrayOf(1, 4, 5, "kotlin", true)
```

## Nullable Types
Ketika mengembangkan sebuah program, ada satu hal yang tak boleh kita abaikan. Ia adalah **NullPointerException (NPE)**, sebuah kesalahan yang terjadi saat ingin mengakses atau mengelola nilai dari sebuah variabel yang belum diinisialisasi atau variabel yang bernilai **null**. Karena sangat umum terjadi dan bisa berakibat fatal, **NPE** terkenal dengan istilah _**“The Billion Dollar Mistake”**_.
Pada Kotlin kita dimudahkan untuk mengelola variable _**nullable**_
Penulisan :
```kotlin
val text: String? = null
```
Jika ingin sebuah object bernilai null, kita bisa menambahkan tanda **?** seteleh menentukan tipe data object tersebut.

## Safe calls Operator (?.)
Safe call akan menjamin kode yang kita tulis aman dari **NullPointerException**. Dalam menggunakan safe call, kita akan menggantikan tanda titik ==( **.** )== dengan tanda ==(**?.**)== saat mengakses atau mengelola nilai dari object _nullable_
Penulisan : 
```kotlin
val data: String? = null //deklarasi variable atau object
data?.length //safe calls operator
```
dengan safe call, kompiler akan melewatkan proses jika object / variable tersebut bernilai **null**

## Elvis Operator (?:)
**Elvis operator** memungkinkan kita untuk menetapkan _default value_ atau nilai dasar jika objek bernilai **null**.
```kotlin
val data: String? = null //deklarasi variable atau object null
val textLength = data?.length ?: 7
```
kode diatas sebenarnya sama dengan **if/else** berikut :
```kotlin
val.textLength = if (data != null) data.length else 7
```
Elvis Operator akan mengembalikan nilai ```data.length``` jika ```data``` tidak bernilai **null**. Sebaliknya, jika ```data``` bernilai **null** maka default value yang akan dikembalikan.
Perhatikan penggunaan operator **non-null assertion** ``(!!)``, misalnya seperti berikut:
```kotlin
val data: String? = null
val textLength = data!!.length
```
dengan menggunakan **non-null assertion** kompiler akan mengizinkan kita untuk mengakses atau mengelola nilai dari sebuah objek _nullable_.Namun penggunaan operator tersebut sangat tidak disarankan karena akan memaksa sebuah objek menjadi **non-null.** Sehingga ketika objek tersebut bernilai **null**, Anda tetap akan berjumpa dengan **NullPointerException**.

## Enumeration
Enumeration merupakan salah satu fitur yang kita gunakan untuk menyimpan kumpulan objek yang telah didefinisikan menjadi tipe data konstanta. Enumeration dapat ditetapkan sebagai nilai kedalam sebuah variable dengan cara yang lebih efesien.
Contohnya :
```kotlin
fun main () {
    val colorRed = Color.RED
    val colorGreen = Color.GREEN
    val colorBlue = Color.BLUE
}

enum class Color(val value: Int) {
    RED(0xFF0000)
    GREEN(0x00FF00)
    BLUE(0x0000FF)
}
```
Perhatikan. Untuk mendapatkan daftar objek Enum kita bisa menggunakan fungsi _`values()`_. Sedangkan untuk mendapatkan nama dari objek Enum kita bisa menggunakan fungsi _`valueOf()`_ seperti berikut: