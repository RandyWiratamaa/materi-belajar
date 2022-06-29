# Kotlin Functional Programming
---
## Functional Programming
---
Untuk mengawalinya, perhatikan kode berikut:
```kotlin
val list = getListUser()

fun getUsername(): List<String>{
    val name = mutableListOf<String>()
    for (user in list){
        name.add(user.name)
    }
    return name
}
```
kode diatas biasanya kita tuliskan untuk mendapatkan nilai tertentu dari sebuah list. Karena kode pada Kotlin bisa dituliskan dengan gaya fungsional, maka kode di atas cukup dituliskan seperti berikut:
```kotlin
fun getUsername(): List<String>{
    return list.map {
        it.name
    }
}
```
## Anatomi Function
---
Pada dasarnya sebuah fungsi memiliki 2 (dua) bagian utama yaitu **function header** dan **function body**.

### Function Header
Function header adalah bagian yang merupakan konstruksi dari sebuah fungsi untuk menentukan perilakunya akan seperti apa. Di dalam function header terdapat _visibility modifier_, kata kunci `fun`, nama, daftar parameter dan nilai kembalian dari fungsi tersebut.

### Visibility Modifier
Visibility modifier atau tingkatan akses merupakan bagian spesifik dari sebuah bahasa pemrograman yang ditujukan untuk mengatur bagaimana hak akses dari sebuah kelas, fungsi, properti dan variabel.

Secara default ketika kita membuat sebuah fungsi baru, ia akan memiliki _modifier_ **public**. Artinya fungsi tersebut dapat diakses dari luar kelas. Sedangkan contoh pada ilustrasi di atas adalah sebuah fungsi yang memiliki _modifier_ **private**. Maka akses dari fungsi tersebut terbatas hanya untuk kelas di mana fungsi tersebut dideklarasi.

Terdapat beberapa visibility modifier yang akan kita pelajari bersama pada sub-modul Object Orientation Programming nanti.

### Function Name
Nama dari sebuah fungsi merupakan sebuah identifier yang akan memudahkan kita untuk menggunakan fungsi tersebut. Perlu diketahui bahwa kita tidak bisa memberikan nama yang sama untuk beberapa fungsi.

Untuk penamaan dari sebuah fungsi sendiri menggunakan format penulisan **camelCase**. Nama dari fungsi tersebut diawali dengan huruf kecil dan huruf besar untuk kata berikutnya. Ini merupakan standar penulisan resmi yang sudah ditentukan.

### Function Parameter
Ketika kita mendeklarasikan sebuah fungsi baru, kita bisa atau tanpa menetapkan parameter tersebut. Parameter adalah data atau nilai yang disematkan ketika fungsi tersebut dipanggil. Nantinya parameter akan diproses di dalam fungsi tersebut. Kita bisa melampirkan nilai konstan atau variabel untuk sebuah fungsi ketika ia dipanggil.

Parameter dari sebuah fungsi terdiri dari nama dan tipe dari parameter itu sendiri. Ia digunakan untuk menentukan nilai atau variabel apa yang dapat dilampirkan. Setiap parameter dipisahkan oleh tanda (,). Catatan: setiap parameter bersifat read-only, sehingga kita hanya diijinkan untuk menggunakan nilainya untuk diproduksi.

### Function return type
Setiap fungsi yang kita deklarasi akan selalu mengembalikan dan nilai yang akan dikembalikan bisa kita gunakan untuk keperluan lain. Misalnya untuk dijadikan sebagai argumen untuk fungsi lainnya.

Lalu apakah tipe ini harus ditentukan setiap deklarasi sebuah fungsi? Tentu tidak. Jika kita tidak menentukan return type, secara implisit fungsi tersebut akan mengembalikan nilai dengan tipe Unit, yaitu return type yang tidak mengembalikan nilai signifikan.

### Funtion Body
**function body** ditandai dengan _curly braces_. Di dalamnya kita akan menempatkan sebuah logika kode baik itu sebuah _expression_ atau _statement_. Seperti yang dijelaskan pada sub-modul pengenalan, jika kita menetapkan sebuah fungsi dapat mengembalikan nilai, maka kita wajib menambah sebuah baris kode yang diawali dengan kata kunci return yang diikuti oleh _expression_ untuk menetapkan nilai yang akan dikembalikan.

## Named Argument
---
Penamaan pada argument ini berguna agar pada penulisan parameter kita tidak perlu lagi untuk menghafal posisi.
```kotlin
fun getFullName(first: String, middle: String, last: String): String {
    return "$first $middle $last"
}
```
Nah, dengan memanfaatkan named argument, kita bisa menuliskannya seperti di bawah ini:
```kotlin
fun main() {
    val fullName = getFullName(first = "Belajar", middle = "Kotlin", last = "Dicoding")
    print(fullName)
}

fun getFullName(first: String, middle: String, last: String): String {
    return "$first $middle $last"
}
```
## Default Argument
---
Kotlin juga memungkinkan kita untuk menentukan nilai _default_ dari sebuah parameter. Jika melewatkan argumen untuk dilampirkan, maka nilai _default tersebutlah yang akan digunakan.

Untuk menambahkan nilai default itu sendiri pun cukup mudah, yaitu dengan cara menempatkannya langsung tepat di samping dari parameter seperti halnya ketika ingin menginisialisasikan sebuah nilai untuk variabel. Contohnya seperti berikut:
```kotlin
fun getFullName(
        first: String = "Belajar", 
        middle: String = " Kotlin ", 
        last: String = "Dicoding"): String {
    return "$first $middle $last"
}
```
Kita bisa memanggil fungsi di atas seperti biasanya. Tetapi karena parameternya sudah memiliki nilai, maka argumen untuk fungsi tersebut bisa dilewatkan ketika dipanggil.
```kotlin
fun main() {
    val fullName = getFullName()
    println(fullName)
}

fun getFullName(
    first: String = "Belajar",
    middle: String = "Kotlin",
    last: String = "Dicoding"): String {
        return "$first $middle $last"
    }

    //output : Belajar Kotlin Dicoding
```
Ketika kita telah menetapkan nilai default, kita tak perlu khawatir saat lupa melampirkan sebuah argumen. Tentunya ini menghindari kita dari eror. Meskipun begitu, kita tetap bisa melampirkan sebuah argumen. Contohnya seperti berikut:
```kotlin
fun main() {
    val fullName = getFullName(first = "Materi")
    println(fullName)
}

fun getFullName(
    first: String = "Belajar",
    middle: String = "Kotlin",
    last: String = "Dicoding"): String {
        return "$first $middle $last"
    }

    //output : Materi Kotlin Dicoding
```

## Vararg (Variable Argument)
---
Dengan _keyword_ `vararg` kita juga bisa menyederhanakan beberapa parameter yang memiliki tipe data sama menjadi parameter tunggal.

Dengan `vararg` sebuah fungsi dapat memiliki jumlah parameter berdasarkan jumlah argumen yang kita masukkan ketika fungsi tersebut dipanggil. Contohnya adalah :
```kotlin
fun sumAngka(vararg angka: Int): Int {
    return angka.sum()
}
```
Bisa kita perhatikan pada contoh kode di atas bahwa kata kunci `vararg` ditempatkan sebelum nama parameter. Ketika ingin memanggil fungsi tersebut, kita bisa melampirkan beberapa argumen, misal seperti berikut:
```kotlin
fun main() {
    val angka = sumAngka(10,20,30,40)
    println(angka)
}

fun sumAngka(vararg angka: Int): Int {
    retun angka.sum()
}

// output : 100
```
Selain itu kita juga bisa menerapkan Generic untuk tipe parameter ketika parameter tersebut ditentukan dengan `vararg`. Contohnya seperti berikut:
```kotlin
fun <T> asList(vararg input: T): List<T> {
    val result = ArrayList<T>()
    for (item in input)
        result.add(item)
    return result
}
```
Ketika sebuah parameter ditentukan dengan `vararg`, pada dasarnya semua argumen yang dilampirkan, ditampung di dalam sebuah `Array<out T>` seperti pada kode contoh diatas.

Karena pada dasarnya adalah sebuah array, maka kita bisa memanggil fungsi atau properti yang tersedia pada kelas array dari dalam fungsi tersebut. 

```kotlin
fun main() {
    val angka = getAngkaSize(10,20,30,40,50,60)
    println(angka)
}

fun getAngkaSize(vararg angka: Int): Int {
    return angka.size // menggunakan properti size
}

// output : 5
```
di dalam sebuah fungsi, tidak diizinkan untuk memiliki 2 (dua) parameter bertanda `vararg`.


Selanjutnya jika kita ingin menambahkan parameter baru tanpa kata kunci `vararg`, parameter yang ditandai dengan `vararg` sebaiknya berada pada posisi terakhir. COntohnya seperti berikut :
```kotlin 
fun main() {
    sets("Kotlin", 10, 10)
}
 
fun sets(name: String, vararg number: Int): Int {
    ...
}
```
## Extension
Kotlin memungkinkan kita untuk menambahkan sebuah fungsi baru pada sebuah kelas tanpa harus mewarisi kelas tersebut. Misal kita ingin menambahkan fungsi baru untuk kelas Int, maka kita akan menuliskannya seperti berikut:
```kotlin
class NewInt : Int(){
    fun printInt(){
        println("value $this")
    }
}
```
Ketika dijalankan, kode di atas akan gagal dikompilasi, kenapa? Karena kelas `Int` bersifat final, sehingga tidak memungkinkan untuk mewarisi kelas tersebut. Untuk itu, kita bisa melakukannya dengan deklarasi khusus yang disebut dengan **Extensions**. 

Kotlin mendukung 2 (dua) extension yang dapat digunakan, yaitu **Extension Functions** dan **Extension Properties**. Jika extension functions digunakan untuk menambahkan fungsi baru, extension properties tentunya digunakan untuk menambahkan sebuah properti baru.

## Extension Functions
Untuk mendeklarasikan sebuah extension function, kita perlu menentukan terlebih dahulu _receiver type_, sedangkan kata kunci `this` adalah _receiver type_ yang bertindak sebagai objeknya.
Nilai dari objek tersebut bisa digunakan di dalam _extension_ yang sudah dibuat. untuk memanggil _extension function_ diatas, dilakukan dengan cara seperti berikut :
```kotlin
fun main() {
    10.printInt()
}

fun Int.printInt() {
    println("value $this")
}

// output : value 10
```
Kita juga bisa menetapkan jika extension functions tersebut dapat mengembalikan nilai, deklarasinya pun sama halnya seperti fungsi pada umumnya. Contohnya seperti berikut:
```kotlin
fun main() {
    println(10.penjumlahan())
}

fun Int.penjumlahan(): Int {
    return this + 4
}

// output : 14
```
## Extensions Properties
Deklarasinya sama seperti extension functions. Kita terlebih dahulu menentukan _receiver type_ kemudian nama dari properti tersebut. Contoh seperti berikut:
```kotlin
val Int.pembagian: Int
get() = this / 2
```
Untuk memanggil extension di atas, lakukan dengan cara berikut:
```kotlin
fun main() {
    println(10.pembagian)
}
val Int.pembagian: Int 
get() = this / 2

// output : 5
```

## Nullable Receiver
Kita juga bisa mendeklarasikan _extension_ dengan _nullable receiver type_. Alhasil, extension tersebut bisa dipanggil pada objek yang bahkan nilainya **null**.
```kotlin
val Int?.pembagian: Int
get() = if (this == null) 0 else this.div(2)
```
**If expression** pada contoh di atas adalah untuk memeriksa apakah receiver object-nya bernilai **null**. Jika tidak bernilai **null**, maka receiver object tersebut akan secara otomatis di-casting menjadi tipe **non-null**, sehingga kita bisa menggunakan nilainya.

Selain menggunakan if expression, kita juga bisa menggunakan elvis operator. Misalnya seperti berikut:
```kotlin
val Int?.pembagian: Int
    get() = this?.div(2) ?: 0 // Elvis Operator
```
Untuk memanggilnya pun sama seperti extension properties sebelumnya.
```kotlin
fun main() {
    val value: Int? = null
    println(value.pembagian)
}

val Int?.pembagian: Int
get() = this?.div(2) ?:0

// output : 0
```
Saat kita tidak menetapkannya dengan _nullable receiver_ type, maka kita perlu memeriksa apakah objek tersebut bernilai **null** atau tidak? Bisa juga dengan menggunakan operator safe call setiap kali _extension_ tersebut dipanggil. Contohnya seperti berikut:
```kotlin
fun main() {
    val value: Int? = null
    val value1: Int? = null

    println(value?.pembagian)
    println(value1?.pembagian)
}
val Int?.pembagian: Int
get() = this.div(2)

/* 
output :    null
            null
*/
```
Kita juga bisa menentukan nilai dari _receiver object_ jika bernilai **null**. Sehingga kita tidak perlu lagi menggunakan operator safe call ketika ingin memanggil _extension_ tersebut.
```kotlin
fun main() {
    val value: Int? = null
    val value1: Int? = null

    println(value?.pembagian)
    println(value1?.pembagian)
}
val Int?.pembagian: Int
get() = this.div(2) ?: 0

/* 
output :    0
            0
*/
```

## Function Type
Funtion type dapat membuat sebuah fungsi menjadi tipe data. Kotlin sendiri menggunakan function type untuk tipe deklarasi yang berhubungan dengan sebuah fungsi. Dalam penggunaannya, terdapat beberapa tanda yang berhubungan dengan sebuah fungsi seperti jumlah dan tipe parameter serta tipe kembalian(_return_).
```kotlin
(Int, Int) -> String
```
setiap function type memiliki tanda kurung. Didalamnya terdapat sebuah parameter dan jumlah tipe yang menandakan jumlah parameter dari fungsi tersebut. Pada contoh diatas, fungsi tersebut memiliki 2 (dua) parameter dengan tipe `Int` dan memiliki tipe _return_ `String`. Ketika kita tidak ingin fungsi tersebut mengembalikan nilai, kita bisa menggunakan `Unit`. Berbeda dengan fungsi pada umumnya, jika menggunakan tipe kembalian unit, kita tidak wajib menuliskannya.

Ketika kita mempunyai beberapa fungsi yang memiliki function type yang sama, kita bisa menyederhanakannya dengan memanfaatkan kata kunci `typealias` untuk memberikan name alternatif dari sebuah function type seperti berikut :
```kotlin
typealias Arithmetic = (Int, Int) -> Int
val sum: Arithmetic = { valueA, valueB -> valueA + valueB }
val multiply: Arithmetic = { valueA, valueB -> valueA * valueB }
```
`typealias` cocok digunakan ketika mempunyai sebuah function type yang panjang. Dengannya, kita bisa memberikan nama untuk sebuah function type dan menggunakannya sebagai tipe untuk fungsi lainnya.

Untuk membuat _instance_ dari sebuah function type, terdapat beberapa cara, salah satunya dengan lambda expression. Sedangkan untuk menggunakan _instance_-nya, kita bisa memanfaatkan operator `invoke()` seperti berikut :
```kotlin
val sumResult = sum.invoke(10,10)
val multiplyResult = multiply.invoke(20,20)
```
atau kita bisa menuliskannya secara langsung dengan menghilangkan operator `invoke()`.
```kotlin
val sumResult = sum(10,10)
val multiplyResult = multiply(20,20)
```
kita juga bisa menandai function type sebagai **nullable** dengan menempatkannya didalam tanda kurung dan diakhiri dengan _`safe call`_ seperti berikut :
```kotlin
typealias Arithmertic = ((Int, Int) -> Int)?
val sum: Arithmetic = { valueA, valueB -> valueA + valueB }
```
Berikut adalah contoh penggunaan function type yang ditandai sebagai **nullable** :
```kotlin
sum?.invoke(10,20)
```

## Lambda
Lambda expression biasa disebut _anonymous function_ atau _function literal_. Disebut sebagai _anonymous_ karena lambda tidak memiliki sebuah nama seperti halnya sebuah fungsi pada umumnya. Karena merupakan sebuah fungsi, lambda juga dapat memiliki daftar **parameter**, **body**, dan **return type**.

Karakteristik dari lambda adalah :
1. Dalam menggunakan lambda, kita tidak perlu mendeklarasi tipe spesifik untuk kembaliannya. Tipe tersebut akan ditentukan oleh kompiler secara otomatis.
2. Walaupun merupakan sebuah fungsi, lambda tidak membutuhkan kata kunci `fun` dan _visibility modifier_ saat dideklarasikan, karena lambda bersifat _anonymous_.
3. Parameter yang ditetapkan berada di dalam kurung kurawat **{}**.
4. Ketika ingin mengembalikan nilai, kata kunci return tidak diperlukan lagi karena kompiler akan secara otomatis mengembalikan dari dalam **body**.
5. Lambda expression dapat digunakan sebagai argumen untuk sebuah **parameter** dan dapat disimpan dalam variable.

Dari beberapa karakteristik diatas, lambda sangat berguna karena dapat membuat penulisan kode menjadi lebih mudah dan sederhana. Salah satu contohnya adalah kita bisa menghindari _boilerplate code_ dalam menggunakan _anonymous class_ seperti berikut :
```kotlin
val comparator = object :Runnable{
    override fun run() {
        // TODO:
    }
}
```
dengan lambda, kita bisa menyederhanakannnya menjadi seperti di bawah ini :
```kotlin
val comparator = Runnable {
    // TODO:
}
```
## Menggunakan Lambda Expression
Cara mendeklarasikan lambda :
```kotlin
val message = { println("Hello from Lambda") }
```
fungsi lambda diatas ditandai dengan sepasang kurung kurawal, didalamnya terdapat fungsi untuk mencetak teks pada konsol. Ketika menggunakannya, kita bisa memanggilnya seperti halnya kita memanggil sebuah fungsi pada umumnya.
```kotlin
fun main() {
    message()
}

val message = { println("Hello from Lambda") }

// output : Hello from Lambda
```
Jika kita ingin menambahkan sebuah parameter pada fungsi lambda, kita bisa menuliskannya seperti berikut:
```kotlin
fun main() {
    printMessage("Hello from Lambda")
}

val printMessage = { message: String -> println(message) }
```
Untuk membedakan **body**, daftar **parameter** yang ada dipisahkan dengan tanda `->`. Kemudian, bagaimana cara mendeklarasi lambda agar dapat mengembalikan nilai? Untuk itu kita bisa menuliskannya seperti di bawah ini: 
```kotlin
fun main() {
    val length = messageLength("Hello from Lambda")
    println("Message length $length")
}
val messageLength = { message: String -> message.length }
```
Bisa kita perhatikan, kita tidak membutuhkan tipe kembalian dan kata kunci `return` untuk mengembalikan sebuah nilai. Pada dasarnya, kompiler akan mengembalikan nilai berdasarkan expression atau statement di baris terakhir di dalam **body**.

## High-Order Function
Dalam mendeklarasi lambda, khususnya jika ingin ditetapkan agar dapat mengembalikan nilai, terkadang kompiler tidak dapat menentukan tipenya. Alhasil, kita perlu menuliskannya secara eksplisit. Terdapat beberapa tipe deklarasi yang dapat kita gunakan untuk mendeklarasi lambda, antara lain: 
```kotlin
var sum: (Int) -> Int = { value -> value + value }
```
Tipe deklarasi pada kode di atas adalah contoh ketika kita ingin membuat lambda yang memiliki 1 (satu) parameter dengan tipe kembalian Int.

Dengan ditetapkannya tipe deklarasi pada fungsi tersebut, memungkinkan kita untuk bisa menggunakannya sebagai argumen untuk fungsi lainnya. Contohnya seperti berikut:
```kotlin
fun main() {
    printResult(10, sum)
}

fun printResult(value: Int, sum: (Int) -> Int) {
    val result = sum(value)
    println(result)
}

var sum: (Int) -> Int = { value -> value+ value }

// output : 20
```
atau kita bisa melampirkannya secara langsung ketika fungsi `printResult()` diatas dipanggil seperti berikut :
```kotlin
fun main() {
    printResult(10){ value ->
        value + value
    }
}

fun printResult(value: Int, sum(Int) -> Int) {
    val result = sum(value)
    println(result)
}
```
Konsep ini dinamakan sebagai **Higher-Order Function**, yaitu sebuah fungsi yang menggunakan fungsi lainnya sebagai parameter, menjadikan tipe kembalian, ataupun keduanya. Yang perlu diperhatikan adalah, jika argumen terakhir dari fungsi merupakan sebuah lambda expression, maka lambda expression tersebut ditempatkan di luar _parenthesis_ seperti pada contoh kode di atas.

## Lambda with Receiver
Setelah mengetahui bagaimana cara mendeklarasikan dan menggunakan lambda, selanjutnya kita akan mempelajari bagaimana lambda dideklarasikan dengan receiver. Konsep ini digunakan sebagai dasar Kotlin untuk digunakan sebagai Domain Specific Languages (DSL).

Apa itu DSL? DSL adalah sebuah bahasa komputer yang dikhususkan untuk domain aplikasi tertentu. Ia berbeda dengan general-purpose language yang bisa diterapkan di semua domain aplikasi. Dengan DSL, kita bisa menuliskan kode lebih ringkas dan ekspresif. Contoh sistem yang menerapkan DSL adalah Gradle dan sistem database yang berbasis SQL.

Pada dasarnya sebuah lambda yang mempunyai receiver mirip seperti extension functions, yang memungkinkan kita untuk mengakses anggota objek receiver dari dalam extension. Pada lambda, receiver ditentukan pada saat menentukan tipe deklarasi. Contohnya perhatikan kode yang tidak menggunakan DSL di bawah ini:
```kotlin
fun buildString(): String {
    val stringBuilder = StringBuilder()
    stringBuilder.append("Hello ")
    stringBuilder.append("from ")
    stringBuilder.append("lambda")
    return stringBuilder.toString()
}
```
Kode di atas merupakan contoh kode StringBuilder yang digunakan untuk menambahkan kata satu per satu. Jika dilihat kode ini cukup panjang tidak fleksibel. Jika Anda ingin membuat menambahkan kata baru harus di dalam kode tersebut dan mengulang-ulang kata stringBuilder. Dengan menggunakan DSL, Anda dapat menyingkat kode tersebut dan cukup fokus pada fungsi _append_-nya saja. Berikut adalah contoh membuat Lambda with Receiver:
```kotlin
fun buildString(action: StringBuilder.() -> Unit): String {
    val stringBuilder = StringBuilder()
    stringBuilder.action()
    return stringBuilder.toString()
}
```
Pada kode di atas, _**`StringBuilder`**_ dijadikan sebagai receiver untuk tipe deklarasi parameter `action`. Dengan begitu kita dapat memanggil parameter `action` tersebut dari variabel yang bertipekan `StringBuilder`. Untuk memanggil fungsi di atas bisa seperti berikut:
```kotlin
fun main() {
    val message = buildString {
        append("Belajar")
        append("Kotlin")
        append("Dicoding")
    }
    println(message)
}

fun buildString(action: StringBuilder.() -> Unit): String {
    val stringBuilder = StringBuilder()
    stringBuilder.action()
    return stringBuilder.toString()
}

// output : Belajar Kotlin Dicoding
```
Seperti yang Anda lihat, kita sebagai client bisa menggunakan suatu fungsi yang kompleks cukup dengan menggunakan fungsi `append` yang dipanggil di dalam block `buildString`. Anda tidak perlu tahu bagaimana proses `buildString` di baliknya, yang terpenting adalah hasilnya sesuai dengan yang diharapkan. 

Ini merupakan salah satu konsep dasar untuk membuat kode yang lebih simpel seperti yang diterapkan pada `Gradle KTS` dan `Jetpack Compose`.

## Kotlin standard library
Kotlin hadir dengan berbagai fitur menarik yang sudah kita bahas pada sub-modul sebelumnya. Salah satu fitur yang selanjutnya perlu kita ketahui adalah **standard function library**, yaitu sebuah extension functions dari sebuah objek yang menggunakan lambda sebagai argumen atau yang disebut sebagai higher-order function.

## Scope Function
Kotlin standard library memiliki beberapa fungsi yang tujuan utamanya adalah bagaimana menuliskan logika kode di dalam konteks dari sebuah objek. Dalam menggunakan fungsi tersebut kita akan memanfaatkan lambda expression yang memiliki ruang lingkupnya sendiri, di mana dalam ruang lingkup tersebut kita dapat mengakses konteks dari sebuah objek.

Fungsi inilah yang dinamakan sebagai scope function. Beberapa fungsi yang berada di dalamnya antara lain **let**, **run**, **with**, **apply**, dan also. Pada dasarnya beberapa fungsi tersebut melakukan tugas yang sama yaitu mengeksekusi blok kode dari dalam sebuah objek. Yang membedakannya adalah bagaimana objek tersebut tersedia dan seperti apa hasil yang didapat dari seluruh expression yang berada di dalam blok.

## Context Object
Sebelum kita mengulas beberapa fungsi yang menjadi bagian dari scope function di atas, kita perlu mengetahui terlebih dahulu bagaimana cara mengakses konteks sebuah objek dari dalam lambda yang menjadi bagian dari scope function. 

Terdapat 2 (dua) cara, yaitu: diakses sebagai lambda receiver (this) dan lambda argumen (it). Keduanya memiliki kapabilitas yang sama dan tentunya digunakan untuk kasus yang berbeda.

### Lambda Receiver (this)
Beberapa fungsi yang menggunakan lambda receiver adalah `run`, `with`, dan `apply`. Ketika ingin mengakses konteks dari sebuah objek, kita bisa saja tidak menuliskan atau menghilangkan kata kunci `this`. Misalnya seperti penggunaan fungsi `apply` berikut:
```kotlin
val buildString = StringBuilder().apply {
    append("Belajar")
    append("Kotlin")
    append("Dicoding")
}
```
Cara ini memiliki kekurangan yaitu kita tidak dapat membedakan objek _receiver_ dengan objek yang berada dari luar lingkup fungsi tersebut. Alih-alih, cara ini lebih ditujukan untuk operasi objek itu sendiri, seperti memanggil fungsi dan inisialisasi nilai dari anggota yang menjadi bagian dari objek tersebut.

### Lambda Argument (it)
Selanjutnya, fungsi yang menggunakan lambda argument untuk mengakses konteks dari sebuah objek adalah fungsi `let` dan `also`. Berbeda dengan lambda receiver, nilai dari argumen tersebut dapat kita gunakan untuk diproduksi atau di inisialisasikan untuk variabel lain. Contohnya seperti berikut:
```kotlin
val text = "Kotlin"
text.let {
    val message = "$it Dicoding"
    println(message)
}
```
Secara _default_, nama dari argumen tersebut adalah `it`, namun kita dapat mengubahnya seperti berikut:
```kotlin
val text = "Kotlin"
text.let { value ->
    val message = "$value Dicoding"
    println(message)
}
```

## Scope function with lambda receiver
### run
Fungsi `run` akan mengembalikan nilai berdasarkan _expression_ yang berada di dalam blok lambda. Untuk mengakses konteks dari objek, ia akan menggunakan receiver (`this`). Fungsi `run` akan sangat berguna jika di dalam blok lambda terdapat inisialisasi objek dan perhitungan untuk nilai kembalian. Contoh penggunaannya seperti berikut:
```kotlin
fun main() {
    val text = "Kotlin"
    val result = text.run {
        val from = this
        val to = this.replace("Kotlin", "Dicoding")
        "replace text from $from to $to"
    }
    println("result : $result")
}

// output : replace text from Kotlin to Dicoding
```

### with
Selanjutnya fungsi `with`. Pada dasarnya fungsi `with` bukanlah sebuah extension melainkan hanyalah fungsi biasa. Konteks objeknya disematkan sebagai argumen dan dari blok lambda diakses sebagai _receiver_. Contohnya seperti berikut:
```kotlin
fun main() {
    val message = "Kotlin Dicoding"
    val result = with(message) {
        "value is $this" + " and text length = ${this.length}"
    }
    return(hasil)
}

// output : value is Kotlin Dicoding and text length = 15
```
Fungsi with sendiri disarankan untuk mengakses apa yang menjadi anggotanya tanpa harus menyediakan nilai kembalian.

### apply
Berbeda dengan fungsi-fungsi sebelumnya, nilai yang dikembalikan dari fungsi `apply` adalah nilai dari konteks objeknya dan objek konteksnya tersedia sebagai _receiver_ (`this`). Baiknya fungsi `apply` dapat melakukan inisialisasi atau konfigurasi dari _receiver_-nya. Perhatikan kode berikut:
```kotlin
fun main() {
    val builder = StringBuilder()
    builder.append("Kotlin")
    builder.append("Dicoding")

    println(builder.toString())
}

// output : Kotlin Dicoding
```
dengan menggunakan fungsi `apply` kita bisa menuliskan seperti dibawah ini :
```kotlin
fun main() {
    val message = StringBuilder().apply {
        append("Kotlin")
        append("Dicoding")
    }
    println(message.toString())
}

// output : Kotlin Dicoding
```

### let
Fungsi `let` menggunakan argumen (`it`) untuk mengakses konteks dari sebuah objek. Penggunaan fungsi `let` akan banyak kita temukan pada objek yang bertipe **non-null**. Contohnya seperti di bawah ini:
```kotlin
fun main() {
    val message: String? = null
    message?.let {
        val length = it.length * 2
        val text = "text length = $length"
        println(text)
    }
}
```
Dengan menggunakan fungsi `let` seperti pada kode di atas, kita bisa mengurangi penggunaan operator `safe call` seperti berikut:
```kotlin
fun main() {
    val message: String? = null
    val length = message?.length ?: 0 * 2
    val text = "text length = $length"
    println(text)
}
```
Lalu bagaimana jika kita ingin menjalankan logika kode lain jika objeknya bernilai **null**? Di sini kita akan memanfaatkan fungsi lainnya yaitu `run` dan _`elvis operator`_ yang sudah kita pelajari sebelumnya. Contohnya seperti berikut:
```kotlin
fun main() {
    val message: String? = null
    message?.let {
        val length = it.length * 2
        val text = "text length = $length"
        println(text)
    } ?: run {
        val text = "message is null"
        println(text)
    }
}
```
Sedangkan untuk nilai kembalian, ia bergantung pada _expression_ yang berada di dalam blok lambda seperti pada contoh di atas. Karena pada baris terakhir dari blok lambda tersebut adalah fungsi `println()`, maka nilai yang akan dikembalikan adalah **Unit**. Ini dikarenakan fungsi `println()` sendiri mengembalikan nilai **Unit**.

### also
Fungsi also sama seperti fungsi `apply`, di mana nilai yang dikembalikan adalah nilai dari konteks objek. Namun untuk konteks objeknya tersedia sebagai argumen (`it`). Fungsi also baiknya digunakan ketika kita ingin menggunakan konteks dari objek sebagai argumen tanpa harus mengubah nilainya. 
```kotlin
fun main() {
    val text = "Kotlin Dicoding"
    val result = text.also {
        println("Panjang Karakter = ${it.length}")
    }
    println("text = $result")
}
    /*
    output :
    Panjang Karakter = 15
    text = Kotlin Dicoding
    */
```
## Member References
Seperti yang sudah kita pelajari pada sub-modul sebelumnya, saat mendeklarasikan sebuah lambda dengan function type, kita bisa menggunakannya seperti berikut:
```kotlin
val sum: (Int, Int) -> Int = { valueA, valueB -> valueA + valueB }
```
Dengan Kotlin, kita bisa memisahkan lambda expression menjadi fungsi tersendiri dan mereferensikannya langsung sebagai instance dari function type dengan cara seperti di bawah ini:
```kotlin
val sum: (Int, Int) -> Int = ::count
fun count(valueA: Int, valueB: Int): Int {
    return valueA + valueB
}
```
Kode di atas ditulis dengan mekanisme **Reflection** yang berarti seperangkat fitur bahasa dan _library_ yang memungkinkan kita untuk mengamati struktur kode dari proyek yang sedang kita kerjakan secara langsung.

## Function References
Pada suatu kondisi, terkadang kita butuh mereferensikan sebuah fungsi. Sebagai contoh, misal kita memiliki fungsi seperti berikut:
```kotlin
fun isEvenAngka(angka: Int) = angka % 2 == 0
```
Fungsi di atas digunakan untuk memeriksa apakah suatu angka merupakan sebuah bilangan genap. Dengan menggunakan operator **`::`** kita bisa menggunakannya sebagai _instances_ dari function type. Sebagai contoh, penggunaan fungsi `filter()` yang menjadi bagian dari kelas List berikut:
```kotlin
fun main() {
    val angka = 1.rangeTo(20)
    val evenAngka = angka.filter(::isEvenAngka)

    println(evenAngka)
}

fun Int.isEvenAngka() = this % 2 == 0

// output = [2,4,6,8,10]
```
## Property References
Selain digunakan untuk mereferensikan sebuah fungsi. Operator **`::`** juga dapat digunakan untuk mereferensikan sebuah properti. Dengan Operator, kita bisa mengakses apa yang menjadi bagian dari properti tersebut seperti nama, fungsi _setter getter_, dll. Contohnya seperti berikut:
```kotlin
var message = "Kotlin"

fun main() {
    println(::message.name)
    println(::message.get())

    ::message.set("Kotlin Dicoding 2022")

    println(::message.get())
}
```
Ekspresi `::message` akan dievaluasi ke dalam objek dengan `KMutableProperty` yang memungkinkan kita untuk membaca nilainya dengan menggunakan `get()`, menetapkan nilai menggunakan `set()` dan mendapatkan nama dari properti tersebut menggunakan properti `name`.

Sedangkan untuk properti yang bersifat _immutable_ seperti ``val message = “Kotlin”``, `::message` akan mengembalikan nilai dengan tipe `KProperty`, yang mana hanya terdapat fungsi `get()` di dalamnya.
```kotlin
var message = "Kotlin"

fun main() {
    println(::message.name)
    println(::message.get())

    ::message.set("Kotlin Dicoding 2022")

    println(::message.get())
}
```

## Function inside Function
Ketika mengembangkan sebuah proyek, kita pasti membuat beberapa fungsi tersendiri dengan tujuan untuk memisahkan logika program dari fungsi utama. Tujuannya adalah agar kode lebih terstruktur dan mudah dibaca. Namun pada praktiknya, terkadang kode yang ada pada fungsi tersebut malah lebih panjang dan susah dibaca. Salah satu penyebabnya adalah karena penulisan kode yang berulang atau lainnya.

Untuk mengatasinya, kita bisa memisahkannya lagi menjadi sebuah fungsi lokal (_inner function_) dengan hak akses terbatas hanya untuk fungsi terluarnya. Ini bisa dilakukan karena pada Kotlin kita bisa mendefinisikan sebuah fungsi di mana pun, bahkan di dalam sebuah fungsi (_function inside function_).

Berikut adalah contoh dari sebuah _inner function_:
```kotlin
fun setWord(pesan: String) {
    // inner function
    fun cetakPesan(text: String) {
        println(text)
    }
    cetakPesan(pesan)
}
```
Bisa diperhatikan bahwa fungsi `cetakPesan()` didefinisikan di dalam fungsi `setWord()`. Mendefinisikan sebuah _inner function_ sama halnya seperti kita mendefinisikan sebuah fungsi seperti biasanya. Menariknya, kita bisa mengakses apa yang menjadi bagian fungsi terluarnya. Contoh, parameter dari fungsi s`etWord()` bisa diakses dari dalam fungsi print sehingga kode di atas bisa diubah menjadi seperti berikut:
```kotlin
fun setWord(pesan: String) {
    // inner function
    fun cetakPesan() {
        println(pesan)
    }
    cetakPesan()
}
```
Lebih sederhana bukan? Perlu diperhatikan, _inner function_ hanya bisa diakses setelah fungsi tersebut didefinisikan.

Lalu, pada kondisi seperti apa kita bisa memanfaatkan _inner function_? Perhatikan deklarasi fungsi berikut di bawah ini:
```kotlin
fun penjumlahan(valueA: Int, valueB: Int, valueC: Int): Int {
    if(valueA == 0) {
        throw illegalArgumentException("valueA must be better than 0")
    }

    if(valueB == 0) {
        throw illegalArgumentException("valueB must be better than 0")
    }

    if(valueC == 0) {
        throw illegalArgumentException("valueC must be better than 0")
    }

    return valueA + valueB + valueC
}
```
Tidak ada yang salah dengan semua fungsi di atas. Fungsi tersebut akan berjalan dengan semestinya tanpa adanya eror selama kondisi yang berada di dalamnya tidak terpenuhi. Namun jika kita perhatikan, terdapat pengulangan kode yang sama yaitu penggunaan `if expression` untuk memeriksa apakah nilai dari argumen yang diberikan bernilai **null**.

Di sinilah kita bisa memanfaatkan _inner function_ untuk membuat kode yang ditulis berulang tersebut menjadi fungsi tersendiri.
```kotlin
fun penjumlahan(valueA: Int, valueB: Int, valueC: Int): Int {
    fun validasiAngka(value: Int) {
        if(value == 0) {
            throw IllegalArgumentException("value must be better than 0")
        }
    }
    validasiAngka(valueA)
    validasiAngka(valueB)
    validasiAngka(valueC)

    return valueA + valueB + valueC
}
```
Setelah menjadikannya sebagai sebuah fungsi tersendiri, kode yang ada di dalam fungsi `penjumlahan()` tersebut lebih singkat dan tentunya lebih mudah dibaca dibandingkan sebelumnya.

Selain itu, kita juga bisa menjadikan _inner function_ sebagai _extensions function_. Contohnya seperti berikut:
```kotlin
fun penjumlahan(valueA: Int, valueB: Int, valueC: Int): Int {
    fun validasiAngka(value: Int) {
        if(value == 0) {
            throw IllegalArgumentException("value must be better than 0")
        }
    }
    // extension function
    valueA.validasiAngka()
    valueB.validasiAngka()
    valueC.validasiAngka()

    return valueA + valueB + valueC
}
```

## Fold, Drop, dan Take
Kotlin Collection adalah salah satu struktur data mumpuni yang banyak menyediakan fungsi untuk memudahkan kita dalam mengelola dan memanipulasi data. Pada sub-modul sebelumnya, kita sudah mempelajari beberapa fungsi yang disediakan seperti `map()`, `sum()`, `sorted()`, dan sebagainya.

Pada sub-modul ini kita akan mempelajari beberapa fungsi tingkat lanjut lainnya yang tentunya bisa kita manfaatkan untuk mengelola data seperti yang disebutkan di atas.

### Fold
Langsung saja kita mulai dengan fungsi **fold**, kita bisa dengan mudah melakukan perhitungan setiap nilai yang berada di dalam sebuah _collection_ tanpa harus melakukan iterasi item tersebut satu-persatu menggunakan fungsi `fold()`. Untuk contoh penggunaannya adalah sebagai berikut:
```kotlin
val angka = listOf(1,2,3)
val dataFold = angka.fold(10) { current, item ->
    println("current $current")
    println("item $item")
    println()
    current + item
}
println("Fold result: $dataFold")

/*
output :
    current 10
    item    1

    current 11
    item    2

    current 13
    item    3

    Fold Right Result: 16
*/
```

Fungsi `fold()` memerlukan 2 (dua) argumen yaitu nilai awal untuk perhitungan dan lambda expression yang nilai kembaliannya digunakan untuk menentukan nilai awal selanjutnya. Nah, di dalam lambda expression nya juga terdapat 2 (dua) argumen. Yaitu, argumen `current` yang merepresentasikan nilai awal dan argumen `item` merepresentasikan masing-masing item yang berada pada `val angka`.

Selain itu, terdapat juga fungsi fold lainnya yaitu `foldRight()`. Berbeda dengan fungsi `fold()`, fungsi `foldRight()` akan melakukan proses iterasi dari indeks terakhir dan posisi dari argumen pada lambda expression nya pun berbeda, di mana argumen `item` berada pada posisi pertama dan argumen `current` berada pada posisi kedua. Contohnya seperti berikut:
```kotlin
val angka = listOf(1,2,3)
val dataFold = angka.foldRight(10) { item, current ->
    println("current $current")
    println("item $item")
    println()
    current + item
}
println("Fold Right result: $dataFold")

/*
output :
    current 10
    item    3

    current 13
    item    2

    current 15
    item    1

    Fold Right Result: 16
*/
```
### Drop
Selanjutnya adalah fungsi `drop()`, fungsi yang bisa kita manfaatkan untuk memangkas item yang berada di dalam sebuah objek _collection_ berdasarkan jumlah yang kita tentukan. Sebagai contoh, saat kita mempunyai sebuah _collection_ seperti berikut:
```kotlin
val angka = listOf(1,2,3,4,5,6)
```
Kemudian kita ingin memangkas 3 (tiga) item dari collection di atas. Dengan fungsi `drop()`, kita bisa melakukannya seperti di bawah ini:
```kotlin
val angka = listOf(1,2,3,4,5,6,7)
val hapus = angka.drop(3)

println(hapus)

// output : [4,5,6,7]
```
Seperti yang dijelaskan sebelumnya, nilai 3 yang menjadi argumen dari fungsi `drop()` di atas adalah jumlah item yang akan dipangkas. Pemangkasan dimulai dari posisi atau indeks pertama (`index[0]`), lalu bagaimana jika kita ingin memangkas nilai dari indeks terakhir? Kita bisa menggunakan fungsi `dropLast()`. Contohnya seperti berikut:
```kotlin
val angka = listOf(1,2,3,4,5,6,7)
val hapus = angka.dropLast(3)

println(hapus)

// output : [1,2,3,4]
```

### Take
Jika fungsi `drop()` digunakan untuk memangkas, fungsi `take()` bisa kita manfaatkan untuk menyaring item yang berada di dalam sebuah objek collection. Pemanggilan fungsi `take()` sama halnya seperti fungsi `drop()` di mana kita perlu menentukan jumlah item yang akan disaring. Berikut contoh penggunaannya:
```kotlin
val angka = listOf(1,2,3,4,5,6,7,8)
val take = angka.take(3)

println(take)

// output : [1,2,3]
```
Kotlin juga menyediakan fungsi seperti `dropLast()` yang menjalankan operasi dari posisi atau indeks terakhir yaitu `takeLast()`. Contohnya seperti berikut:
```kotlin
val angka = listOf(1,2,3,4,5,6,7,8)
val take = angka.takeLast(3)

println(take)

// output : [6,7,8]
```

## Slice
Setelah pembahasan fungsi `take()` pada sub-modul sebelumnya, muncul pertanyaan, bagaimana jika kita ingin menyaring item dari posisi tertentu? Untuk itu kita bisa memanfaatkan fungsi `slice()`. Dalam penggunaannya, fungsi `slice()` membutuhkan sebuah argumen berupa Range yang digunakan untuk menentukan posisi pertama dan terakhir yang akan disaring. Berikut contohnya:
```kotlin
val total = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
val slice = slice('3..6')

println(slice)

// output : [4,5,6,7]
```
Karena menggunakan **Range**, kita juga bisa menggunakan operator `step` ketika argumennya disematkan seperti berikut:
```kotlin
val total = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
val slice = slice('3..6 step 2')

println(slice)

// output : [4,6]
```
Kemudian jika ingin menentukan posisi yang lebih spesifik, kita bisa mendefinisikannya di dalam sebuah _collection_, kemudian disematkan sebagai argumen. Misal seperti di bawah berikut:
```kotlin
val index = listOf(2, 3, 5, 8)
val total = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
val slice = total.slice(index)

println(slice)

// output : [3,4,6,9]
```
Kita harus berhati-hati dalam menentukan cakupan index untuk mendapatkan data. Karena dapat menyebabkan terjadinya **ArrayIndexOutOfBoundsException** jika posisi yang ditentukan tidak terdapat pada objek _collection_.

## Distinct
Saat berurusan dengan item yang sama di dalam sebuah _collection_, untuk menyaring item yang sama tersebut kita akan melakukan iterasi dan membandingkan setiap itemnya. Namun dengan Kotlin kita tidak perlu melakukannya secara manual, karena Kotlin _Collection_ menyediakan fungsi untuk melakukannya dengan mudah yaitu fungsi `distinct()`. Sebagai contoh:
```kotlin
val total = listOf(1,2,1,3,4,5,2,3,4,5)
val disticnt = total.distinct()

println(distinct)

// output : [1,2,3,4,5]
```
Sama halnya seperti beberapa fungsi sebelumnya yang sudah dibahas, fungsi `distinct()` bisa langsung dipanggil dari objek _collection_. Kita juga bisa menggunakannya pada _collection_ dengan tipe parameter seperti data **class**. Misal seperti berikut:
```kotlin
data class Item(val key: String, val value: Any)

val Item = listOf(
    Item("1", "Belajar")
    Item("2", "Kotlin")
    Item("3", "Dicoding")
    Item("3", "Tahun")
    Item("3", "2022")
)

val distinctItems = itens.distinctBy { it.key }
distinctItems.forEach {
    println("${it.key} with value = ${it.value}")
}

/*
output :
    1 with value = Belajar
    2 with value = Kotlin
    3 with value = Dicoding
*/
```
Menariknya, kita bisa juga menentukan proses penyaringan item yang sama seperti apa yang akan dijalankan dengan menggunakan fungsi distinctBy(). Misal kita ingin menyaring item yang memiliki panjang sama, kita bisa melakukannya seperti berikut:
```kotlin
val text = listOf("A", "B", "CC", "DD", "EEE", "F", "GGGG")
val distinct = text.distinctBy {
    it.length
}

println(distinct)

// output : [A, CC, EEEE, GGGG]
```
yang perlu diperhatikan, fungsi `distinct()` tidak dapat digunakan pada Object Map Collection

## Chunked
Sama seperti fungsi `split()`, fungsi `chunked()` bisa kita gunakan untuk memecah nilai String menjadi beberapa bagian kecil dalam bentuk Array. Namun untuk penerapannya sedikit berbeda, di mana fungsi `split()` membutuhkan argumen berupa RegEx sebagai parameter sedangkan `chunked()` membutuhkan nilai yang akan digunakan sebagai jumlah indeks untuk pemisah. Contoh penggunaannya seperti berikut:
```kotlin
val word = "QWERTY"
val chunked = word.chunked(3)

println(chunked)

// output : [QWE, RTY]
```
Selain itu, kita juga bisa menggunakannya untuk memodifikasi setiap nilai yang sudah dipecah. Contoh, hasil dari nilai yang sudah dipecah ingin kita buat menjadi huruf kecil, maka kita bisa menggunakan fungsi `chunked()` seperti berikut: 
```kotlin
val word = "QWERTY"
val chunked = word.chunked(3) {
    it.toString().toLowerCase() // mengubah menjadi huruf kecil
}

println(chunked)

// output : [qwe, rty]
```
Argumen yang berada pada lambda expression di atas merepresentasikan setiap nilai yang sudah dipecah.

## Recursion
Recursion merupakan sebuah teknik dasar dalam pemrograman yang bisa kita gunakan untuk menyederhanakan pemecahan masalah yang umumnya diselesaikan dengan cara yang kompleks. Di Kotlin, recursion disebut juga dengan _recursive function_.

Recursive function adalah sebuah mekanisme di mana sebuah fungsi digunakan dari dalam fungsi itu sendiri. Ini memungkinkan sebuah fungsi dapat berjalan beberapa kali. Setiap pemanggilannya bisa kita atur agar dapat mengembalikan nilai dan digunakan sebagai argumen untuk pemanggilan fungsi berikutnya serta mengembalikan nilai akhir berupa perhitungan nilai kembalian dari setiap pemanggilan fungsi tersebut.

Lalu penyelesaian seperti apa yang dapat kita lakukan dengan recursive? Perhatikan kode di bawah ini:
```kotlin
fun factorial(n: Int): Int {
    return if(n == 1) {
        n
    } else {
        var result = 1
        for(i in 1..n) {
            result *= i
        }
        result
    }
}
```
Fungsi di atas adalah contoh bagaimana menghitung faktorial dari nilai yang kita tentukan. Nah, tidak ada yang salah dengan kode tersebut dan dapat dijalankan serta mengembalikan nilai sesuai dengan yang kita inginkan. Namun jika kita perhatikan, untuk menghitung nilai akhir, kode di atas menggunakan _for loop_ yang di setiap iterasinya terdapat proses perhitungan nilai yang akan dikembalikan sebagai nilai akhir. Dengan recursive kita bisa menentukan nilai akhir tersebut dengan cara yang lebih sederhana. Berikut contoh ketika kode di atas ditulis dengan mekanisme recursive:
```kotlin
fun factorial(n: Int): Int {
    return if(n == 1) {
        n
    } else {
        n * factorial(n - 1)
    }
}
```
Ketika kita menjalankan fungsi di atas, program akan menciptakan tumpukan _frame_ dengan jumlah berdasarkan nilai **n** di mana setiap _frame_ akan mengkonsumsi memori. Ini bisa jadi masalah dalam penerapannya. Contoh, jika kita memasukkan argumen dengan nilai besar ketika ingin menggunakannya seperti berikut:
```kotlin
fun main() {
    println("Factorial 9999 is = ${factorial(9999)}")
}

fun factorial(n: Int): Int {
    return if(n == 1) {
        n
    } else {
        n * factorial(n - 1)
    }
}
```
Maka pada konsol akan menampilkan eror berikut:
**`Exception in thread "main" java.lang.StackOverflowError`**

## Tail Call Recursion
Namun kita tidak perlu khawatir dengan masalah seperti di atas. Kotlin mendukung gaya pemrograman fungsional yang bernama _tail recursion_ yakni sekumpulan urutan instruksi untuk menjalankan tugas tertentu (**subroutine**) yang dijalankan terakhir pada sebuah prosedur.

Dengannya, kita bisa meminimalisir penumpukan frame ketika kita menerapkan recursive. **Tail recursion** akan memastikan proses sebelumnya telah selesai sebelum pemanggilan fungsi berikutnya dijalankan. Contohnya adalah seperti berikut:
```kotlin
fun factorial(n: Int, result: Int = 1): Int {
    val newResult = n * result
    return if(n == 1) {
        newResult
    } else {
        factorial(n - 1, newResult)
    }
}
```
Namun dengan kode di atas, kita tidak bisa langsung menghindari penumpukan _frame_. Ini karena secara default JVM tidak mendukung optimasi ***tail recursion***. Untuk itu, Kotlin menyediakan _modifier_ agar kita bisa tetap menerapkannya, yaitu _modifier_ `tailrec`. Penggunaanya adalah seperti berikut :
```kotlin
tailrec fun factorial(n: Int, result: Int = 1): Int {
    val newResult = n * result
    return if(n == 1) {
        newResult
    } else {
        factorial(n - 1, newResult)
    }
}
```
Pada kode diatas, _modifier_ `tailrec` ditempatkan sebelum kata kunci `fun`. Ketika sebuah fungsi ditandai dengan modifier `tailrec`, maka fungsi tersebut hanya boleh dipanggil untuk dijalankan terakhir dan tidak boleh digunakan dari dalam blok **try-catch-finally**.

