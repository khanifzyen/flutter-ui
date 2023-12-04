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

# Basic Widget

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

## AppBar

AppBar selalu ditempatkan di bagian atas layar. Jika scaffold mempunyai drawer, maka button icon hamburger (yang terletak di property leading) akan ditambahkan secara otomatis untuk menangani open close drawer.

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

![Gambar 2. AppBar](img/02%20appbar.png)

Gambar 2. AppBar

## Container

## Text

## Button

## Icon

## Images

## CircleAvatar

# Layout

# Form

# Navigator

# Figma

##
