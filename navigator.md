# Navigator

Navigator merupakan widget yang memiliki tugas untuk melakukan navigasi/pindah halaman lain. Dalam materi form sebelumnya anda sudah membreakdown widget menjadi bagian lebih kecil. Hal ini sebenarnya mekanismenya hampir mirip karena navigator berarti nanti anda akan memanggil widget stateless atau stateful baru.

Dalam materi navigasi ini akan dipelajari tentang:

- [Navigator push](#navigator-push)
- [Navigator pop](#navigator-pop)
- [Bottom Navigation Bar](#bottom-navigation-bar)
- [TabBar](#tabbar)
- [Drawer](#drawer)
- [SliverAppBar](#sliverappbar)

## Navigator push

Sebagian besar app berisi beberapa layar untuk menampilkan berbagai jenis informasi. Misalnya, aplikasi mungkin memiliki layar yang menampilkan produk. Saat pengguna mengetuk gambar suatu produk, layar baru menampilkan detail tentang produk tersebut.

Terminologi: Di Flutter, layar dan halaman disebut rute.

```
Navigator
│───push()
|   |───MaterialPageRoute()
|   |───CupertinoPageRoute()
|   |───PageRouteBuilder()
│───pop()
```

Di Android, rute setara dengan activity. Di iOS, rute setara dengan ViewController. Di Flutter, rute hanyalah sebuah widget. Aturan ini menggunakan Navigator untuk menavigasi ke rute baru. Beberapa bagian selanjutnya menunjukkan cara bernavigasi di antara dua rute, menggunakan langkah-langkah berikut:

Buat dua rute:

- Arahkan ke rute kedua : Navigator.push().
- Kembali ke rute pertama : Navigator.pop()

Contoh code dibawah ini kita akan praktekan push ke route page selanjutnya dengan cara klik button Next Page

```dart
...
      body: Padding(
        padding: const EdgeInsets.all(10.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            ElevatedButton(
              onPressed: () {
                Navigator.of(context).push(
                    MaterialPageRoute(builder: (context) => const PageTwo()));
              },
              child: const Text('Next Page'),
            ),
          ],
        ),
      ),
...
```

Sedangkan di halaman dua hanya ditampilkan teks Page Two

```dart
...
      body: const Padding(
        padding: EdgeInsets.all(10.0),
        child: Text('Page Two'),
      ),
...

```

Output:

![Gambar 41. Widget Navigotor.push](img/41%20navigator%20push.png)

Gambar 41. Widget Navigator

Baca Dokumentasi Resmi:

- [Navigator.](https://api.flutter.dev/flutter/widgets/Navigator-class.html)

- [MaterialPageRoute.](https://api.flutter.dev/flutter/material/MaterialPageRoute-class.html)

## Navigator pop

Navigation pop ini berfungsi untuk kembali ke page sebelumnya setelah tampil karena navigator pop. Code disamping memperlihatkan kondisi ketika page two dengan button go back diklik, maka akan kembali ke page pertama. Ubah kode di page two menjadi seperti kode berikut:

```dart
...
      body: Padding(
        padding: const EdgeInsets.all(10.0),
        child: ElevatedButton(
          onPressed: () {
            Navigator.pop(context);
          },
          child: const Text('Go Back'),
        ),
...
```

## Bottom Navigation Bar

Ini adalah widget yang ditampilkan di bagian bawah aplikasi untuk memilih diantara beberapa tampilan, biasanya antara tiga dan lima. Bottom navigation bar terdiri dari beberapa item dalam bentuk label teks, ikon, atau keduanya, yang diletakkan di atas material. Ini menyediakan navigasi cepat antara tampilan tingkat atas aplikasi. Untuk layar yang lebih besar, navigasi samping mungkin lebih cocok.Bottom navigation bar biasanya digunakan bersamaan dengan Scaffold, yang disediakan sebagai argumen Scaffold.bottomNavigationBar.

```
BottomNavigationBar
│───items
|   |───List<BottomNavigationBarItem>
│───iconSize
│───currentIndex
│───onTap
│───fixedColor
│───type
|   |───BottomNavigationBarType
|   |   |───fixed
|   |   |───shifting
```

```dart
...
  List<Map<String, dynamic>> menuItems = [
    {
      "title": "Home",
      "icon": Icons.home,
    },
    {
      "title": "Chart",
      "icon": Icons.shopping_cart,
    },
    {
      "title": "Favorites",
      "icon": Icons.star_border,
    },
    {
      "title": "Account",
      "icon": Icons.person,
    },
  ];

  int _selectedItem = 0;

  String _text = "Home";

  void _onItemTapped(int index) {
    setState(() {
      _selectedItem = index;
      _text = menuItems[index]["title"];
    });
  }

...

          children: <Widget>[
            Text(
              'Kamu klik: $_text',
              style: Theme.of(context).textTheme.headlineMedium,
            ),
...

      bottomNavigationBar: BottomNavigationBar(
        backgroundColor: Colors.white,
        showUnselectedLabels: false,
        showSelectedLabels: false,
        unselectedItemColor: Colors.black87,
        elevation: 32,
        type: BottomNavigationBarType.fixed,
        selectedLabelStyle: const TextStyle(
          height: 1.5,
          fontSize: 12,
        ),
        unselectedLabelStyle: const TextStyle(
          height: 1.5,
          fontSize: 12,
        ),
        items: menuItems
            .map(
              (item) => BottomNavigationBarItem(
                icon: Icon(item["icon"]),
                label: item["title"],
                activeIcon: Container(
                  padding: const EdgeInsets.all(10),
                  decoration: const BoxDecoration(
                    color: Colors.grey,
                    borderRadius: BorderRadius.all(Radius.circular(14)),
                  ),
                  child: Icon(item["icon"]),
                ),
              ),
            )
            .toList(),
        currentIndex: _selectedItem,
        selectedItemColor: Colors.white,
        onTap: _onItemTapped,
      ),
```

Output:

![Gambar 42. Widget BottomNavigationBar](img/42%20bottom%20navigation%20bar.png)

Gambar 42. Widget BottomNavigationBar

Baca Dokumentasi Resmi:

- [BottomNavigationBar.](https://api.flutter.dev/flutter/material/BottomNavigationBar-class.html)

## TabBar

Widget ini menampilkan deretan tab horizontal. Biasanya dibuat sebagai bagian AppBar.bottom dari AppBar dan bersamaan dengan TabBarView.

```
tabs
│───DefaultTabController()
|   |───length
|   │───child
│───SingleTickerProviderStateMixin
|   │───TabController()
|   |   │───vsync
|   |   │───length
|   |   |───addListener()
```

Dibawah ini adalah sample code untuk membuat TabBar dengan TabBarView dibawahnya

```dart
import 'package:flutter/material.dart';

class MyTabBar extends StatefulWidget {
  const MyTabBar({super.key});

  @override
  State<MyTabBar> createState() => _MyTabBarState();
}

class _MyTabBarState extends State<MyTabBar> with TickerProviderStateMixin {
  late TabController _tabController;

  @override
  void initState() {
    super.initState();
    _tabController = TabController(length: 3, vsync: this);
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Coding Flutter - TabBar"),
        bottom: TabBar(
          controller: _tabController,
          tabs: const [
            Tab(icon: Icon(Icons.directions_boat)),
            Tab(icon: Icon(Icons.directions_bus)),
            Tab(icon: Icon(Icons.directions_bike)),
          ],
        ),
      ),
      body: TabBarView(
        controller: _tabController,
        children: const [
          Center(child: Text("Tab 1")),
          Center(child: Text("Tab 2")),
          Center(child: Text("Tab 3")),
        ],
      ),
    );
  }
}
```

Output:

![Gambar 43. Widget TabBar](img/43%20tabbar.png)

Gambar 43. Widget TabBar

Baca Dokumentasi Resmi:

- [TabBar.](https://api.flutter.dev/flutter/material/TabBar-class.html)

## Drawer

## SliverAppBar
