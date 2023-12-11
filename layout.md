# Layout

[Kembali](README.md)

Di dalam bab Layout dasar, akan dipelajari Widget-widget berikut:

- [Column](#column)
- [Row](#row)
- [ListView](#listview)
- [GridView](#gridview)
- [Padding](#padding)
- [AspectRatio](#aspectratio)
- [Center](#center)
- [Expanded](#expanded)
- [SizedBox](#sizedbox)
- [Wrap](#wrap)
- [Stack](#stack)

## Column

Widget `Column` ini menempatkan widget-widget anaknya pada sumbu vertikal dengan batasan ruang yang sudah ditentukan. Dibawah ini mindmap dari widget Column. `mainAxisAligment` adalah alignment yang mengikuti sumbu axis nya column artinya sumbu vertikal. Sedang `crossAxisAligment` adalah sebaliknya yaitu aligment yang mengikuti sumbu horizontal.

```
Column
│───mainAxisAlignment
|   |───MainAxisAlignment
|   |   │───.start
|   |   │───.center
|   |   │───.end
|   |   │───.spaceAround
|   |   │───.spaceBetween
|   |   │───.spaceEvenly
│───children
|   |───List<Widget>
│───crossAxisAlignment
|   |───CrossAxisAlignment
|   |   │───.baseline
|   |   │───.start
|   |   │───.center
|   |   │───.end
|   |   │───.stretch
```

Dalam contoh code dibawah ceritanya saya ingin membuat tampilan susun dari atas ke bawah. Kita gunakan widget Column lalu cross alignmentnya saya set start supaya rata kiri. Dan setelah itu childrennya pertama saya isi text, lalu jarak 10px, lalu bawahnya text lagi berupa harga.

```dart
...
      body: Container(
        padding: const EdgeInsets.all(10.0),
        child: const Column(
          children: [
            Text(
              "Stylish Chair",
              style: TextStyle(
                color: Colors.black,
                fontSize: 14.0,
                fontWeight: FontWeight.w500,
              ),
            ),
            SizedBox(
              height: 10,
            ),
            Text(
              "Rp. 350.000",
              style: TextStyle(
                fontSize: 20,
                color: Color(0xFF9A9390),
                fontWeight: FontWeight.w400,
                letterSpacing: 1,
              ),
            ),
          ],
        ),
      ),
...
```

Output:

![Gambar 14. Widget Column](img/14%20column.png)

Gambar 14. Widget Column

Nantinya dapat kita implementasi seperti contoh berikut dalam menata tampilan title product dan harga serta rating.

![Gambar 15. Implementasi Column](img/15%20implementasi%20column.PNG)

Gambar 15. Implementasi Column

Baca Dokumentasi Resmi:

- [Column.](https://api.flutter.dev/flutter/widgets/Column-class.html)

## Row

Widget `Row` ini menempatkan widget-widget anaknya pada sumbu horizontal dengan batasan ruang yang sudah ditentukan, kebalikan dari column. Dibawah ini adalah mindmap dari widget `Row`. `mainAxisAlignment` adalah alignment yang mengikuti sumbu axis nya row artinya sumbu horizontal. Sedang `crossAxisAlignment` adalah sebaliknya yaitu aligment yang mengikuti sumbu vertikal.

```
Row
│───mainAxisAlignment
|   |───MainAxisAlignment
|   |   │───.start
|   |   │───.center
|   |   │───.end
|   |   │───.spaceAround
|   |   │───.spaceBetween
|   |   │───.spaceEvenly
│───children
|   |───List<Widget>
│───crossAxisAlignment
|   |───CrossAxisAlignment
|   |   │───.baseline
|   |   │───.start
|   |   │───.center
|   |   │───.end
|   |   │───.stretch
```

Contoh kode dibawah ceritanya kita akan membuat tampilan header dibagian sebelah kiri ada icon back, ditengah ada title dan disebelah kanan ada icon share.

```dart
...
      body: Container(
        padding: const EdgeInsets.all(10.0),
        child: Row(
          mainAxisAlignment: MainAxisAlignment.spaceBetween,
          children: [
            Container(
              decoration: BoxDecoration(
                borderRadius: BorderRadius.circular(12),
                color: Colors.grey,
              ),
              child: IconButton(
                icon: const Icon(Icons.arrow_back),
                onPressed: () {},
              ),
            ),
            const Text(
              "Detail",
              style: TextStyle(
                fontSize: 24,
                fontWeight: FontWeight.normal,
              ),
            ),
            IconButton(
              icon: const Icon(
                Icons.share,
                size: 32,
              ),
              onPressed: () {},
            ),
          ],
        ),
      ),
...
```

Output:

![Gambar 16. Widget Row](img/16%20row.png)

Gambar 16. Widget Row

Nantinya dapat kita implementasi seperti contoh berikut dalam menata tampilan di detail product untuk headernya.

![Gambar 17. Implementasi Row](img/17%20implementasi%20row.PNG)

Gambar 17. Implementasi Row

Baca Dokumentasi Resmi:

- [Row.](https://api.flutter.dev/flutter/widgets/Row-class.html)

## ListView

ListView pada dasarnya adalah sebuah Kolom dengan perilaku bergulir atau scroll karena menempatkan satu atau lebih banyak anak dalam sumbu vertikal, secara berurutan. Widget ini sangat banyak digunakan karena memberikan keunggulan untuk menggulirkan konten ketika jumlah content lebih besar dari ukuran layar.Untuk membuat listview scroll ke samping, teman-teman bisa menggunakan properties scollDirection Axis.horizontal seperti yang terlihat di mindmap

```
ListView
│───children
|   |───List<Widget>
│───scrollDirection
|   |───Axis
|   |   │───.horizontal
|   |   │───.vertical
│───padding
|   |───EdgeInset
|   |   │───.all()
|   |   │───.only()
|   |   │───.symmetric
│───reverse
|   |───bool
│───pyshics
|   |───NeverScrollableScrollPhysics()
│───shrinkWrap
|   |───bool
|   |   │───true
|   |   │───false
```

Dalam contoh code dibawah ini, saya ingin memperlihatkan bagaimana kita dapat membuat tampilan list ke samping dan jumlah kontennya melebihi lebar layar dan itu tidak masalah, karena dia dapat di scroll ke samping. Kita membuat widget ListView dimana childnya adalah list dari categories.

```dart
import 'package:flutter/material.dart';

class MyListView extends StatelessWidget {
  MyListView({super.key});

  final List<String> categories = [
    "All",
    "Living Room",
    "Bedroom",
    "Dining Room",
    "Kitchen"
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Coding Flutter - ListView"),
      ),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.spaceBetween,
        children: [
          SizedBox(
            height: 35,
            child: CustomListView(
              categories: categories,
              scrollDirection: Axis.horizontal,
            ),
          ),
          SizedBox(
            height: 200,
            child: CustomListView(
              categories: categories,
              scrollDirection: Axis.vertical,
            ),
          ),
          SizedBox(
            height: 200,
            child: CustomListView(
              categories: categories,
              scrollDirection: Axis.vertical,
            ),
          ),
        ],
      ),
    );
  }
}

class CustomListView extends StatelessWidget {
  const CustomListView({
    super.key,
    required this.categories,
    required this.scrollDirection,
  });

  final List<String> categories;
  final Axis scrollDirection;

  @override
  Widget build(BuildContext context) {
    return ListView(
      scrollDirection: scrollDirection,
      children: List.generate(
        categories.length,
        (index) {
          return GestureDetector(
            onTap: () {},
            child: AnimatedContainer(
              duration: const Duration(milliseconds: 150),
              decoration: BoxDecoration(
                borderRadius: BorderRadius.circular(20),
                color: Colors.grey,
              ),
              padding: const EdgeInsets.symmetric(
                horizontal: 24,
                vertical: 8,
              ),
              margin: const EdgeInsets.symmetric(horizontal: 2, vertical: 2),
              child: Text(categories[index],
                  textAlign: TextAlign.center,
                  style: const TextStyle(
                    fontSize: 12,
                    color: Colors.black,
                    fontWeight: FontWeight.w500,
                    letterSpacing: 1,
                  )),
            ),
          );
        },
      ),
    );
  }
}

```

Output:

![Gambar 18. Widget ListView](img/18%20listview.png)

Gambar 18. Widget ListView

Nantinya dapat kita implementasi seperti contoh berikut dalam menata tampilan untuk memilih kategori furniture.

![Gambar 19. Implementasi ListView](img/19%20implementasi%20listview.PNG)

Gambar 19. Implementasi ListView

Baca Dokumentasi Resmi:

- [ListView.](https://api.flutter.dev/flutter/widgets/ListView-class.html)
- [GestureDetector.](https://api.flutter.dev/flutter/widgets/GestureDetector-class.html)
- [AnimatedContainer.](https://api.flutter.dev/flutter/widgets/Row-class.html)

## ListView.builder

`ListView.builder()` sangat berguna ketika list harus dibuat berdasarkan data yang lebih banyak. Dokumentasi resmi Flutter menyarankan untuk menggunakan konstruktor bernama `builder()` ketika sumber data adalah data yang panjang karena secara efisien widget ini akan mengelola anak-anaknya ketika dipanggil dan hanya akan di build ketika terlihat dilayar. Jadi, daripada secara manual mengisi ListView yang panjang dengan loop for, gunakan `builder()` yang lebih efisien.

```
ListView.builder()
│───itemCount
│───itemBuilder
|   |───context
|   |───index
```

Dibawah ini adalah contoh tampilan yang menggunakan listview builder. Untuk data yang panjang seperti data dari database sangatlah cocok menggunakan widget ini karena data akan diproses build ketika data di tampilan di layar akibat dari scroll kebawah atau keatas.

```dart
...
    return ListView.builder(
      itemCount: categories.length,
      itemBuilder: (BuildContext context, int index) {
        return GestureDetector(
          onTap: () {},
          child: AnimatedContainer(
            duration: const Duration(milliseconds: 150),
            decoration: BoxDecoration(
              borderRadius: BorderRadius.circular(20),
              color: Colors.grey,
            ),
            padding: const EdgeInsets.symmetric(
              horizontal: 24,
              vertical: 8,
            ),
            margin: const EdgeInsets.symmetric(horizontal: 2, vertical: 2),
            child: Text(categories[index],
                textAlign: TextAlign.center,
                style: const TextStyle(
                  fontSize: 12,
                  color: Colors.black,
                  fontWeight: FontWeight.w500,
                  letterSpacing: 1,
                )),
          ),
        );
      },
    );
...
```

Untuk tampilan ListView.builder sama seperti menggunakan ListView biasa, .scrollDirection nya vertikal atau dari atas ke bawah. Untuk data sedikit mungkin tidak terlalu terlihat perbedaannya, namun untuk data yang banyak akan terlihat lebih efisien menggunakan ListView.builder

## GridView.builder

Widget GridView secara otomatis menempatkan elemen dalam grid dan jumlah kolom ditentukan oleh nilai yang diteruskan ke crossAxisCount. Kode ini dikatakan responsif karena ketika lebar layar berubah, maka UI akan diatur ulang.

```
GridView.builder()
│───itemCount
│───itemBuilder
|   |───context
|   |───index
│───gridDelegate
|   |───SliverGridDelegateWithFixedCrossAxisCount()
|   |───SliverGridDelegateWithMaxCrossAxisCount()
```

Kode disamping kita menggunakan gridview untuk membuat tampilan 2 column yang akan berisi container dengan bentuk yang siap menampung tampilan product.

```dart
...
      body: Expanded(
        child: GridView.builder(
            gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
                crossAxisCount: 2),
            itemCount: 50,
            itemBuilder: (BuildContext context, int index) {
              return Container(
                height: 100,
                width: double.infinity,
                margin: const EdgeInsets.all(5),
                decoration: BoxDecoration(
                  color: Colors.blue,
                  borderRadius: BorderRadius.circular(20),
                  boxShadow: [
                    BoxShadow(
                      color: Colors.black.withOpacity(0.2),
                      offset: Offset.zero,
                      blurRadius: 15,
                    ),
                  ],
                ),
                child: Center(
                    child: Text(
                  (index + 1).toString(),
                  style: const TextStyle(
                    fontSize: 16,
                    color: Colors.white,
                  ),
                )),
              );
            }),
      ),
...
```

Output:

![Gambar 20. Widget GridView.builder](img/20%20gridview.png)

Gambar 20. Widget GridView.builder

Nantinya dapat kita implementasi seperti contoh berikut dalam menata tampilan untuk memilih kategori furniture.

![Gambar 21. Implementasi GridView.builder](img/21%20implementasi%20gridview.PNG)

Gambar 21. Implementasi GridView

Baca Dokumentasi Resmi:

- [GridView.](https://api.flutter.dev/flutter/widgets/GridView-class.html)

## Stack

Dengan Widget Stack, Anda dapat menumpuk widget dan memposisikannya dengan bebas di layar menggunakan widget Positioned. Bahkan jika childrennya ditempatkan di luar batas UI, tidak akan ada kesalahan sistem yang muncul, karena Stack tidak membatasi batas lebar dan tinggi.

```
Stack
│───alignment
|   |───Alignment
|   |   |───top
|   |   |   |───left
|   |   |   |───center
|   |   |   |───right
|   |   |───center
|   |   |   |───left
|   |   |   |───right
|   |   |───bottom
|   |   |   |───left
|   |   |   |───center
|   |   |   |───right
|   |───Alignment()
|   |   |───x
|   |   |   |───1
|   |   |   |   |───right
|   |   |   |───-1
|   |   |   |   |───left
|   |   |───y
|   |   |   |───1
|   |   |   |   |───bottom
|   |   |   |───-1
|   |   |   |   |───top
│───children
```

Seperti contoh code dibawah. Saya membuat tampilan menggunakan Stack dimana dibagian bawah saya mempunyai icon shopping cart dengan size 50, lalu diatasnya saya tumpuk dengan widget lingkaran dengan radius 10 dan background warna merah lalu didalamnya terdapat text angka 3.

```dart
...
      body: const Padding(
        padding: EdgeInsets.all(8.0),
        child: Stack(
          clipBehavior: Clip.none,
          children: [
            Icon(
              Icons.shopping_cart,
              size: 50,
            ),
            Positioned(
              top: -4,
              right: -4,
              child: CircleAvatar(
                radius: 10,
                backgroundColor: Colors.red,
                child: Text(
                  "1",
                  style: TextStyle(
                    fontSize: 10,
                    color: Colors.white,
                  ),
                ),
              ),
            ),
          ],
        ),
      ),
...
```

Output:

![Gambar 22. Widget Stack](img/22%20stack.png)

Gambar 22. Widget Stack

Baca Dokumentasi Resmi:

- [Stack.](https://api.flutter.dev/flutter/widgets/Stack-class.html)

## Padding

Padding widget melakukan persis seperti namanya, menambahkan padding atau ruang kosong di sekitar widget atau sekelompok widget. Kita dapat menerapkan padding di sekitar widget apapun dengan menempatkannya sebagai child dari widget Padding.

```
Padding
│───EdgeInsets
|   |───.only()
|   |───.symmetric()
|   |───.all()
|   |───.fromLTRB()
```

Seperti contoh dibawah. Text categories saya bungkus dengan widget padding supaya mempunyai jarak dengan area luarnya. Disini saya set jarak dari text ke arah kiri sejauh 20px, keatas 30px dan ke bawah 40px.

```dart
...
      body: Container(
        height: 500,
        width: 300,
        margin: const EdgeInsets.all(10),
        decoration: BoxDecoration(
          border: Border.all(),
        ),
        child: const Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Padding(
              padding: EdgeInsets.only(
                left: 20.0,
                top: 30,
                bottom: 40,
              ),
              child: Text(
                "Categories",
                style: TextStyle(
                  fontSize: 16,
                  fontWeight: FontWeight.w500,
                ),
              ),
            ),
          ],
        ),
      ),
...
```

Output:

![Gambar 23. Widget Padding](img/23%20padding.png)

Gambar 23. Widget Padding

Baca Dokumentasi Resmi:

- [Padding.](https://api.flutter.dev/flutter/widgets/Padding-class.html)

## AspectRatio

Widget yang mencoba mengubah ukuran child ke rasio tinggi dan lebar tertentu.Widget terlebih dahulu mencoba rasio lebarnya terlebihdahulu sesuai yang sudah diatur. Ketinggian widget ditentukan dengan menerapkan rasio aspek yang diberikan ke lebar, dinyatakan sebagai rasio lebar terhadap tinggi.

```
AspectRatio
│───aspectRatio
│───child
```

Seperti contoh code dibawah. Saya memasukkan Container dengan color blue kedalam widget AspectRatio dengan rasio lebar 180 dan tingginya 240. Dan widget ini akan otomatis mengikuti lebar dan tinggi layar dengan rasio yang sama.

```dart
...
      body: AspectRatio(
        aspectRatio: 180 / 240,
        child: Container(
          color: Colors.red,
        ),
      ),
...
```

Output:

![Gambar 24. Widget AspectRatio](img/24%20aspectratio.png)

Gambar 24. Widget AspectRatio

Mungkin tidak begitu terlihat hasil rasionya, namun ketika widget ini dimasukan ke dalam gridview, maka akan cocok sekali karena konten yg ada di dalam gridview nanti nya akan memiliki rasio yg sama dan fleksible mengikuti lebar dan tinggi layar device.

![Gambar 25. Implementasi AspectRatio](img/24%20implementasi%20aspectratio.PNG)

Gambar 25. Implementasi AspectRatio

Baca Dokumentasi Resmi:

- [AspectRatio.](https://api.flutter.dev/flutter/widgets/AspectRatio-class.html)

## Center

Widget ini akan memusatkan anak nya kediri dia, yang itu artinya widget anaknya akan ada ditengah-tengah widget disekitarnya karena sifatnya yang dapat memenuhi ruang di sekitarnya. Pada contoh di bawah saya bungkus button add to
cart dengan center sehingga tampilannya bisa berada ditengah layar.

```dart
...
        child: Column(
          children: [
            Center(
              child: ElevatedButton(
                onPressed: () {},
                style: ElevatedButton.styleFrom(
                  backgroundColor: Colors.blue,
                  shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(20.0),
                  ),
                  shadowColor: Colors.grey[20],
                  elevation: 5.0,
                ),
                child: Text(
                  "Add To Cart".toUpperCase(),
                  style: const TextStyle(
                      fontSize: 20.0,
                      fontWeight: FontWeight.w500,
                      color: Colors.white),
                ),
              ),
            ),
          ],
        ),
...
```

Output:

![Gambar 26. Widget Center](img/25%20center.png)

Gambar 26. Widget Center

![Gambar 27. Implementasi Center](img/26%20implementasi%20center.PNG)

Gambar 27. Implementasi Center

Baca Dokumentasi Resmi:

- [Center.](https://api.flutter.dev/flutter/widgets/Center-class.html)

## Expanded

Widget yang memperluas childnya dari Row, Column, atau Flex sehingga child tersebut mengisi ruang yang tersedia. Dengan expanded widget child dari Row, Column, atau Flex dapat memperluas diri untuk mengisi ruang yang tersedia di sepanjang sumbu utamanya (misal secara horizontal untuk Baris/row atau vertikal untuk Kolom). Jika beberapa child diperluas, ruang yang tersedia dibagi di antara mereka menurut faktor flex.

```
Expanded
│───flex
│───child
```

Expanded harus berada di bawahnya row atau column, dalam contoh kode disamping, expanded ada di dalam row dan membungkus text list checklist, yg artinya text ini akan mengisi sisa area yg ada. Yg akhirnya icon arrow back dan check akan ada di sebelah kiri dan kanan.

```dart
...
     body: Container(
        margin: const EdgeInsets.all(10.0),
        child: const Column(
          children: [
            Row(
              children: [
                Icon(
                  Icons.arrow_back_ios,
                ),
                Expanded(
                  child: Padding(
                    padding: EdgeInsets.all(8.0),
                    child: Text(
                      "List checklist ",
                      style: TextStyle(fontSize: 16),
                    ),
                  ),
                ),
                Icon(
                  Icons.check,
                  color: Colors.blue,
                )
              ],
            ),
          ],
        ),
      ),
...
```

Output:

![Gambar 28. Widget Expanded](img/27%20expanded.png)

Gambar 28. Widget Expanded

Bisa dilihat bahwa list checklist memenuhi area yang ada sehingga icon check berada di paling ujung kanan.

Baca Dokumentasi Resmi:

- [Expanded.](https://api.flutter.dev/flutter/widgets/Expanded-class.html)

## SizedBox

Sebuah kotak dengan ukuran tertentu. Jika diberi child, widget ini memaksanya child untuk memiliki lebar dan/atau tinggi tertentu. Nilai ini akan diabaikan jika induk widget ini mempunyai ukuran sendiri, maka sizedbox mengikuti ukuran parent nya. Hal ini dapat diatasi dengan membungkus child dari SizedBox ke dalam sebuah widget yang memungkinkan ukurannya sesuai dengan ukuran induknya, seperti Center atau Align.

```
SizedBox
│───height
│───width
│───child
```

Untuk contoh dibawah ini, SizedBox dipakai untuk membuat jarak antar text dengan membuat kotak kosong dengan tinggi 4 dan tinggi 2.

```dart
...
      body: const Padding(
        padding: EdgeInsets.all(20.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              "Size",
              style: TextStyle(
                  fontSize: 18,
                  color: Colors.grey,
                  fontWeight: FontWeight.bold),
            ),
            SizedBox(
              height: 4,
            ),
            Text(
              "Height 120cm",
              style: TextStyle(
                  fontSize: 16,
                  color: Colors.grey,
                  fontWeight: FontWeight.normal),
            ),
            SizedBox(
              height: 2,
            ),
            Text(
              "Width 80cm",
              style: TextStyle(
                  fontSize: 16,
                  color: Colors.grey,
                  fontWeight: FontWeight.normal),
            ),
          ],
        ),
      ),
...
```

Output:

![Gambar 29. Widget SizedBox](img/28%20sizedbox.png)

Gambar 29. Widget SizedBox

![Gambar 30. Implementasi SizedBox](img/29%20implementasi%20sizedbox.PNG)

Gambar 30. Implementasi SizedBox

Baca Dokumentasi Resmi:

- [SizedBox.](https://api.flutter.dev/flutter/widgets/SizedBox-class.html)

## Wrap

Widget yang menampilkan childnya dalam beberapa urutan horizontal atau vertikal. Sebuah wrap widget meletakkan setiap child dan mencoba untuk menempatkan childnya berdekatan dengan child sebelumnya di sumbu utama, diberikan arahnya, dan meninggalkan ruang jarak di antaranya. Jika tidak ada cukup ruang untuk memasukkan childnya, wrap membuat lintasan baru yang berdekatan dengan child yang sudah ada di sumbu silang.

```
Wrap
│───direction
│───alignment
|   │───mainAxis
│───runAlignment
|   │───crossAxis
│───spacing
|   │───mainAxis
│───runSpacing
|   │───crossAxis
```

Contoh kode dibawah ini memperlihatkan list widget lingkaran dengan warna dibungkus dengan wrap dan hasilnya ketika kontennya tadi menabrak lebar layar, maka konten selanjutnya akan ditempatkan paling dekat dengan temannya namun disisi cross dari sumbu utama alias ketika ke samping maka next contentnya akan ada dibawahnya.

```dart
import 'package:flutter/material.dart';

class MyWrap extends StatelessWidget {
  MyWrap({super.key});

  final List<Color> colors = [
    Colors.red,
    Colors.green,
    Colors.blue,
    Colors.yellow,
    Colors.orange,
    Colors.purple,
    Colors.pink,
    Colors.teal,
    Colors.cyan,
    Colors.indigo,
    Colors.brown,
    Colors.grey,
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Coding Flutter - Wrap"),
      ),
      body: Padding(
        padding: const EdgeInsets.all(8),
        child: Column(
          children: [
            Wrap(
              spacing: 20,
              runSpacing: 10,
              children: colors.map((color) {
                return InkWell(
                  onTap: () {},
                  child: Container(
                    width: 45,
                    height: 45,
                    decoration: BoxDecoration(
                      border: Border.all(width: 3, color: Colors.grey),
                      color: color,
                      shape: BoxShape.circle,
                      boxShadow: [
                        BoxShadow(
                            color: Colors.black.withOpacity(0.1),
                            blurRadius: 15,
                            offset: Offset.zero),
                      ],
                    ),
                  ),
                );
              }).toList(),
            ),
          ],
        ),
      ),
    );
  }
}
```

Output:

![Gambar 31. Widget Wrap](img/30%20wrap.png)

Gambar 31. Widget Wrap

Baca Dokumentasi Resmi:

- [Wrap.](https://api.flutter.dev/flutter/widgets/Wrap-class.html)

# [Materi Selanjutnya: Form](form.md)
