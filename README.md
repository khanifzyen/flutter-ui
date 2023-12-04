# Flutter UI

Materi Mata Kuliah Pemrograman Mobile | Teknik Informatika UNISNU Jepara | Akhmad Khanif Zyen

---

Setelah sebelumnya kita mempelajari bagaimana flutter bekerja bersama dart dalam membuat sebuah tampilan pada layar, yuk kita belajar tentang widget widget yang akan sering dipakai dalam proses development UI dalam pengembangan aplikasi.

Materi yang akan dibahas pada modul ini adalah:

1. [Basic widget](#basic-widget)
2. [Layout](#layout)
3. [Form](#form)
4. [Navigator](#navigator)
5. [Figma](#figma)

# 1. Basic Widget

Untuk basic widget yang minimal harus diketahui oleh seorang Flutter developer diantaranya:

- [Scaffold](#scaffold)
- [AppBar](#appbar)
- [Container](#container)
- [Text](#text)
- [Button](#button)
- [Icon](#icon)
- [Images](#images)
- [CircleAvatar](#circleavatar)

## Scaffold

Scaffold adalah widget yang mengimplementasi struktur tata letak dari design material. Lalu apa itu design material ?

Material Design adalah sebuah gaya desain terbaru dari Google yang memiliki prinsip bahwa desain itu harus seperti sebuah kertas pada kenyataannya. Terus apa bedanya dengan kertas? Material design merupakan kertas ajaib yang bisa membesar, mengecil, membelah diri, berubah warna, dan bertransformasi menjadi berbagai bentuk.

Skema Scaffold:

```
Scaffold
│───appBar
|   |   leading
|   |   title
|   |   action
│   body
│   bottomNavigationBar
|   floatingActionButton
|   drawer
```

Dibawah ini adalah contoh tampilan layar dari widget scaffold, dimana dia mempunyai appbar di paling atas, yang berwarna biru dengan title Sample Code. Lalu ada body yang berisi text dan berada di bagian tengah dengan wording ‘You have pressed the button 0 times.’ lalu ada `floatingActionButton` di pojok kanan bawah yang berisi icon add.

![Gambar 1](img/01%20counter%20app.png)

Gambar 1. Aplikasi Counter

[Dokumentasi Scaffold.](https://api.flutter.dev/flutter/material/Scaffold-class.html)

## Scaffold > appBar

Parameter appBar menerima widget AppBar yang selalu ditempatkan di bagian atas layar. Jika Scaffold mempunyai Drawer, maka button icon hamburger (yang terletak di property leading) akan ditambahkan secara otomatis untuk menangani open close drawer.

```dart
...
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Theme.of(context).colorScheme.inversePrimary,
        title: Text(widget.title),
        leading: IconButton(
          onPressed: () {},
          icon: const Icon(Icons.menu),
        ),
        actions: [
          IconButton(
            onPressed: () {},
            icon: const Icon(Icons.search),
          ),
          IconButton(
            onPressed: () {},
            icon: const Icon(Icons.more_vert),
          ),
        ],
      ),
      ...
```

Output:

![Gambar 2. AppBar](img/02%20appbar.png)

Gambar 2. AppBar

Pada parameter `title` berisi `Text(widget.title)`, disini tidak menggunakan `const` karena isi dari widget `Text` didapatkan dari luar, sehingga ada potensi untuk value berubah. Berbeda pada class `IconButton` dengan parameter `icon`, yang berisi class `Icon` di depannya diberi `const` karena sudah dipastikan icon tidak berubah atau tidak berubah dari external maupun internal sehingga nanti tidak akan di-rebuild ulang UInya.

[Dokumentasi AppBar.](https://api.flutter.dev/flutter/material/AppBar-class.html)

## Scaffold > body

```dart
...
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            const Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headlineMedium,
            ),
          ],
        ),
      ),
...
```

Di parameter body ini nantilah yang akan banyak kita tulis kodenya. Karena disini nantilah widget yang akan tampil hampir 99% di layar kita. Body ini butuh kembalian widget, widget disini bisa di isi oleh widget yang bisa menampung widget lain, seperti Column, ListView, Stack, Container, dll. Ini nanti akan kita bahas di layout widget. Untuk contoh case diatas, body saya isi dengan widget Center yang isinya terdapat widget text dengan value ‘You have pressed the button 0 times.'

## Scaffold > floatingActionButton

```dart
      ...
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: const Icon(Icons.add),
      ),
      ...
```

Parameter `floatActionButton` juga sudah disediakan oleh flutter yang fungsinya membuat button yang floating di sisi bawah kanan, ini untuk posisi bisa kita geser2 dengan config yang dia sediakan. Seperti dibaris 21 ini, floatingactionbutton dia membutuhkan kembalian widget dan widgetnya menggunakan widget `FloatingActionButton` dengan child sebuah icon `Icons.add`. Nanti hasilnya seperti di tampilan di Gambar 1.

[Dokumentasi FloatingActionButton.](https://api.flutter.dev/flutter/material/FloatingActionButton-class.html)

## Scaffold > drawer

```dart
...
      drawer: Drawer(
        child: ListView(
          children: [
            const DrawerHeader(
              decoration: BoxDecoration(
                color: Colors.deepPurple,
              ),
              child: Text(
                'Drawer Header',
                style: TextStyle(color: Colors.white),
              ),
            ),
            ListTile(
              title: const Text('Item 1'),
              onTap: () {},
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

Parameter `drawer` menerima kembalian berupa widget `Drawer`. Jika drawer diisi, maka parameter `leading` di widget `AppBar` bisa tidak usah diisi. Widget `Drawer` akan menampilkan menu icon hamburger, yang jika ditap maka akan menampilkan menu di samping, dan isinya sesuai dengan ListView, sehingga bisa discroll.

[Dokumentasi Drawer.](https://api.flutter.dev/flutter/material/Drawer-class.html)

[Dokumentasi DrawerHeader.](https://api.flutter.dev/flutter/material/DrawerHeader-class.html)

[Dokumentasi ListTile.](https://api.flutter.dev/flutter/material/ListTile-class.html)

## Scaffold > bottomNavigationBar

Parameter `bottomNavigationbar` menerima kembalian berupa widget `BottomNavigationBar`, adalah widget yang digunakan dalam aplikasi Flutter untuk menyediakan navigasi di bagian bawah layar. Biasanya digunakan untuk berpindah antara beberapa tampilan atau layar utama dalam aplikasi.

```dart
...
      bottomNavigationBar: BottomNavigationBar(
        items: const [
          BottomNavigationBarItem(
            icon: Icon(Icons.home),
            label: 'Home',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.mail),
            label: 'Messages',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.person),
            label: 'Profile',
          ),
        ],
      ),
...
```

![Gambar 3. Bottom Navigation Bar](img/03%20bottomnavigationbar.png)

Gambar 3. Bottom Navigation Bar

[Dokumentasi BottomNavigationBar.](https://api.flutter.dev/flutter/material/BottomNavigationBar-class.html)

[Dokumentasi BottomNavigationBarItem.](https://api.flutter.dev/flutter/widgets/BottomNavigationBarItem-class.html)

## Container

## Text

## Button

## Icon

## Images

## CircleAvatar

# 2. Layout

# 3. Form

# 4. Navigator

# 5. Figma

##
