# Object-Oriented Programming (OOP)
## Object Everywhere
Pada sub-modul **Data Types** telah disebutkan bahwa pada Kotlin semua bertindak sebagai objek dimana kita bisa memanggil _member function_ dan properti dari sebuah variable. Objek merupakan hasil realisasi dari sebuah _blueprint_ atau _class_ yang tentunya memiliki fungsi dan juga properti sama seperti *blueprint*-nya. Artinya, dengan membuat objek kita dapat mengakses fungsi dan properti yang terdapat pada kelas tersebut.

Pada Kotlin, nilai primitif seperti **String**, **Integer**, **Char**, **Boolean** merupakan sebuah **Object**. Hal ini berbeda dengan bahasa pemrograman lain. Maka dari itu, terdapat sebuah istilah yang terkenal di kotlin, yaitu "**Object Everywhere**". Perhatikan kode berikut :
```java
val someString = "Kotlin Dicoding"
```

Pada kode tersebut kita melakukan pembuatan variable yang juga merupakan sebuah object dengan nama `someString`. Objek tersebut merupakan realisasi dari kelas `String`, maka object `someString` memiliki fungsi dan properti yang merupakan anggota dari kelas `String`.

Dari completion suggestion yang tersedia pada IntelliJ Idea, kita bisa melihat beberapa fungsi yang dapat digunakan oleh objek `someString`. Kita bisa menggunakan fungsi `reverse()` untuk membuat urutan huruf disusun secara terbalik, fungsi `toUpperCase()` yang dapat membuat huruf menjadi kapital atau fungsi `toLowerCase()` yang dapat membuat menjadi huruf kecil.
```java
fun main() {
    val someString = "Kotlin"
    println(someString.reversed())
    println(someString.toUpperCase())
    println(someString.toLowerCase())
}

/*
output :
    niltoK
    KOTLIN
    kotlin
*/
```
Kita juga dapat mengubah tipe data dengan mengakses fungsi yang tersedia dari sebuah objek String.
```java
fun main() {
    val someString = "123"
    val someInt = someString.toInt()
    val someOtherString = "12.34"
    val someDouble = someOtherString.toDouble()

    println(someInt is Int) 
    println(someDouble is Double) 
}
```
Hasil dari *output* kode menunjukan nilai **true** pada kedua variabel tersebut, yang artinya kita telah berhasil mengubah suatu tipe data String ke tipe data lainnya dengan menggunakan fungsi yang terdapat pada objek String.

Mungkin seperti itulah gambaran mengenai objek. Penting digaris bawahi bahwa objek merupakan realisasi dari sebuah *blueprint* yang tentunya memiliki properti dan fungsi yang sama dengan *blueprint*-nya. Salah satu kegunaan objek adalah untuk mengakses berbagai properti dan fungsi pada kelas.

## Class
Seperti yang telah dijelaskan dalam pembahasan objek, **Class** merupakan sebuah _blueprint_. Di dalam **Class** ini kita mendefinisikan sesuatu yang merupakan **attribute** ataupun **behaviour**. Contohnya pada sebuah kelas Kendaraan, atributnya berupa roda, warna, nomor kendaraan, merk, dll. Sedangkan untuk *behaviour* nya yaitu maju, mundur, belok kanan, belok kiri, berhenti. Contoh lainnya pada sebuah kelas Hewan atributnya berupa nama, berat, umur, termasuk mamalia atau bukan dll. Sedangkan untuk *behaviour*-nya bisa makan, tidur, berjalan, dsb.

Setiap kelas memiliki atribut dan *behaviour*. Dalam Kotlin *attributes* lebih sering disebut dengan **properties**, sedangkan *behaviour* sering disebut **functions**. Properti dalam sebuah kelas memiliki tipe data. Contoh, untuk properti berat pada kelas Hewan dapat bertipe **Double**, nama dapat bertipe **String**, umur dapat bertipe **Int** dan indikasi mamalia dapat bertipe **Boolean**. Jika kelas Hewan kita representasikan dalam bentuk tabel maka akan terlihat seperti:

|animal              |
|--------------------|
|+ name: String      |
|+ weight: Double    |
|+ age: Int          |
|+ isMammal: Boolean |
|- eat()             |
|- sleep()           |
|                    |
> **+** merupakan properti
> 
> **-** merupakan fungsi

Pada pembahasan selanjutnya kita akan mencoba membuat sebuah kelas berdasarkan bentuk tabel di atas. Namun kita lanjut ke pembahasan berikutnya, mari kita tekankan kembali beberapa hal yang sudah kita pelajari :

+ **Class** : Merupakan sebuah *blueprint* yang terdapat properti dan fungsi di dalamnya.
+ **Properties** : Karakteristik dari sebuah kelas, memiliki tipe data.
+ **Functions** : Kemampuan atau aksi dari sebuah kelas.

## Membuat Class
Untuk mendefinisikan kelas dalam Kotlin, Anda cukup gunakan kata kunci `class` diikuti dengan nama kelas yang akan dibuat. Mari kita buat contoh kelas pada Kotlin:
```java
class Animal
```
Selanjutnya kita tambahkan properti dan fungsi pada kelas tersebut.
```java
class Animal(
    val name: String,
    val weight: Double,
    val age: Int,
    val isMammal: Boolean) {
        fun eat() {
            println("$name makan !")
        }
        fun sleep() {
            println("$name tidur !")
        }
    }
```
Lalu untuk membuat sebuah objek dari suatu kelas, perhatikan struktur kode berikut :
```java
val nameOfObject = NameOfClass([property1], [property2])
```
Sama seperti variabel, kita bisa gunakan `val` atau `var`, dilanjutkan dengan nama objek yang akan anda buat. Tanda **=** menunjukan bahwa kita akan menginisialisasi suatu objek, kemudian diikuti dengan nama kelas dan tanda kurung. Tanda kurung tersebut menunjukan bahwa kita membuat sebuah objek baru. Di dalam tanda kurung kita dapat menambahkan nilai properti sesuai yang dibutuhkan pada **primary constructor** kelasnya.

Maka jika kita coba membuat objek dari kelas yang sudah kita buat, kodenya akan terlihat seperti ini:
```java
val kucing = Animal("Miaw", 4.2, 2, true)
```
Mari kita coba buat kode secara keseluruhan dengan ditambahkan fungsi cetak untuk melihat nilai properti dalam objeknya.
```java
class Animal(
    val name: String,
    val weight: Double,
    val age: Int,
    val isMammal: Boolean
    ) {
    fun eat() {
        println("$name makan !")
    }
    fun sleep() {
        println("$name tidur !")
    }
}

fun main() {
    val kucing = Animal("Miaw", 4.2, 2, true)
    println("Nama: ${kucing.name}, Berat: ${kucing.weight}, Umur: ${kucing.age}, Mamalia: ${kucing.isMammal}")
    kucing.eat()
    kucing.sleep()
}
/*
output :
    Nama: Miaw, Berat: 4.2, Umur: 2, Mamalia: true
    Miaw makan !
    Miaw tidur !
*/
```