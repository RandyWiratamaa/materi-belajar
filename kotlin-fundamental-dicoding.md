# Belajar Kotlin
## Type Data dan Variable
Membutuhkan kata kunci **var** atau **val**
Penulisannya : 
```kotlin
var judul: String = "Type data & Variable"
```
> **judul => identifier**
> 
>  **String => type data**

penulisannya bisa juga :
```kotlin
val judul = "Type Data & Variable"
```
>**var** untuk nilai yang dapat berubah ketika sudah diinisialisasikan
>
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

## Safe calls Operator `?.`
Safe call akan menjamin kode yang kita tulis aman dari **NullPointerException**. Dalam menggunakan safe call, kita akan menggantikan tanda titik ==( **.** )== dengan tanda ==(**?.**)== saat mengakses atau mengelola nilai dari object _nullable_
Penulisan : 
```kotlin
val data: String? = null //deklarasi variable atau object
data?.length //safe calls operator
```
dengan safe call, kompiler akan melewatkan proses jika object / variable tersebut bernilai **null**

## Elvis Operator `?:`
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
    RED(0xFF0000),
    GREEN(0x00FF00),
    BLUE(0x0000FF)
}
```
Untuk mendapatkan daftar objek Enum kita bisa menggunakan fungsi _`values()`_. Sedangkan untuk mendapatkan nama dari objek Enum kita bisa menggunakan fungsi _`valueOf()`_ seperti berikut:
```kotlin
fun main() {
    val color: Color = Color.valueOf("RED")
    println("Color is $color")
    println("Color value is ${color.value.toString(16)}")
}
 
enum class Color(val value: Int) {
    RED(0xFF0000),
    GREEN(0x00FF00),
    BLUE(0x0000FF)
}

/*
    output : 
    Color is RED
    Color value is ff0000
*/
```
Di atas telah disebutkan bahwa setiap objek merupakan instance dari *enum* class yang kita definisikan. Lantas bagaimana cara kita mengecek instance dari Enum itu sendiri? Nah, untuk mengeceknya, gunakan **When Expression** seperti berikut:
```kotlin
fun main () {
    val color: Color = Color.GREEN

    when(color) {
        Color.RED -> print("Color is Red")
        Color.GREEN -> print("Color is Green")
        Color.BLUE -> print("Color is Blue")
    }
}

enum class Color(val value: Int) {
    RED(0xFF0000),
    GREEN(0x00FF00),
    BLUE(0x0000FF)
}
```

## Expression dan Statement
Contoh :
```kotlin
fun main() {
    val value1 = 10
    val value2 = 20

    sum(value1, value2)
}

fun sum(value1: Int, value2: Int) = value1 + value2
```
pada kode diatas deklarasi `value1` dan `value2` adalah sebuah *Statement*. Sedangkan pemanggilan fungsi `sum` merupakan sebuah _Expression_.

## When Expression
Untuk menentukan statement dan expression kita menggunakan **If Expression**. Selain itu kita bisa juga menggunakan **When Expression**, yakni mekanisme yang memungkinkan nilai dari sebuah *variable/expression*, mampu mengubah alur program.
Contoh :
```kotlin
fun main() {
    val value = 7

    when(value) {
        6 -> println(value is 6)
        7 -> println(value is 7)
        8 -> println(value is 8)
    }
}
```
`when` akan mencocokan semua argumen yang berada di setiap branch secara berurutan sampai salah satu kondisi terpenuhi. Di dalam `when` kita juga bisa menambahkan *branch* `else` seperti berikut:
```kotlin
fun main() {
    val value = 7

    when(value) {
        6 -> println(value is 6)
        7 -> println(value is 7)
        8 -> println(value is 8)
        else -> println("Failed)
    }
}
```
`when` juga memungkinkan kita untuk memeriksa *instance* dengan tipe data tertentu dari sebuah objek menggunakan `is` atau `!is`.
Contoh :
```kotlin
fun main() {
    val anyType : Any = 100L
    when(anyType) {
        is Long -> println("The value is long")
        is String -> println("The value is string")
        else -> println("Undefined")
    }
}
```
Selain itu, when expression juga bisa kita gunakan untuk memeriksa nilai yang terdapat pada sebuah **Range** atau **Collection**. Range sendiri merupakan salah satu tipe data yang unik di mana kita dapat menentukan nilai awal dan nilai akhir.
```kotlin
fun main() {
    val value = 15
    val ranges = 10..50
    when(value) {
        is ranges -> println("The value is in the range")
        !is ranges -> println("The value is outside the range")
        else -> println("Undefined")
    }
}
```

## While dan Do While
### - While
Contoh penulisan :
```kotlin
fun main () {
    var counter = 1
    while(counter <= 7) {
        println("Hello World!")
        counter++
    }
}
```

### - Do While
Contoh penulisan :
```kotlin
fun main() {
    var counter = 1
    do {
        prinln("Hello World)
        counter++
    } while (counter <= 7)
}
```
Saat menggunakan While dan Do While perhatikan _infinite loop_, yaitu kondisi dimana proses perulangan berlangsung terus menerus sampai aplikasi menjadi _crash_. 

## Range
Dengan menggunakan range kita dapat menentukan nilai awal dan nilai akhir pada range. Range direpresentasikan dengan operator `..` atau dengan fungsi `rangeTo()` dan `downTo()`.
Contoh :
```kotlin
val rangeInt = 1.rangeTo(10) //output 1 2 3 4 5 6 7 8 9 10
val downInt = 10.downTo(1) //output 10 9 8 7 6 5 4 3 2 1

fun main() {
    val dataRange = 10.downTo(1)
    if(7 in dataRange) {
        println("Value 7 is available)
    }
}
```

## For Loop
For dapat digunakan pada **Ranges, Collections, Arrays** dan apapun yang menjadi _interator_.
Contoh :
```kotlin
fun main() {
    //penggunaan for pada Ranges
    val ranges = 1..5
    for (i in ranges) {
        println("values is $i)
    }
}
```
Kita juga dapat mengakses `index` setiap elemen yang ada pada ranges dengan memanfaatkan fungsi `withIndex()` seperti berikut :
```kotlin
fun main() {
    val data = 1.rangeTo(10) step 3
    for ((index, value) in ranges.withIndex()) {
        println("value = $value, index = $index")
    }

    /*
    output : 
    value = 1, index = 0
    value = 4, index = 1
    value = 7, index = 2
    value = 10, index = 3
    */
}
```
Kita menggunakan kata kunci `for` untuk memulai proses perulangan. Untuk tujuan yang sama kita juga bisa memanfaatkan salah satu ekstensi pada kotlin yaitu ` forEach`. Contohnya seperti berikut :
```kotlin
fun main() {
    val data = 1.rangeTo(10) step 3
    data.forEach { value -> 
        println("value is $value")
    }
}
```
`forEach` pada kode diatas merupakan sebuah **lambda expression** yang hanya memiliki satu argumen yaitu nilai tunggal yang dicakup pada `data/ranges`. Jika kita mendapatkan index dari tiap nilai yang dicakup kita bisa menggunakan ekstensi `forEachIndexed` seperti berikut :
```kotlin
fun main() {
    val data = 1.rangeTo(10) step 3
    data.forEachIndexed { index, value -> 
        println("value = $value, index = $index")
    }
}
```
Jika kita hanya ingin menggunakan argumen index, maka kita bisa mengubah argumen value menjadi **`_`** seperti berikut:
```kotlin
fun main() {
    val data = 1.rangeTo(10) step 3
    data.forEachIndexed { index, _ -> 
        println("index = $index")
    }
}
```

## Break dan Continue
Continue digunakan untuk melewatkan proses iterasi dan lanjut dengan proses iterasi berikutnya. Sementara itu, Break digunakan untuk menghentikan proses iterasi.

Berikut adalah contoh proses iterasi pada kode di atas. Kita akan coba melewatkannya jika nilai yang dihasilkan adalah null.
```kotlin
fun main() {
    val listOfInt = listOf(1,2,3, null, 5, null, 7)
    for (i in listOfInt) {
        if(i == null) continue
        print(i)
    }
}
```
Pada kode diatas kita menggunakan kata kunci `continue`. Jika hasil evaluasi _expression_ yang diberikan bernilai **true**, maka proses iterasi akan dilewatkan dan lanjut pada proses iterasi berikutnya.

Contoh penggunaan **break**
```kotlin
fun main() {
    val listOfInt = listOf(1,2,3, null, 5, null, 7)
    for (i in listOfInt) {
        if(i == null) break
        print(i)
    }
}
```
Penggunaan `break` pada kode diatas, akan menghentikan proses _looping_ jika bertemu dengan nilai **null**

### Break dan Continue Labels
Pada kotlin, sebuah _expression_ dapat ditandai dengan sebuah label. Label pada kotlin memiliki sebuah _identifier_ yang diikut dengan tanda **`@`**. Contoh dari sebuah label adalah **foo@** dan **bar@**.

Untuk melabeli sebuah _expression_, kita cukup menempatkan label didepannya, seperti berikut :
```kotlin
fun main() {
    loop@ for (i in 1..10) {
        println("Outside Loop")

        for (j in 1..10) {
            println("Inside loop")
            if(j > 5) break@loop
        }
    }
}
```
Pada kode diatas, `break` yang sudah ditandai dengan label akan dilompati ke titik awal proses perulangan yang sudah ditandai dengan label. break akan menghentikan proses perulangan terluar dari dalam proses perulangan, di mana break tersebut dipanggil.

## Data _Class_