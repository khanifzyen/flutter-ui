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

## ListView

## GridView

## Padding

## AspectRatio

## Center

## Expanded

## SizedBox

## Wrap

## Stack
