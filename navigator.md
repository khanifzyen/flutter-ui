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

## TabBar

## Drawer

## SliverAppBar
