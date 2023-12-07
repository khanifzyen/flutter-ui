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

Dalam contoh code dibawah ini, saya ingin memperlihatkan bagaimana kita dapat membuat tampilan list ke samping dan jumlah kontennya melebihi lebar layar dan itu tidak masalah, karena dia dapat di scroll ke samping. Kita membuat widget listview dimana childnya adalah list dari categories.

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

## GridView

## Padding

## AspectRatio

## Center

## Expanded

## SizedBox

## Wrap

## Stack
