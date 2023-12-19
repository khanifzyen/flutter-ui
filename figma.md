# Figma

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
      - title_price_star_detail.dart
      - color_picker_detail.dart
      - quantity_detail.dart
      - add_to_cart_detail.dart

Ini adalah rancangan awal, dengan membreakdown widget menjadi bagian yang lebih kecil. Seiring berjalannya waktu, widget-widget diatas bisa bertambah.

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

Fitur Home terdiri dari satu halaman yaitu HomePage()
