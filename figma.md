# Figma

[Kembali](navigator.md)

Daftar Isi:

1. [Feature first architecture](#feature-first-architecture)
2. [Mengekspor Assets dari Figma](#mengekspor-assets-dari-figma)
3. [Pembuatan Fitur Home](#pembuatan-fitur-home)
   1. [Persiapan Library dan Asset](#persiapan-library-dan-asset)
   2. [Pembuatan AppBar](#pembuatan-appbar)
   3. [Pembuatan Headline](#pembuatan-headline)
   4. [Pembuatan Daftar Category](#pembuatan-daftar-category)
   5. [Pembuatan Recommended Furnitures](#pembuatan-recommended-furnitures)
   6. [Pembuatan Bottom Navigation Bar](#pembuatan-bottom-navigation-bar)
4. [Pembuatan Fitur Detail](#pembuatan-fitur-detail)
   1. [Pembuatan AppBar Detail](#pembuatan-appbar-detail)
   2. [Pembuatan Container Detail](#pembuatan-container-detail)
   3. [Pembuatan Nama Produk Harga Detail](#pembuatan-nama-produk-harga-detail)
   4. [Pembuatan Select Color Detail](#pembuatan-select-color-detail)
   5. [Pembuatan Select Quantity Detail](#pembuatan-select-quantity-detail)
   6. [Pembuatan Tombol Add to Cart Detail](#pembuatan-tombol-add-to-cart-detail)

Figma adalah tool desain berupa website dan tersedia versi desktop yang terhubung dengan cloud sehingga bisa digunakan kapanpun dan dimanapun melalui internet. Tool ini berbasis vector, sehingga akan lebih cocok untuk mendesain UI website atau mobile dan aset ilustrasi. Aplikasi ini sangat cocok untuk kolaborasi pengembangan aplikasi dimana UI/UX designer membuat design di figma lalu developer akan menulis kode berdasarkan UI/UX final yang sudah disepakati bersama dan membuatnya sesuai roles yang ada di figma

Teman-teman tinggal register lalu login, didalamnya temen temen dapat mencari contoh design di figma community. Atau bisa juga meminta temen yg punya design figma untuk share urlnya, nanti otomatis dibisa lihat design dari temennya tersebut.

Link Figma untuk design Furniture Shop:

https://www.figma.com/file/U1OKbGtchtzpxJd7jWAXxI/furniture-shop?type=design&node-id=0-1&mode=design&t=2A5lLHV0GKb1uYn2-0

Setelah itu klik Duplicate to your draft, agar teman-teman bisa mengedit di draft project masing-masing

![Gambar 46. Duplicate to your draft](img/46%20figma%20duplicate%20to%20your%20draft.png)

Gambar 46. Duplicate to your draft

## Feature first architecture

Feature-first adalah pendekatan dalam struktur proyek Flutter di mana setiap fitur aplikasi memiliki direktori sendiri yang berisi semua lapisan yang relevan. Misalnya, jika Anda memiliki fitur ‘login’, Anda akan memiliki direktori ‘login’ yang berisi semua file yang relevan untuk fitur tersebut, seperti widget, state, controller, services, models, repositories, data sources, dan DTO (data transfer objects).

Berikut adalah beberapa poin penting tentang arsitektur feature-first:

- Memudahkan navigasi kode: Semua kode yang relevan untuk suatu fitur tertentu ditempatkan dalam satu direktori, membuatnya lebih mudah untuk menavigasi dan memahami bagian kode yang berhubungan.

- Meningkatkan modularitas: Dengan mengelompokkan kode berdasarkan fitur, Anda dapat memastikan bahwa setiap bagian kode Anda dapat berfungsi secara independen dari yang lain. Ini juga memudahkan pengujian dan pemeliharaan kode.

- Mengurangi kompleksitas: Dengan memisahkan kode Anda menjadi fitur-fitur yang berbeda, Anda dapat mengurangi kompleksitas keseluruhan aplikasi Anda dan membuatnya lebih mudah untuk dipahami.

![Gambar 47. Project Figma Furniture Shop](img/47%20figma%20furniture%20shop.PNG)

Gambar 47. Project Figma Furniture Shop

Pada project figma Furniture Shop ini, terdiri dari dua halaman, yaitu Home dan Detail, maka akan kita buat dua fitur, sehingga struktur foldernya menjadi seperti berikut

- features
  - home
    - pages
      - home_page.dart
    - widgets
      - app_bar_home.dart
      - category_home.dart
      - recommended_furniture_home.dart
      - bottom_navigation_bar_home.dart
  - detail
    - pages
      - detail_page.dart
    - widgets
      - app_bar_detail.dart
      - container_detail.dart
      - nama_produk_harga_detail.dart
      - select_color_detail.dart
      - select_quantity_detail.dart
      - add_to_cart_detail.dart

Ini adalah rancangan awal, dengan membreakdown widget menjadi bagian yang lebih kecil. Seiring berjalannya waktu, widget-widget diatas bisa bertambah atau berkurang.

## Mengekspor Assets dari Figma

Untuk semua icon dan gambar, anda bisa ekspor satu satu manual dari figma. Misal untuk AppBar pada HomePage(), terdiri dari icon hamburger, dan sebelah kanan terdapat icon search. Walaupun di Flutter sudah disediakan icon, tentu kita sebagai seorang programmer mengikuti apa yang sudah didesain oleh desainer UI/UX sehingga kita akan menggunakan icon yang berada di Figma. Untuk cara ekspor yaitu klik pada icon, kemudian pada property ada tombol Export. Khusus icon pilih format SVG, untuk image pilih PNG. Simpan di lib/assets/icon dan lib/assets/image

![Gambar 48. Proses export assets icon dari figma](img/48%20figma%20export%20icon.PNG)

Gambar 48. Proses export assets icon dari figma

Lakukan hal yang sama untuk gambar/image.

![Gambar 49. Proses export assets image dari figma](img/49%20figma%20export%20image.PNG)

Gambar 49. Proses export assets image dari figma

Sehingga hasil akhirnya adalah sebagai berikut:

![Gambar 50. Hasil export assets image dan icon dari figma](img/50%20figma%20hasil%20export%20icon%20dan%20image.PNG)

Gambar 50. Hasil export assets image dan icon dari figma

## Pembuatan Fitur Home

Fitur Home terdiri dari satu halaman yaitu `HomePage()`, kemudian dipecah-pecah menjadi beberapa widget diantaranya:

- `app_bar_home.dart`: widget untuk menampilkan title dan actions pada AppBar bagian atas
- `category_home.dart`: widget untuk menampilkan daftar kategori dalam bentuk ListView yang discroll secara horizontal
- `recommended_furniture_home.dart`: widget untuk menampilkan daftar item furniture dalam bentuk GridView
- `bottom_navigation_bar_home.dart`: widget untuk menampilkan BottomNavigationBar dengan custom activeIcon

### Persiapan library dan asset

Sebelum anda membuat halaman `HomePage()`, anda perlu menambahkan dua library pada `pubspec.yaml` yaitu:

- `flutter_svg`: library untuk dapat menggunakan file svg sebagai asset
- `google_fonts`: library untuk dapat menggunakan font public di repository google font

Dan tambahkan pula asset icon dan image, sehingga di `pubspec.yaml` ada tambahan sebagai berikut:

```yaml
dependencies:
  ...
  flutter_svg: ^2.0.9  ## gunakan versi terbaru
  google_fonts: ^6.1.0 ## gunakan versi terbaru
  ...
flutter:
  ...
  assets:
    - assets/icons/
    - assets/images/furniture/
  ...
```

### Pembuatan AppBar

AppBar disini menggunakan icon menu dan icon search, kemudian title menggunakan font Poppins dengan size 16, fontweight semibold, color dengan kode hex 4A4543, sehingga kodenya adalah seperti berikut:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';
import 'package:google_fonts/google_fonts.dart';

class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.transparent,
        leading: IconButton(
          onPressed: () {},
          icon: SvgPicture.asset('assets/icons/menu.svg'),
        ),
        title: Center(
            child: Text(
          "Home",
          style: GoogleFonts.poppins(
            textStyle: const TextStyle(
                fontWeight: FontWeight.w600,
                fontSize: 16,
                color: Color(0xff4A4543)),
          ),
        )),
        actions: [
          IconButton(
            onPressed: () {},
            icon: SvgPicture.asset('assets/icons/search.svg'),
          ),
        ],
      ),
    );
  }
}
```

Output:

![Gambar 51. Perbandingan desain AppBar di Figma dengan kode akhir di Flutter](img/51%20appbar%20figma%20dibandingkan%20appbar%20flutter.PNG)

Gambar 51. Perbandingan desain AppBar di Figma dengan kode AppBar di Flutter

### Pembuatan headline

Selanjutnya adalah terdapat headline 'Discover the most modern furniture' memiliki jarak 30 dari AppBar dan jarak 14 dari tepi. Untuk style dari headline tersebut adalah font Poppins dengan size 22, fontweight medium, color dengan kode hex 4A4543, sehingga kodenya adalah seperti berikut:

```dart
...
      body: Padding(
        padding: const EdgeInsets.symmetric(horizontal: 14.0),
        child: Column(
          children: [
            const SizedBox(height: 20),
            SizedBox(
              width: 226,
              child: Text(
                'Discover the most modern furniture',
                style: GoogleFonts.poppins(
                  textStyle: const TextStyle(
                      fontWeight: FontWeight.w500,
                      fontSize: 22,
                      color: Color(0xFF4A4543)),
                ),
              ),
            ),
          ],
        ),
      ),
...
```

**Edit:** karena default AppBar dan body sudah memiliki jarak, maka SizedBox awal diberi height 20.

Output:

![Gambar 52. Body headline setelah AppBar di Figma dengan kode final di Flutter](img/51%20perbandingan%20body%20headline.PNG)

Gambar 52. Perbandingan desain AppBar di Figma dengan kode AppBar di Flutter

### Pembuatan daftar Category

Selanjutnya terdapat kategori furniture dengan nilai 'All, Living Room, Bedroom, Dining Room, Kitchen' yang memiliki jarak dari headline 30, font menggunakan Poppins, fontweight medium, fontsize 12, dan color dengan kode hex 4A4543. Disini sudah mulai agak kompleks karena ada state dan tampilan yang berubah ketika kategori sedang aktif atau tidak aktif, maka perlu dipisahkan menjadi widget sendiri

```dart
import 'package:flutter/material.dart';
import 'package:google_fonts/google_fonts.dart';

class CategoryHome extends StatefulWidget {
  const CategoryHome({super.key});

  @override
  State<CategoryHome> createState() => _CategoryHomeState();
}

class _CategoryHomeState extends State<CategoryHome> {
  final List<String> _category = [
    'All',
    'Living Room',
    'Bedroom',
    'Dining Room',
    'Kitchen',
  ];

  int _selectedCategory = 0;

  void _onTapCategory(int index) {
    setState(() {
      _selectedCategory = index;
    });
  }

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      scrollDirection: Axis.horizontal,
      itemCount: _category.length,
      itemBuilder: (context, index) {
        return Padding(
          padding: const EdgeInsets.only(right: 17),
          child: InkWell(
              onTap: () => _onTapCategory(index),
              child: _selectedCategory == index
                  ? CategoryItem(
                      category: _category[index],
                      backgroundColor: const Color(0xFF9A9390),
                      fontColor: const Color(0xFFFFFFFF),
                    )
                  : CategoryItem(
                      category: _category[index],
                      backgroundColor: Colors.transparent,
                      fontColor: const Color(0xFF4A4543),
                    )),
        );
      },
    );
  }
}

class CategoryItem extends StatelessWidget {
  const CategoryItem({
    super.key,
    required this.category,
    required this.backgroundColor,
    required this.fontColor,
  });

  final String category;
  final Color backgroundColor;
  final Color fontColor;

  @override
  Widget build(BuildContext context) {
    return Container(
      padding: const EdgeInsets.symmetric(horizontal: 20, vertical: 5),
      decoration: BoxDecoration(
        borderRadius: const BorderRadius.all(Radius.circular(20)),
        color: backgroundColor,
      ),
      child: Center(
        child: Text(
          category,
          style: GoogleFonts.poppins(
            textStyle: TextStyle(
              fontWeight: FontWeight.w500,
              fontSize: 12,
              color: fontColor,
            ),
          ),
        ),
      ),
    );
  }
}
```

Kemudian pada `home_page.dart` memanggil `CategoryHome()`

```dart
...
            const SizedBox(height: 30),
            const SizedBox(
              height: 40,
              child: CategoryHome(),
            ),
...
```

Output:

![Gambar 53. Perbandingan daftar kategori](img/53%20perbandingan%20daftar%20kategori.PNG)

Gambar 53. Perbandingan daftar kategori di Figma dengan kode di Flutter

### Pembuatan Recommended Furnitures

Yang pertama adalah subjudul `Recommended Furniture` yang berjarak 30 dari daftar kategori,menggunakan font Poppins, fontweight medium, fontsize 16, dan color menggunakan 4A4543. Untuk subjudul ini tidak perlu dipisah, bisa digabung dengan `home_page.dart`.

```dart
...
        Text(
          "Recommended Furnitures",
          style: GoogleFonts.poppins(
              textStyle: const TextStyle(
            fontWeight: FontWeight.w500,
            fontSize: 16,
            color: Color(0xFF4A4543),
          )),
        ),
...
```

> **Catatan**: Nanti akan muncul banyak eror dikarenakan penggunaan keyword `const`diawal `Padding`, hapus saja dan beri `const` manual satu-satu pada list `children` di `Column`, karena penggunaan `GoogleFonts` tidak bisa dengan `const`

Selanjutnya dibawahnya adalah `GridView` yang memuat 4 produk dimana masing-masing dibungkus dalam sebuah Card. Oh iya, untuk warna dasar aplikasi bukan putih tetapi berwarna F2F2F2, maka perlu diedit terlebih dahulu.

`home_page.dart`

```dart
...
      backgroundColor: const Color(0xFFF2F2F2),
      body: const Padding(
...
```

Untuk GridView disini akan kita pisah di widget baru dengan nama `recommended_furnitures_home.dart`.

Sebelum mulai coding hendaknya kita menyusun logika pembentukan satu card di dalam GridView, contoh seperti berikut:

- container penuh dengan border radius 20, latar putih
- child Column dengan children yang pertama adalah Container yang memiliki border radius topleft dan topright 20 dengan DecorationImage diambil dari data list image furniture
- karena ada tumpukan gambar, maka Container yang mengandung DecorationImage dibungkus dalam Stack sebagai children pertama, kemudian children kedua adalah Container yang mengandung child icon love yang dibungkus dengan Positioned
- children berikutnya (dari Column) untuk memuat teks, dibungkus padding
- di dalam padding terdapat child Column dengan children yang pertama adalah nama produk, dilanjut dengan sizebox, kemudian children kedua adalah row yang memuat harga dan icon bintang serta nilai bintang.
- Untuk jarak harga dibungkus expanded karena akan memakan semua sisa, kemudian antara icon bintang dan nilai bintang diberi sizedbox

Seiring meningkatnya skill kita, nanti logika penyusunan diatas akan masuk ke otak kita tanpa perlu menuliskan/mendeskripsikan seperti diatas.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';
import 'package:google_fonts/google_fonts.dart';

class RecommendedFurnituresHome extends StatelessWidget {
  RecommendedFurnituresHome({super.key});

  final List<Map<String, dynamic>> _furnitures = [
    {
      'name': 'Stylish Chair',
      'price': 170,
      'star': 4.8,
      'image': 'assets/images/furniture/img_product_2.png',
    },
    {
      'name': 'Modern Table',
      'price': 75,
      'star': 4.9,
      'image': 'assets/images/furniture/img_product_3.png',
    },
    {
      'name': 'Wooden Console',
      'price': 240,
      'star': 4.7,
      'image': 'assets/images/furniture/img_product_4.png',
    },
    {
      'name': 'Brown Armchair',
      'price': 210,
      'star': 4.9,
      'image': 'assets/images/furniture/img_product_5.png',
    },
  ];

  @override
  Widget build(BuildContext context) {
    return GridView.builder(
      itemCount: _furnitures.length,
      gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
        crossAxisCount: 2,
        childAspectRatio: 0.7,
        mainAxisSpacing: 20,
        crossAxisSpacing: 20,
      ),
      itemBuilder: (BuildContext context, int index) {
        return Container(
          decoration: BoxDecoration(
            color: Colors.white,
            borderRadius: BorderRadius.circular(20),
          ),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Expanded(
                child: Stack(
                  children: [
                    Container(
                      decoration: BoxDecoration(
                        borderRadius: const BorderRadius.only(
                          topLeft: Radius.circular(20),
                          topRight: Radius.circular(20),
                        ),
                        image: DecorationImage(
                          image: AssetImage(_furnitures[index]['image']),
                          fit: BoxFit.cover,
                        ),
                      ),
                    ),
                    Positioned(
                      top: 10,
                      left: 10,
                      child: Container(
                        padding: const EdgeInsets.all(7),
                        decoration: BoxDecoration(
                          color: Colors.white,
                          borderRadius: BorderRadius.circular(10),
                        ),
                        child: SvgPicture.asset(
                          'assets/icons/love.svg',
                          width: 15,
                        ),
                      ),
                    )
                  ],
                ),
              ),
              Padding(
                padding: const EdgeInsets.all(10.0),
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text(
                      _furnitures[index]['name'],
                      style: GoogleFonts.poppins(
                        textStyle: const TextStyle(
                          fontWeight: FontWeight.w500,
                          fontSize: 14,
                          color: Color(0xFF4A4543),
                        ),
                      ),
                    ),
                    const SizedBox(height: 5),
                    Row(
                      children: [
                        Expanded(
                          child: Text(
                            '\$${_furnitures[index]['price']}',
                            style: GoogleFonts.poppins(
                              textStyle: const TextStyle(
                                fontWeight: FontWeight.w400,
                                fontSize: 20,
                                color: Color(0xFF9A9390),
                              ),
                            ),
                          ),
                        ),
                        const Icon(Icons.star,
                            size: 15, color: Color(0xFFEEA427)),
                        const SizedBox(width: 8),
                        Text(
                          '${_furnitures[index]['star']}',
                          style: GoogleFonts.poppins(
                            textStyle: const TextStyle(
                              fontWeight: FontWeight.w400,
                              fontSize: 12,
                              color: Color(0xFFBBBBBB),
                            ),
                          ),
                        ),
                      ],
                    ),
                    const SizedBox(height: 5),
                  ],
                ),
              ),
            ],
          ),
        );
      },
    );
  }
}
```

> **Catatan**: untuk mensimulasikan scroll, anda bisa mencopy data list furniture diatas, sehingga total ada 8 data

Output:

![Gambar 54. Perbandingan Recommended Furnitures dari Figma dengan Flutter](img/54%20perbandingan%20recommended%20furniture.PNG)

Gambar 54. Perbandingan Recommended Furnitures dari Figma dengan Flutter

### Pembuatan Bottom Navigation Bar

Selanjutnya membuat bottom navigation bar, sudah pernah dibuat pada materi sebelumnya, jadi tinggal dicopy dan disesuaikan saja.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';

class BottomNavbarHome extends StatefulWidget {
  const BottomNavbarHome({super.key});

  @override
  State<BottomNavbarHome> createState() => _BottomNavbarHomeState();
}

class _BottomNavbarHomeState extends State<BottomNavbarHome> {
  List<Map<String, dynamic>> menuItems = [
    {
      "title": "Home",
      "icon": "assets/icons/home.svg",
    },
    {
      "title": "Chart",
      "icon": "assets/icons/cart.svg",
    },
    {
      "title": "Favorites",
      "icon": "assets/icons/favorite.svg",
    },
    {
      "title": "Account",
      "icon": "assets/icons/profile.svg",
    },
  ];

  int _selectedItem = 0;

  void _onItemTapped(int index) {
    setState(() {
      _selectedItem = index;
    });
  }

  @override
  Widget build(BuildContext context) {
    return BottomNavigationBar(
      backgroundColor: Colors.white,
      showUnselectedLabels: false,
      showSelectedLabels: false,
      unselectedItemColor: Colors.black87,
      elevation: 32,
      type: BottomNavigationBarType.fixed,
      items: menuItems
          .map(
            (item) => BottomNavigationBarItem(
              icon: SvgPicture.asset(item["icon"]),
              label: item["title"],
              activeIcon: Container(
                padding: const EdgeInsets.all(10),
                decoration: const BoxDecoration(
                  color: Colors.grey,
                  borderRadius: BorderRadius.all(Radius.circular(14)),
                ),
                child: SvgPicture.asset(
                  item["icon"],
                  colorFilter:
                      const ColorFilter.mode(Colors.white, BlendMode.srcIn),
                ),
              ),
            ),
          )
          .toList(),
      currentIndex: _selectedItem,
      selectedItemColor: Colors.white,
      onTap: _onItemTapped,
    );
  }
}
```

Output:

![Gambar 55. Perbandingan BottomNavigationBar dari Figma dengan Flutter](img/55%20perbandingan%20bottomnavbar.PNG)

Gambar 55. Perbandingan BottomNavigationBar dari Figma dengan Flutter

## Pembuatan Fitur Detail

Fitur Detail terdiri dari satu halaman yaitu `DetailPage()`, sebelum mulai coding hendaknya kita menyusun logika pembentukan halaman detail ini, contoh seperti berikut:

- Scaffold, dengan body isi Stack, kemudian children berisi gambar utama besar, kemudan AppBar yg dibungkus dengan Positioned top 48
- children berikutnya ContainerDetail penuh (yg dibungkus dengan Positioned bottomcenter 0) topleft 0 dengan border radius topleft,topright 20, latar putih, dengan child Column, dengan children isi deskripsi produk dan lain-lain
- dan seterusnya

`detail_page.dart`

```dart
import 'package:flutter/material.dart';
import 'package:project_pertama/features/detail/widgets/app_bar_detail.dart';
import 'package:project_pertama/features/detail/widgets/container_detail.dart';

class DetailPage extends StatelessWidget {
  const DetailPage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Stack(
        children: [
          Positioned(
            left: 0,
            top: 0,
            child: Image.asset(
              'assets/images/furniture/img_product_1.png',
              fit: BoxFit.contain,
            ),
          ),
          Positioned(
            top: 48,
            child: SizedBox(
              width: MediaQuery.of(context).size.width,
              child: const AppBarDetail(),
            ),
          ),
          const Positioned(
            left: 0,
            bottom: 0,
            child: ContainerDetail(),
          ),
        ],
      ),
    );
  }
}
```

### Pembuatan AppBar Detail

Untuk AppBar detail ada yang spesial disini, hanya sebuah Row dengan 3 buah children yaitu:

1. memuat icon button back
2. memuat Text Detail
3. memuat Row dengan 2 buah children, untuk menampung icon love dan icon share

Ketiga children disusun dengan `mainAxisAlignment.spaceBetween`. Kode lengkapnya adalah sebagai berikut:

`app_bar_detail.dart`

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';
import 'package:google_fonts/google_fonts.dart';

class AppBarDetail extends StatefulWidget {
  const AppBarDetail({super.key});

  @override
  State<AppBarDetail> createState() => _AppBarDetailState();
}

class _AppBarDetailState extends State<AppBarDetail> {
  @override
  Widget build(BuildContext context) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.spaceBetween,
      children: [
        IconButton(
          onPressed: () {},
          icon: SvgPicture.asset("assets/icons/back.svg"),
        ),
        Text("Detail",
            style: GoogleFonts.poppins(
              fontSize: 16,
              fontWeight: FontWeight.w600,
              color: const Color(0xFF4A4543),
            )),
        Row(
          children: [
            InkWell(
              onTap: () {},
              child: Container(
                padding: const EdgeInsets.all(8),
                decoration: BoxDecoration(
                  color: const Color(0xFFFFFFFF),
                  borderRadius: BorderRadius.circular(8),
                ),
                child: SvgPicture.asset(
                  "assets/icons/love.svg",
                ),
              ),
            ),
            IconButton(
              onPressed: () {},
              icon: SvgPicture.asset("assets/icons/share.svg"),
            ),
          ],
        ),
      ],
    );
  }
}
```

### Pembuatan Container Detail

Container detail memuat seluruh informasi barang yang dijual selain gambar, karena gambar barang sudah muncul di `detail_page.dart` sebelumnya.

`container_detail.dart`

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';
import 'package:google_fonts/google_fonts.dart';
import 'package:project_pertama/features/detail/widgets/add_to_cart_detail.dart';
import 'package:project_pertama/features/detail/widgets/nama_produk_harga_detail.dart';
import 'package:project_pertama/features/detail/widgets/select_color_detail.dart';
import 'package:project_pertama/features/detail/widgets/select_quantity_detail.dart';

class ContainerDetail extends StatefulWidget {
  const ContainerDetail({super.key});

  @override
  State<ContainerDetail> createState() => _ContainerDetailState();
}

class _ContainerDetailState extends State<ContainerDetail> {
  @override
  Widget build(BuildContext context) {
    return Container(
      height: 381,
      width: MediaQuery.of(context).size.width,
      decoration: const BoxDecoration(
        color: Color(0xFFFFFFFF),
        borderRadius: BorderRadius.only(
          topLeft: Radius.circular(40),
          topRight: Radius.circular(40),
        ),
      ),
      child: Column(
        children: [
          const SizedBox(height: 10),
          //pembuatan garis strip kecil ditengah
          Container(
            width: 36,
            height: 5,
            color: const Color(0xFFD8D8D8),
          ),
          const SizedBox(height: 15),
          //pembuatan nama produk, harga, dan icon bintang, select color, select quantity dan deskripsi produk dibungkus dalam Padding
          Padding(
            padding: const EdgeInsets.symmetric(horizontal: 24),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                //pembuatan nama produk dan harga
                const NamaProdukHargaDetail(),
                const SizedBox(height: 9),
                //pembuatan icon bintang
                SvgPicture.asset("assets/icons/Score.svg"),
                const SizedBox(height: 21),
                //pembuatan select color
                const SelectColorDetail(),
                const SizedBox(height: 19),
                //pembuatan select quantity
                const SelectQuantityDetail(),
                const SizedBox(height: 32),
                SizedBox(
                  height: 60,
                  child: Text(
                    "Curabitur commodo turpis id placerat mattis. Mauris euismod arcu id orci fringilla sodales. Proin congue eleifend ipsum, eleifend porttitor mi ullamcorper.",
                    style: GoogleFonts.poppins(
                      fontSize: 12,
                      fontWeight: FontWeight.w400,
                      color: const Color(0xFFADADAD),
                    ),
                  ),
                ),
                const SizedBox(height: 30),
                //pembuatan tombol add to cart
                const AddToCartDetail(),
              ],
            ),
          ),
        ],
      ),
    );
  }
}
```

### Pembuatan Nama Produk Harga Detail

`nama_produk_harga_detail.dart`

```dart
import 'package:flutter/material.dart';
import 'package:google_fonts/google_fonts.dart';

class NamaProdukHargaDetail extends StatelessWidget {
  const NamaProdukHargaDetail({
    super.key,
  });

  @override
  Widget build(BuildContext context) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.spaceBetween,
      children: [
        Text(
          "Wooden Coff",
          style: GoogleFonts.poppins(
            fontSize: 26,
            fontWeight: FontWeight.w400,
            color: const Color(0xFF4A4543),
          ),
        ),
        Text(
          "\$240",
          style: GoogleFonts.poppins(
            fontSize: 22,
            fontWeight: FontWeight.w500,
            color: const Color(0xFF9A9390),
          ),
        ),
      ],
    );
  }
}
```

### Pembuatan Select Color Detail

`select_color_detail.dart`

```dart
import 'package:flutter/material.dart';
import 'package:google_fonts/google_fonts.dart';

class SelectColorDetail extends StatefulWidget {
  const SelectColorDetail({super.key});

  @override
  State<SelectColorDetail> createState() => _SelectColorDetailState();
}

class _SelectColorDetailState extends State<SelectColorDetail> {
  final List<Color> _colors = [
    const Color(0xFF9A9390),
    const Color(0xFFEEA427),
    const Color(0xFFE3E3E3),
    const Color(0xFF80450A),
  ];

  int _selectedColor = 0;

  void onTapColor(int index) {
    setState(() {
      _selectedColor = index;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.spaceBetween,
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        Text(
          "Choose a color",
          style: GoogleFonts.poppins(
            fontSize: 16,
            fontWeight: FontWeight.w400,
            color: const Color(0xFF7A8D9C),
          ),
        ),
        Row(
          mainAxisAlignment: MainAxisAlignment.end,
          children: _colors.asMap().entries.map((entry) {
            int index = entry.key;
            Color color = entry.value;

            return Padding(
              padding: const EdgeInsets.only(left: 8),
              child: InkWell(
                onTap: () => onTapColor(index),
                child: _selectedColor == index
                    ? CircleAvatar(
                        radius: 14,
                        backgroundColor: color,
                        child: CircleAvatar(
                          radius: 12,
                          backgroundColor: Colors.white,
                          child: CircleAvatar(
                            radius: 10,
                            backgroundColor: color,
                          ),
                        ),
                      )
                    : CircleAvatar(
                        radius: 10,
                        backgroundColor: color,
                      ),
              ),
            );
          }).toList(),
        ),
      ],
    );
  }
}
```

### Pembuatan Select Quantity Detail

`select_quantity_detail.dart`

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/svg.dart';
import 'package:google_fonts/google_fonts.dart';

class SelectQuantityDetail extends StatefulWidget {
  const SelectQuantityDetail({super.key});

  @override
  State<SelectQuantityDetail> createState() => _SelectQuantityDetailState();
}

class _SelectQuantityDetailState extends State<SelectQuantityDetail> {
  int _counter = 1;
  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  void _decrementCounter() {
    setState(() {
      if (_counter > 0) {
        _counter--;
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.spaceBetween,
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        Text(
          "Select Quantity",
          style: GoogleFonts.poppins(
            fontSize: 16,
            fontWeight: FontWeight.w400,
            color: const Color(0xFF7A8D9C),
          ),
        ),
        Row(
          children: [
            GestureDetector(
              onTap: _decrementCounter,
              child: Container(
                width: 32,
                height: 32,
                padding: const EdgeInsets.all(8),
                decoration: BoxDecoration(
                  border: Border.all(
                    color: const Color(0xFFEAEBEC),
                  ),
                  color: const Color(0xFFFCFCFC),
                  borderRadius: const BorderRadius.only(
                      bottomLeft: Radius.circular(18),
                      topLeft: Radius.circular(18)),
                ),
                child: SvgPicture.asset("assets/icons/substract.svg"),
              ),
            ),
            Container(
              width: 40,
              height: 32,
              color: const Color(0xFFE3E3E3),
              child: Center(
                child: Text(_counter.toString(),
                    style: GoogleFonts.poppins(
                      fontSize: 16,
                      fontWeight: FontWeight.w400,
                      color: const Color(0xFF4A4543),
                    )),
              ),
            ),
            GestureDetector(
              onTap: _incrementCounter,
              child: Container(
                width: 32,
                height: 32,
                padding: const EdgeInsets.all(8),
                decoration: BoxDecoration(
                  border: Border.all(
                    color: const Color(0xFFEAEBEC),
                  ),
                  color: const Color(0xFFFCFCFC),
                  borderRadius: const BorderRadius.only(
                      topRight: Radius.circular(18),
                      bottomRight: Radius.circular(18)),
                ),
                child: SvgPicture.asset("assets/icons/add.svg"),
              ),
            ),
          ],
        ),
      ],
    );
  }
}
```

### Pembuatan Tombol Add To Cart Detail

`add_to_cart_detail.dart`

```dart
import 'package:flutter/material.dart';
import 'package:google_fonts/google_fonts.dart';

class AddToCartDetail extends StatelessWidget {
  const AddToCartDetail({super.key});

  @override
  Widget build(BuildContext context) {
    return SizedBox(
      width: MediaQuery.of(context).size.width,
      child: ElevatedButton(
        style: ElevatedButton.styleFrom(
          backgroundColor: const Color(0xFF9A9390),
        ),
        onPressed: () {},
        child: Text(
          "ADD TO CART",
          style: GoogleFonts.poppins(
            fontSize: 12,
            fontWeight: FontWeight.w700,
            color: const Color(0xFFFFFFFF),
          ),
        ),
      ),
    );
  }
}
```

Hasil akhir untuk `DetailPage()`

![Gambar 56. Perbandingan Detail Page dari Figma dengan Flutter](img/56%20perbandingan%20detail%20page.PNG)

Gambar 56. Perbandingan Detail Page dari Figma dengan Flutter

> Tugas 1
>
> Buatlah project slicing desain figma ke flutter (2 sampai 3 halaman), dari beberapa pilihan berikut:
>
> - [Instagram App UI](<https://www.figma.com/file/lXCXhzF2P18TWhbsFIYUjM/Instagram-UI-Screens-(Community)?type=design&node-id=0-2&mode=design>)
> - [Medical App UI](<https://www.figma.com/file/wXY32rVqx4g3OxJiXSqvDh/Medical-app-%7C-Improving-speech-%F0%9F%A9%BA-(Community)?type=design&node-id=0-1&mode=design&t=tchKLWzOd4m6l3Zn-0>)
> - [Grocery App UI](<https://www.figma.com/file/xBWXLGr0qqKjmuL0ai5aLG/Grocery-App-UI-Kit---Community-(Community)?type=design&node-id=113-7674&mode=design&t=KTf62hw2f8fE0C1Y-0>)
> - atau yang lainnya (search di figma community)
