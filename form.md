# Form

[Kembali](layout.md)

Di dalam bab Form dasar, akan dipelajari Widget-widget berikut:

- [TextField](#textfield)
- [DropdownButton](#dropdownbutton)
- [Switch](#switch)
- [Radio](#radio)
- [Checkbox](#checkbox)
- [DatePicker](#datepicker)
- [Dialog](#dialog)
- [BottomSheet](#bottomsheet)
- [Snackbar](#snackbar)

## TextField

Bidang teks atau `TextField` memungkinkan user untuk memasukkan teks, baik dengan keyboard fisik maupun keyboard dilayar.

`TextField` memanggil callback `onChanged` setiap kali user mengubah teks di bidang. Jika pengguna menunjukkan bahwa mereka telah selesai mengetik di bidang (misal dengan menekan tombol Enter di keyboard), `TextField` akan memanggil callback `onSubmitted`

Untuk mengontrol teks yang ditampilkan di bidang teks, gunakan `controller`. Misalnya, untuk mengatur nilai awal bidang teks, gunakan `controller` yang sudah berisi beberapa teks. Controller juga dapat mengontrol wilayah pemilihan dan penulisan (dan untuk mengamati perubahan pada teks, pemilihan, dan wilayah penulisan).

Secara default, bidang teks memiliki dekorasi yang menggambar pembatas di bawah bidang teks. Anda dapat menggunakan properti `decoration` untuk mengontrol dekorasi, misalnya dengan menambahkan label atau ikon. Jika Anda menyetel properti dekorasi ke null, dekorasi akan dihapus seluruhnya, termasuk padding tambahan yang dimasukkan oleh dekorasi untuk menghemat ruang bagi label.

```
TextField
│───controller
|   |───TextEditingController()
│───onChanged
|   |───Function(String)
│───onSubmitted
|   |───Function(String)
│───obscureText
|   |───bool
│───autoFocus
|   |───bool
│───focusNode
|   |───FocusNode()
│───maxLines
│───autocorrect
|   |───bool
│───style
|   |───TextStyle()
│───keyboardType
|   |───TextInputType()
|   |   |───text
|   |   |───number
|   |   |───emailAddress
|   |   |───dll.
│───textAlign
|   |───TextAlign()
|   |   |───center
|   |   |───start
|   |   |───end
|   |   |───justify
|   |   |───dll.
│───textCapitalization
|   │───TextCapitalization
|   |   |───sentences
|   |   |───characters
|   |   |───words
│───textCapitalization
|   │───TextCapitalization
|   |   |───sentences
|   |   |───characters
|   |   |───words
│───decoration
|   │───InputDecoration
|   |   |───hintText
|   |   |───labelText
|   |   |───helperText
|   |   |───icon
|   |   |───prefixIcon
|   |   |───border
|   |   |   |───OutlineInputBorder()
```

Contoh code dibawah ini ceritanya saya ingin membuat text field dengan panjang karakter input 20, terdapat controller untuk mengontrol textfield, ada decoration dengan label Name, lalu terdapat border underline berwarna bluegrey dan ada onchange juga yang bisa kita pakai untuk melihat perubahan tiap kali textfield di edit.

```dart
import 'package:flutter/material.dart';

class MyTextField extends StatefulWidget {
  const MyTextField({super.key});

  @override
  State<MyTextField> createState() => _MyTextFieldState();
}

class _MyTextFieldState extends State<MyTextField> {
  final textController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return TextField(
      maxLength: 20,
      controller: textController,
      decoration: const InputDecoration(
        labelText: "Nama",
        labelStyle: TextStyle(color: Colors.blueGrey),
        enabledBorder: UnderlineInputBorder(
          borderSide: BorderSide(color: Colors.blueGrey),
        ),
        helperText: "Masukkan nama",
      ),
      onChanged: (value) {},
    );
  }
}
```

Output:

![Gambar 32. Widget TextField](img/31%20textfield.png)

Gambar 32. Widget TextField

Hasilnya seperti gambar diatas dimana terdapat TextField dengan label Nama dan border underline bluegery serta tanda max karakter 20 dan helper noted Masukkan nama

Baca Dokumentasi Resmi:

- [TextField.](https://api.flutter.dev/flutter/material/TextField-class.html)

## DropdownButton

`DropdownButton` memungkinkan user memilih dari sejumlah item. Tombol menunjukkan item yang dipilih saat ini, serta panah yang membuka menu untuk memilih item lain.

Seperti kode dibawah, saya membuat dropdownbutton disampingnya text your favorite language. Properties value wajib di isi dan wajib ada datanya di dalam item dengan value item wajib ada salah satunya itu yg terdapat di properties value.

```dart
import 'package:flutter/material.dart';

class MyDropDown extends StatefulWidget {
  const MyDropDown({super.key});

  @override
  State<MyDropDown> createState() => _MyDropDownState();
}

class _MyDropDownState extends State<MyDropDown> {
  String selected = "Dart";

  final List<String> dropDownList = const [
    "Dart",
    "Kotlin",
    "Java",
    "Javascript",
    "PHP",
    "Python",
    "Ruby",
    "Swift",
  ];

  @override
  Widget build(BuildContext context) {
    return Row(
      crossAxisAlignment: CrossAxisAlignment.center,
      mainAxisAlignment: MainAxisAlignment.start,
      children: [
        const Text("Bahasa favorit: "),
        const SizedBox(width: 8),
        DropdownButton(
          value: selected,
          icon: const Icon(Icons.arrow_drop_down),
          iconSize: 20,
          style: TextStyle(color: Colors.blue[600]),
          underline: Container(
            decoration: const BoxDecoration(
              border: Border(
                bottom: BorderSide(
                  color: Colors.grey,
                  width: 3,
                ),
              ),
            ),
          ),
          items: dropDownList.map((String value) {
            return DropdownMenuItem(
              value: value,
              child: Text(value),
            );
          }).toList(),
          onChanged: (val) {
            setState(() {
              if (val != null) selected = val;
              print(selected);
            });
          },
        ),
      ],
    );
  }
}
```

Output:

![Gambar 33. Widget DropdownButton](img/32%20dropdown.png)

Gambar 33. Widget DropdownButton

Baca Dokumentasi Resmi:

- [DropdownButton.](https://api.flutter.dev/flutter/material/DropdownButton-class.html)

- [DropdownMenuItem.](https://api.flutter.dev/flutter/material/DropdownMenuItem-class.html)

## Switch

`Switch` atau saklar adalah widget yang digunakan untuk memilih di antara dua opsi, AKTIF atau NONAKTIF. Dia tidak mempunya state sendiri. Untuk mempertahankan state nya, kita perlu memanggil properti onChanged. Jika nilai yang dikembalikan oleh properti ini adalah true, maka switch akan ON dan false saat OFF.

```
Switch
│───value
|───onChanged
```

Seperti code dibawah ini, state nya akan diubah dengan bantuan `onChanged` lalu dibantu dengan `setState((){})` untuk mengupdate value switch dengan value yang baru untuk mempertahankan nilai nya.

```dart
import 'package:flutter/material.dart';

class MySwitch extends StatefulWidget {
  const MySwitch({super.key});

  @override
  State<MySwitch> createState() => _MySwitchState();
}

class _MySwitchState extends State<MySwitch> {
  bool isOn = false;
  @override
  Widget build(BuildContext context) {
    return Row(
      children: [
        const Text("Connect Instagram"),
        Switch(
          value: isOn,
          onChanged: (bool? val) {
            if (val != null) {
              setState(() {
                isOn = val;
                print("Switch: $isOn");
              });
            }
          },
        ),
      ],
    );
  }
}
```

Output:

![Gambar 34. Widget Switch](img/)

Gambar 34. Widget Switch

Baca Dokumentasi Resmi:

- [Switch.](https://api.flutter.dev/flutter/material/Switch-class.html)

## Radio

## Checkbox

## DatePicker

## Dialog

## BottomSheet

## Snackbar
