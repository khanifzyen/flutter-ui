# Navigator

[Kembali](form.md)

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

Di app yang menggunakan Desain Material, ada dua opsi utama untuk navigasi: tab dan drawer. Jika tidak ada cukup ruang untuk mendukung tab, drawer memberikan alternatif yang praktis. Di Flutter, gunakan widget Drawer yang dikombinasikan dengan Scaffold untuk membuat tata letak dengan panel di samping Desain Material. Aturan ini menggunakan langkah-langkah berikut:

- Buat scaffold.
- Tambahkan drawer.
- Isi drawer dengan item.
- Tutup drawer secara terprogram.

```
drawer
│───Drawer()
|   │───child
|   |   │───DrawerHeader()
|   |   │───UserAccountDrawerHeader()
```

Dibawah ini adalah contoh code dalam penggunaan drawer, disini saya menggunakan `drawer` yang artinya nanti munculnya dari sebelah kiri. Berisikan `UserAccountDrawerHeader`, dan juga `ListTile`

```dart
...
      drawer: Drawer(
        child: ListView(
          children: [
            Container(
              color: Colors.blue[100],
              child: UserAccountsDrawerHeader(
                decoration: BoxDecoration(
                  color: Colors.grey[200],
                ),
                accountName: const Text(
                  'Khanif Zyen',
                  style: TextStyle(color: Colors.black),
                ),
                accountEmail: const Text(
                  "khanif.zyen@gmail.com",
                  style: TextStyle(color: Colors.black),
                ),
                currentAccountPicture: const CircleAvatar(
                  child: FlutterLogo(size: 50),
                ),
              ),
            ),
            ListTile(
              title: const Text('Item 1'),
              onTap: () {
                Navigator.pop(context);
              },
            ),
            ListTile(
              title: const Text('Item 2'),
              onTap: () {},
            ),
          ],
        ),
      ),
...
```

Output:

![Gambar 44. Widget Drawer](img/44%20drawer.png)

Gambar 44. Widget Drawer

Parameter `drawer` menerima kembalian berupa widget `Drawer`. Jika drawer diisi, maka parameter `leading` di widget `AppBar` bisa tidak usah diisi. Widget `Drawer` akan menampilkan menu icon hamburger, yang jika ditap maka akan menampilkan menu di samping, dan isinya sesuai dengan `ListView`, sehingga bisa discroll.

Baca Dokumentasi Resmi:

- [Drawer.](https://api.flutter.dev/flutter/material/Drawer-class.html)
- [DrawerHeader.](https://api.flutter.dev/flutter/material/DrawerHeader-class.html)
- [ListTile.](https://api.flutter.dev/flutter/material/ListTile-class.html)

## SliverAppBar

Widget ini terintegrasi dengan `CustomScrollView`. Appbar terdiri dari toolbar dan kemungkinan widget lainnya, seperti TabBar dan FlexibleSpaceBar. appbar biasanya memaparkan satu atau beberapa tindakan umum dengan IconButtons yang secara opsional diikuti oleh PopupMenuButton untuk operasi yang kurang umum.

`SliverAppBar` biasanya digunakan sebagai anak pertama dari `CustomScrollView`, yang memungkinkan appbar berintegrasi dengan tampilan scroll sehingga tingginya dapat bervariasi sesuai dengan offset atau melayang di atas konten lain dalam tampilan scroll. Untuk appbar dengan ketinggian tetap di bagian atas layar, lihatlah AppBar, yang menggunakan slot dari Scaffold.appBar.

```
SliverAppBar
│───expandedHeight
│───flexibleSpace
|   │───FlexibleSpaceBar()
│───pinned
|   │───bool
│───floating
|   │───bool
│───snap
|   │───bool
```

Dibawah adalah contoh code penggunaan SliverAppBar yaitu widget CustomScrolView yang didalamnya berisi list sliver dan anak pertama adalah sliverappbar dimana dia punya properties pinned, snap, floating yang bernilai true atau false. Terdapat properties expanedheight juga untuk set tinggi dari sliverappbar, dan terdapat flexiblespace jika scroll terjadi. Lalu di ikuti oleh sliverlist bagian dari `CustomScrollView`.

```dart
...
      body: CustomScrollView(
        slivers: [
          const SliverAppBar(
            pinned: true,
            snap: true,
            floating: true,
            expandedHeight: 160,
            flexibleSpace: FlexibleSpaceBar(
              title: Text(
                "UNISNU Jepara",
                style: TextStyle(color: Colors.black),
              ),
              background: FlutterLogo(),
            ),
          ),
          SliverList(
            delegate: SliverChildBuilderDelegate((context, index) {
              return Container(
                color: index.isOdd ? Colors.white : Colors.blue[200],
                height: 100,
                child: Center(
                  child: Text(
                    "Item $index",
                    textScaler: const TextScaler.linear(2),
                  ),
                ),
              );
            }, childCount: 20),
          ),
        ],
      ),
...
```

Output:

![Gambar 45. Widget SliverAppBar](img/45%20sliverappbar.png)

Gambar 45. Widget SliverAppBar

Bila kita running hasilnya akan seperti diatas. Dimana pertama sliverappbar akan menempati bagiannya dan ketika kita scroll ke atas dia akan fleksible mengikuti scroll sampai tinggal setinggi appbar.

Baca Dokumentasi Resmi:

- [SliverAppBar.](https://api.flutter.dev/flutter/material/SliverAppBar-class.html)

# [Materi Selanjutnya: Figma](figma.md)
