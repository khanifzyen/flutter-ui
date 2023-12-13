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

![Gambar 34. Widget Switch](img/33%20switch.png)

Gambar 34. Widget Switch

Baca Dokumentasi Resmi:

- [Switch.](https://api.flutter.dev/flutter/material/Switch-class.html)

## Radio

Digunakan untuk memilih di antara sejumlah nilai yang sudah ditentukan. Ketika satu tombol radio dalam grup dipilih, tombol radio lain dalam grup tidak lagi dipilih. Nilainya bertipe tipe yang sama, parameter tipe dari kelas Radio. Enum biasanya digunakan untuk tujuan ini.

Tombol radio itu sendiri tidak mempertahankan state apa pun. Sebagai gantinya, radio akan memanggil callback onChanged, meneruskan nilai sebagai parameter. Jika groupValue dan nilai cocok, radio ini akan dipilih. Sebagian besar widget akan merespons onChanged dengan memanggil setState untuk memperbarui groupValue pada tombol radio

```
Radio
│───value
|───onChanged
|───groupValue
|───selected
```

Seperti contoh kode dibawah, saya membuat groupValue dengan group param sex dan default valuenya male.

Lalu group valuenya akan diganti melalui properties onChanged nya ketika di klik akan mentriger properties ini dan mengupdate value nya.

```dart
import 'package:flutter/material.dart';

class MyRadio extends StatefulWidget {
  const MyRadio({super.key});

  @override
  State<MyRadio> createState() => _MyRadioState();
}

class _MyRadioState extends State<MyRadio> {
  String sex = "pria";

  @override
  Widget build(BuildContext context) {
    return Row(
      children: [
        const Text("Jenis Kelamin: "),
        const SizedBox(width: 8),
        Row(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Radio(
              value: 'pria',
              groupValue: sex,
              onChanged: (value) {
                setState(() {
                  if (value != null) {
                    sex = value;
                    print("sex: $sex");
                  }
                });
              },
            ),
            const Text("Pria"),
          ],
        ),
        const SizedBox(width: 16),
        Row(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Radio(
              value: "wanita",
              groupValue: sex,
              onChanged: (value) {
                setState(() {
                  if (value != null) {
                    sex = value;
                    print("sex: $sex");
                  }
                });
              },
            ),
            const Text("Wanita"),
          ],
        ),
      ],
    );
  }
}
```

Hasil kodenya seperti dibawah ini. Jika di klik male,maka female akan otomatis tidak terpilih dan sebaliknya.

Output:

![Gambar 35. Widget Radio](img/35%20radio.png)

Gambar 35. Widget Radio

Baca Dokumentasi Resmi:

- [Radio.](https://api.flutter.dev/flutter/material/Radio-class.html)

## Checkbox

Kotak centang atau checkbox, tidak mempertahankan statusnya sendiri. Sebagai gantinya, saat nilai checkbox berubah, widget akan memanggil callback onChanged untuk mengupdate nilai param yang dipakai di valuenya. Sebagian besar widget yang menggunakan checkbox akan mendengarkan callback onChanged dan membuat ulang checkbox dengan nilai baru untuk memperbarui tampilan visual checkbox.

Kotak centang secara opsional dapat menampilkan tiga nilai - true, false, dan null. Ketika nilainya null, tanda hubung ditampilkan. Secara default mempunyai value false dan value checkbox harus true atau false.

```
Checkbox
│───value
|───onChanged
|───activeColor
|───selected
```

Seperti contoh code disamping ini, saya membuat satu checkbox dengan value default false. Lalu ketika di klik akan mentriger onChanged dan value isCheckednya akan terupdate dengan data dari checkboxnya dan di rebuild ulang dengan bantuan setState

```dart
import 'package:flutter/material.dart';

class MyCheckbox extends StatefulWidget {
  const MyCheckbox({super.key});

  @override
  State<MyCheckbox> createState() => _MyCheckboxState();
}

class _MyCheckboxState extends State<MyCheckbox> {
  bool isChecked = false;

  @override
  Widget build(BuildContext context) {
    return Row(
      children: [
        Checkbox(
          value: isChecked,
          onChanged: (value) {
            setState(() {
              if (value != null) {
                isChecked = value;
                print("setuju: $isChecked");
              }
            });
          },
        ),
        const SizedBox(width: 4),
        const Text(
          "Setuju syarat dan ketentuan.",
          style: TextStyle(decoration: TextDecoration.underline),
        ),
      ],
    );
  }
}
```

Output:

![Gambar 36. Widget Checbox](img/36%20checkbox.png)

Gambar 36. Widget Checkbox

Baca Dokumentasi Resmi:

- [Checkbox.](https://api.flutter.dev/flutter/material/Checkbox-class.html)

## DatePicker

`showDatePicker` akan menampilkan dialog yang berisi pemilih tanggal. Future await akan mengembalikan tanggal yang dipilih oleh user saat user mengkonfirmasi dialog. Jika pengguna membatalkan dialog, akan mengembalikan null.

Saat pemilih tanggal pertama kali ditampilkan, ini akan menampilkan bulan tanggal awal, dengan tanggal awal dipilih. `firstDate` adalah tanggal paling awal yang diperbolehkan. `lastDate` adalah tanggal terbaru yang diperbolehkan. tanggal awal harus jatuh di antara tanggal-tanggal ini, atau sama dengan salah satunya.

```dart
import 'package:flutter/material.dart';

class MyDatePicker extends StatefulWidget {
  const MyDatePicker({super.key});

  @override
  State<MyDatePicker> createState() => _MyDatePickerState();
}

class _MyDatePickerState extends State<MyDatePicker> {
  TextEditingController dateController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return InkWell(
      onTap: () async {
        DateTime? pickedDate = await showDatePicker(
          context: context,
          initialDate: DateTime.now(),
          firstDate: DateTime(1950),
          lastDate: DateTime(2100),
        );
        setState(() {
          if (pickedDate != null) {
            dateController.text = pickedDate.toString();
          }
        });
        debugPrint("Date Picker: $pickedDate");
      },
      child: TextFormField(
        initialValue: "2023-12-11",
        maxLength: 20,
        enabled: false,
        decoration: const InputDecoration(
          labelText: "Tanggal Lahir",
          labelStyle: TextStyle(color: Colors.blueGrey),
          enabledBorder: UnderlineInputBorder(
            borderSide: BorderSide(color: Colors.blueGrey),
          ),
          suffixIcon: Icon(Icons.date_range),
          helperText: "Pilih tanggal lahir anda",
        ),
        onChanged: (value) {},
      ),
    );
  }
}
```

Code tersebut bila kita running hasilnya akan seperti gambar dibawah ini. Pertama tampilan berupa textfield dan ketika diklik maka dialog calendar untuk memilih tanggal akan muncul dan kita dapat meng select salah satunya lalu kita ada pilihan ok atau cancel.

Output:

![Gambar 37. Widget DatePicker](img/37%20datepicker.png)

Gambar 37. Function `showDatePicker` yang mengembalikan `DateTime`

Baca Dokumentasi Resmi:

- [showDatePicker.](https://api.flutter.dev/flutter/material/showDatePicker.html)

## Dialog

Dialog adalah jenis jendela modal yang muncul di depan konten aplikasi untuk memberikan informasi penting atau meminta keputusan. Dialog menonaktifkan semua fungsionalitas aplikasi saat muncul, dan tetap berada di layar hingga dikonfirmasi, ditutup, atau tindakan yang diperlukan telah dilakukan.Dialog sengaja mengganggu, sehingga harus digunakan secara cermat.

```
Dialog
│───showDialog()
|   │───context
|   │───builder
|   │───barrierDismissable
|   |   │───bool
|───AlertDialog
|   │───title
|   |   │───Widget
|   │───content
|   |   │───Widget
|   │───actions
|   |   │───List<Widget>
|   |   |   │───TextButton()
|   │───elevation
|   │───backgroundColor
|   │───shape
|   |   │───CircleBorder()
|   |   │───RoundedRectangleBorder()
|───SimpleDialog
|   │───title
|   │───children
|   |   │───List<Widget>
|   |   |   │───SimpleDialogOption()
|───showGeneralDialog()
|   |───context
|   |───pageBuilder
```

Contoh code disamping ini saya mempunya button dengan text Open Dialog, dan ketika di klik maka akan menjalankan onPressed dan menjalankan showDialog, disini saya mengembalikan AlertDialog dengan berisi title, content dan action.

```dart
import 'package:flutter/material.dart';

class MyDialog extends StatefulWidget {
  const MyDialog({super.key});

  @override
  State<MyDialog> createState() => _MyDialogState();
}

class _MyDialogState extends State<MyDialog> {
  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: () async {
        await showDialog<void>(
          context: context,
          builder: (BuildContext context) {
            return AlertDialog(
              title: const Text('Info'),
              content: const SingleChildScrollView(
                child: ListBody(
                  children: [
                    Text('Your order was placed.'),
                  ],
                ),
              ),
              actions: [
                ElevatedButton(
                  style: ElevatedButton.styleFrom(
                    backgroundColor: Colors.blue,
                  ),
                  child: const Text('Ok'),
                  onPressed: () {
                    Navigator.of(context).pop();
                  },
                ),
              ],
            );
          },
        );
      },
      child: const Text('Open Dialog'),
    );
  }
}
```

Output:

![Gambar 38. Widget AlertDialog](img/38%20dialog.png)

Gambar 38. Function `showDialog` yang mengembalikan `AlertDialog`

Baca Dokumentasi Resmi:

- [showDialog.](https://api.flutter.dev/flutter/material/showDialog.html)

- [AlertDialog.](https://api.flutter.dev/flutter/material/AlertDialog-class.html)

## BottomSheet

Bottom sheet adalah tampilan tambahan yang muncul dibagian bawah yang umum digunakan pada ponsel.

Ada tiga penggunaan yang cocok untuk tiap kasusnya:

- Bottom sheet standar: menampilkan konten yang melengkapi konten utama layar. Bottom sheet tetap terlihat saat user berinteraksi dengan konten utama.
- Bottom sheet modal adalah alternatif untuk dialog sederhana di seluler dan menyediakan ruang untuk item tambahan, deskripsi yang lebih panjang, dan ikonografi. Mereka harus ditutup untuk berinteraksi dengan konten aplikasi utamanya.
- Bottom sheet yang menyediakan permukaan kecil yang diciutkan yang dapat diperluas oleh user untuk mengakses fitur atau tugas utama. Mereka menawarkan akses tetap bottom sheet standar dengan ruang dan fokus bottom sheet modal

```
BottomSheet
│───showModalBottomSheet()
|   │───context
|   │───builder
```

Contoh kode dibawah, saya mempunyai button open bottomsheet dan ketika saya klik maka akan menjalan onPressed function dan mentriger showModalBottomSheet sehingga widget yang di return oleh nya akan muncul di bagian bawah.

```dart
import 'package:flutter/material.dart';

class MyBottomSheet extends StatefulWidget {
  const MyBottomSheet({super.key});

  @override
  State<MyBottomSheet> createState() => _MyBottomSheetState();
}

class _MyBottomSheetState extends State<MyBottomSheet> {
  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: () async {
        showModalBottomSheet<void>(
          context: context,
          builder: (BuildContext context) {
            return Padding(
              padding: const EdgeInsets.all(20),
              child: SizedBox(
                width: MediaQuery.of(context).size.width,
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  mainAxisSize: MainAxisSize.min,
                  children: [
                    const Text('Your order was placed!'),
                    const SizedBox(height: 20),
                    ElevatedButton(
                      style: ElevatedButton.styleFrom(
                        backgroundColor: Colors.blue,
                      ),
                      onPressed: () {
                        Navigator.pop(context);
                      },
                      child: const Text('Ok'),
                    ),
                  ],
                ),
              ),
            );
          },
        );
      },
      child: const Text('Open BottomSheet'),
    );
  }
}
```

Output:

![Gambar 39. Widget BottomSheet](img/39%20bottomsheet.png)

Gambar 39. Function `showBottomSheet` yang mengembalikan `WidgetBuilder`

Baca Dokumentasi Resmi:

- [showBottomSheet.](https://api.flutter.dev/flutter/material/ScaffoldState/showBottomSheet.html)

- [BottomSheet.](https://api.flutter.dev/flutter/material/BottomSheet-class.html)

## Snackbar

Widget ini bermanfaat untuk memberi tahu user secara singkat saat tindakan tertentu terjadi. Misalnya, saat user menghapus pesan dalam daftar, Anda mungkin ingin memberitahu mereka bahwa pesan tersebut telah dihapus. Anda bahkan mungkin ingin memberi mereka opsi untuk membatalkan tindakan.

Seperti contoh kode didibawah, snackbar saya trigger ketika saya klik button Open Snackbar

```dart
...
    return ElevatedButton(
      onPressed: () {
        ScaffoldMessenger.of(context).showSnackBar(
          const SnackBar(
            backgroundColor: Colors.blue,
            content: Text('Your request is succesful'),
          ),
        );
      },
      child: const Text('Open SnackBar'),
    );
...
```

Output:

![Gambar 40. Widget Snackbar](img/40%20snackbar.png)

Gambar 40. Function `showSnackBar` dengan parameter `SnackBar`

Baca Dokumentasi Resmi:

- [showSnackBar.](hhttps://api.flutter.dev/flutter/material/ScaffoldMessengerState/showSnackBar.html)

- [SnackBar.](https://api.flutter.dev/flutter/material/SnackBar-class.html)

# [Materi Selanjutnya: Navigator](navigator.md)
