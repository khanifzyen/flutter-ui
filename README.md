# Flutter UI

Materi Mata Kuliah Pemrograman Mobile | Teknik Informatika UNISNU Jepara | Akhmad Khanif Zyen

---

> **Cara menggunakan modul ini:**
>
> 1. Login ke akun github anda.
> 2. Star ke repository ini.
> 3. Fork repository ini sehingga masuk ke repository di akun github masing-masing.
> 4. Clone project dari repository github masing-masing.
>    ```bash
>    git clone https://github.com/namauser/flutter-ui.git
>    ```
> 5. Buat branch baru `dev` dan gunakan sebagai branch yang aktif.
>
>    ```bash
>    git checkout -b dev
>    ```
>
> 6. Mulai praktek, selesai praktek lakukan commit dengan label sesuai materi yang dikerjakan. Untuk project folder, anda bisa buat di dalam folder flutter-basics dengan nama project "project_flutter_ui"
>
>    ```bash
>    git add .
>    git commit -m "container"
>    ```
>
> 7. Lakukan push ke repository github masing-masing
>    ```bash
>    git push -u origin dev
>    ```
> 8. Jika sudah selesai semua, kembali ke repository ini, kemudian masuk ke menu `issue`, tulis identitas diri (NIM, Nama) dan link repo github hasil dari fork project ini.
> 9. Penilaian berdasarkan commit di branch `dev` pada repo akun github masing-masing.

Setelah sebelumnya kita mempelajari bagaimana flutter bekerja bersama dart dalam membuat sebuah tampilan pada layar, yuk kita belajar tentang widget widget yang akan sering dipakai dalam proses development UI dalam pengembangan aplikasi.

Materi yang akan dibahas pada modul ini adalah:

1. [Basic widget](#1-basic-widget)
2. [Layout](layout.md)
3. [Form](form.md)
4. [Navigator](navigator.md)
5. [Figma](figma.md)

# 1. Basic Widget

Untuk basic widget yang minimal harus diketahui oleh seorang Flutter developer diantaranya:

- [Scaffold](#scaffold)
- [Container](#container)
- [Text](#text)
- [Button](#button)
- [Icon](#icon)
- [Images](#images)
- [CircleAvatar](#circleavatar)

## Scaffold

Scaffold adalah widget yang mengimplementasi struktur tata letak dari design material. Lalu apa itu design material ?

Material Design adalah sebuah gaya desain terbaru dari Google yang memiliki prinsip bahwa desain itu harus seperti sebuah kertas pada kenyataannya. Terus apa bedanya dengan kertas? Material design merupakan kertas ajaib yang bisa membesar, mengecil, membelah diri, berubah warna, dan bertransformasi menjadi berbagai bentuk.

Skema property Scaffold:

```
Scaffold
│───appBar
|   |───leading
|   |───title
|   |───action
│───body
│───bottomNavigationBar
|───floatingActionButton
|───drawer
```

Dibawah ini adalah contoh tampilan layar dari widget scaffold, dimana dia mempunyai appbar di paling atas, yang berwarna biru dengan title Sample Code. Lalu ada body yang berisi text dan berada di bagian tengah dengan wording ‘You have pressed the button 0 times.’ lalu ada `floatingActionButton` di pojok kanan bawah yang berisi icon add.

![Gambar 1](img/01%20counter%20app.png)

Gambar 1. Aplikasi Counter

Baca Dokumentasi Resmi:

- [Scaffold.](https://api.flutter.dev/flutter/material/Scaffold-class.html)

### Scaffold > appBar

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

Baca Dokumentasi Resmi:

- [AppBar.](https://api.flutter.dev/flutter/material/AppBar-class.html)

### Scaffold > body

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

### Scaffold > floatingActionButton

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

Baca Dokumentasi Resmi:

- [FloatingActionButton.](https://api.flutter.dev/flutter/material/FloatingActionButton-class.html)

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

Baca Dokumentasi Resmi:

- [BottomNavigationBar.](https://api.flutter.dev/flutter/material/BottomNavigationBar-class.html)
- [BottomNavigationBarItem.](https://api.flutter.dev/flutter/widgets/BottomNavigationBarItem-class.html)

## Container

Widget Container ini setara dengan tag \<div>\</div> di HTML. Ini adalah wadah yang dapat kita gunakan untuk menyesuaikan bentuk, posisi, ukuran, pewarnaan dan masih banyak lagi. Wadah ini sangat banyak digunakan karena menyelesaikan banyak kasus seperti membuat border melengkung atau bekerja dengan bentuk bentuk tertentu.Di bawah ini adalah skema properties yang dimiliki oleh widget container.

```
Container
|───child
|───height
|───width
│───margin
|   |───EdgeInsets.all()
│───padding
|   |───EdgeInsets.all()
│───alignment
|   |───Alignment
│───decoration
|   │───BoxDecoration()
|       │───color
|       |───border
|       |───borderRadius
│───transform
|   │───Matrix4
|       │───transitionValues
|       |───rotationZ
```

Seperti contoh dibawah ini, widget container kita masukan ke dalam body milik widget scaffold. Didalamnya kita dapat memberi nilai tinggi, lebar, jarak antara border, decoration dan dia juga punya child yang hanya bisa 1 anak widget. Namun tenang saja, anaknya ini bisa diisi dengan column atau row jadi tetap didalamnya bisa berisi banyak widget. Contoh disamping ceritanya kita akan membuat wadah atau container dengan tinggi 300px, lewar selebar layar,margin dengan tepi layar itu 10px, dan mempunyai dekorasi warna grey, border radius yang melengkung dengan lengkungan 20px, lalu ada bayang2 juga.

```dart
...
      body: Container(
        height: 300,
        width: double.infinity,
        margin: const EdgeInsets.all(10),
        decoration: BoxDecoration(
          color: Colors.grey,
          borderRadius: BorderRadius.circular(20),
          boxShadow: [
            BoxShadow(
              color: Colors.black.withOpacity(0.2),
              blurRadius: 15.0,
              offset: Offset.zero,
            ),
          ],
        ),
      ),
...
```

Output:

![Gambar 4. Widget Container](img/04%20container.png)

Gambar 4. Widget Container

Implementasi Container dalam dunia nyata bisa kita lihat misalnya dalam aplikasi ecommerce untuk menampilkan produk yang terdiri dari gambar, title, harga dan rating, sehingga bisa menjadi sebuah Card. Adapun Card sendiri sebenarnya terdapat widget bawaan.

![Gambar 5. Implementasi Container menjadi Widget Card](img/05%20implementasi%20container.PNG)

Gambar 5. Implementasi Container

Baca Dokumentasi Resmi:

- [Container.](https://api.flutter.dev/flutter/widgets/Container-class.html)
- [BoxDecoration.](https://api.flutter.dev/flutter/painting/BoxDecoration-class.html)
- [BorderRadius.](https://api.flutter.dev/flutter/painting/BorderRadius-class.html)
- [BoxShadow.](https://api.flutter.dev/flutter/painting/BoxShadow-class.html)

## Text

Widget teks digunakan untuk menampilkan teks di layar. Ini sangat fleksibel buat kita dalam memanipulasi text seperti mengubah warna font, menggunakan aset font atau paket dari Google Font, menambah ukuran font, memberi garis bawah pada text dan masih banyak lainnya. Di bawah ini adalah skema properties yang dimiliki oleh widget Text.

```
Text
│───style
|   │───TextStyle()
|   |   │───color
|   |   |───fontSize
|   |   |───fontWeight
|   |   |───fontFamily
|   |   |───fontStyle
|   |   |   |───italic
|   |   |───decoration
|   |   |   |───TextDecoration()
|   |   |───decorationStyle
|   |   |   |───TextDecorationStyle()
|   |   |───letterSpacing
|   |   |───wordSpacing
|───overflow
|   |───TextOverflow
|   |   │───ellipsis
|───maxLine
|───textAlign
|   |───TextAlign
|   |   |───center
|───textDirection
|───textScaleFactor
```

Dalam contoh kode dibawah ceritanya kita ingin menampilkan text dengan style warnanya hitam, ukuran fontnya 22px, ketebalan hurufnya medium atau tengah-tengah dan letter spasinya 1px.

```dart
...
      body: Container(
        padding: const EdgeInsets.all(10),
        child: const Column(
          children: [
            Text(
              "Discover the most modern furniture",
              style: TextStyle(
                  color: Colors.black,
                  fontSize: 22.0,
                  fontWeight: FontWeight.w500,
                  letterSpacing: 1),
            )
          ],
        ),
      ),
...
```

Output:

![Gambar 5. Widget Text](img/05%20text.png)

Gambar 5. Widget Text

Untuk implementasi Text dalam dunia nyata bisa kita lihat misalnya dalam aplikasi ecommerce untuk menampilkan tagline dari dari produk.

![Gambar 6. Implementasi Text](img/06%20implementasi%20text.PNG)

Gambar 6. Implementasi Text

Baca Dokumentasi Resmi:

- [Text.](https://api.flutter.dev/flutter/widgets/Text-class.html)
- [TextStyle.](https://api.flutter.dev/flutter/painting/TextStyle-class.html)

## Button

Tombol adalah salah satu bagian dasar dalam aplikasi apapun karena tombol merupakan cara paling intuitif untuk memberi tahu pengguna bahwa saat ditekan, akan terjadi sesuatu. Flutter memiliki beberapa jenis tombol yang sudah disediakan ya itu `ElevatedButton`, `TextButton`, `OutlinedButton`. Di bawah ini adalah skema properties yang dimiliki oleh widget Button.

```
Button
│───ElevatedButton
|   |───child
|   |───onPressed
|   │───style
|   |   │───ElevatedButton.styleFrom()
|   |   |───ButtonStyle()
|   |   |   |───backgroundColor
|   |   |   |───foregroundColor
|   |   |   |───elevation
|   |   |   |───shape
│───TextButton (properties sama seperti ElevatedButton)
│───OutlinedButton (properties sama seperti ElevatedButton)
```

Dalam contoh dibawah, ceritanya kita akan membuat sebuah button dengan style background biru, dan bentuknya itu akan ada lengkungan di tiap sisi sisinya, serta mempunyai sedikit bayangan. Lalu di dalamnya akan ada text dengan warna putih dan ukuran font 20px.

```dart
...
      body: Container(
        padding: const EdgeInsets.all(10.0),
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
...
```

Output:

![Gambar 7. Widget Button](img/07%20button.png)

Gambar 7. Widget Button

Implementasi Button pada dunia nyata nanti akan bermanfaat untuk membuat tombol seperti tombol tambah ke keranjang atau tombol hubungi penjual.

![Gambar 8. Implementasi Button](img/08%20implementasi%20button.PNG)

Gambar 8. Implementasi Button

Baca Dokumentasi Resmi:

- [ElevatedButton.](https://api.flutter.dev/flutter/material/ElevatedButton-class.html)
- [TextButton.](https://api.flutter.dev/flutter/material/TextButton-class.html)
- [OutlinedButton.](https://api.flutter.dev/flutter/material/OutlinedButton-class.html)
- [ButtonStyle.](https://api.flutter.dev/flutter/material/ButtonStyle-class.html)

## Icon

Icon sudah tersedia di flutter, jadi kita tidak perlu mengunduhnya. Icon ini adalah gambar vektor sehingga ukurannya walau berubah-rubah ukuran, tidak akan kehilangan kualitas gambarnya.

Dibawah ini adalah contoh penggunaan widget icon, dimana ceritanya saya ingin membuat icon home dengan ukuran 32, dan juga icon favorite dengan ukuran 36 dan bisa langsung dikasih warna merah.

```dart
...
      body: Container(
        color: Colors.blue[200],
        padding: const EdgeInsets.all(20),
        child: const Row(
          children: [
            Icon(
              Icons.home,
              size: 32,
            ),
            Icon(
              Icons.favorite,
              color: Colors.red,
              size: 36,
            ),
          ],
        ),
      ),
...
```

Output:

![Gambar 9. Widget Icon](img/09%20icon.png)

Gambar 9. Widget Icon

Implementasi icon ini akan banyak sekali dipakai dalam aplikasi apapun yang akan kita buat. Contoh pada icon favorite, awalnya berbentuk outline love berwarna grey, kemudian jika di-tap akan menjadi full merah yang berarti untuk menandai suatu product telah dimasukan ke product favorite user.

![Gambar 10. Implementasi Icon](img/09%20implementasi%20icon.PNG)

Gambar 10. Implementasi Icon

Baca Dokumentasi Resmi:

- [Icon.](https://api.flutter.dev/flutter/widgets/Icon-class.html)

## Images

Beberapa konstruktor disediakan untuk berbagai cara agar gambar dapat ditentukan:

- `Image.new`, untuk mendapatkan gambar dari ImageProvider.
- `Image.asset`, untuk mendapatkan gambar dari AssetBundle menggunakan kunci.
- `Image.network`, untuk mendapatkan gambar dari URL.
- `Image.file`, untuk mendapatkan gambar dari File.
- `Image.memory`, untuk mendapatkan gambar dari Uint8List.

Di bawah ini adalah mindmap yang dimiliki oleh widget Image.

```
Image
│───Image.network()
|   |───alignment
|   |   │───Alignment
|   |───color
|   │───colorBlendMode
|   |   │───BlendMode
|   |───fit
|   |   │───BoxFit
|   |   |   |───.fill
|   |   |   |───.contain
|   |   |   |───.cover
|   |   |   |───.fitWidth
|   |   |   |───.fitHeight
|   │───repeat
|   |   │───ImageRepeat
|   |   |   |───.repeat
|   |   |   |───.repeatX
|   |   |   |───.repeatY
│───Image.asset()
|   |───pubspec.yaml (path file gambar ditulis disini, dalam key assets)
|   |   │───assets (file gambar diletakkan dalam folder assets)
|   |   (property lain sama dengan network image)
|   Circular Image (bagaimana untuk mendapatkan image yang bulat)
|   |───Container
|   |   │───decoration
|   │───ClipOval
|   |   │───child
|   |   |   |───Image.network()
|   |   │───height
|   |   │───width
|   |   │───fit
```

Code dibawah ini, saya ingin mempraktekan image yang diambi dari assets.

```dart
...
      body: Container(
        padding: const EdgeInsets.all(10.0),
        child: Row(
          children: [
            SizedBox(
              width: 180,
              child: ClipRRect(
                borderRadius: const BorderRadius.only(
                  topLeft: Radius.circular(20),
                  topRight: Radius.circular(20),
                ),
                child: Image.asset('assets/images/furniture/img_product_1.jpg'),
              ),
            ),
          ],
        ),
      ),
...
```

Kemudian set config assets di pubspec.yaml

```yaml
assets:
  - assets/images/furniture/
```

Jangan lupa masukan gambar nya ke folder yang sudah didaftakan ke config assets.

Output:

![Gambar 11. Widget Image](img/10%20image.png)

Gambar 11. Widget Image

Untuk implementasi di dunia nyata, nanti anda bisa membuat tampilan seperti berikut:

![Gambar 12. Implementasi Image](img/11%20implementasi%20image.PNG)

Gambar 12. Implementasi Image

Baca Dokumentasi Resmi:

- [Image.](https://api.flutter.dev/flutter/widgets/Image-class.html)

## CircleAvatar

Ini adalah widget yang selalu berbentuk lingkaran yang mempunyai background warna atau gambar. Biasa digunakan untuk gambar profil user. Walau tidak menutup kemungkinan untuk urusan lain yang penting urusan bentuk lingkaran dengan latar belakang gambar dan warna. Seperti contoh dibawah. Disini kita membuat profile picture menggunakan CircleAvatar dengan radius 50. Lalu kita membuat row yang isinya widget lingkaran dengan latar belakang warna dengan radius 40.

```dart
...
  Widget build(BuildContext context) {
    List<Color> colors = [
      Colors.red,
      Colors.green,
      Colors.blue,
    ];
    return Scaffold(
      appBar: AppBar(
        title: const Text("Coding Flutter - CircleAvatar"),
      ),
      body: Container(
        padding: const EdgeInsets.all(10.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            const CircleAvatar(
              radius: 50,
              backgroundImage: NetworkImage('https://picsum.photos/200'),
            ),
            Row(
              children: [
                ...List.generate(
                  colors.length,
                  (index) => Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: CircleAvatar(
                      radius: 20,
                      backgroundColor: colors[index],
                    ),
                  ),
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
...
```

Output:

![Gambar 12. Widget CircleAvatar](img/12%20circleavatar.png)

Gambar 12. Widget CircleAvatar

Untuk implementasi di dunia nyata, nanti anda bisa membuat tampilan seperti berikut:

![Gambar 13. Implementasi CircleAvatar](img/13%20implementasi%20circleavatar.PNG)

Gambar 13. Implementasi CircleAvatar

Baca Dokumentasi Resmi:

- [CircleAvatar.](https://api.flutter.dev/flutter/material/CircleAvatar-class.html)

# [Materi Selanjutnya: Layout](layout.md)
