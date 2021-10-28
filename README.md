# MOBILE-PROGRAMMING
just random stuff

pada soal no 6 dijelaskan cara membangun aplikasi flutter dari awal membuat item scroll widget sebagai berikut:
1. buatlah project flutter dengan nama apapun bisa menggunkan CLI, ANDROID STUDIO atau VS CODE namun kali ini saya akan menggunakan CLI dengan sistem operasi windows 10
2. langkah pertama tentukan difoolder mana yang akan dibuat project, misalkan folder document, kemudia buatlah 1 folder bernama projetc, setelah itu masuk ke terminal, ketik create flutter (nama project) misalnya app_first
3. pastikan koneksi internet lancar.
4. setelah berhasil buka cmd kemudia arahkan ke folder project yang sudah dibuat misalkan cd C:\Users\SUCIPTO DJAMIN\Documents\project\app_first
5. setelah berhasil jalankan kode dengan cara ketik flutter run, kemudian pilih browser apa yang ingin digunakan untuk menjalankan flutter, 1. chrome. 2 edge kali ini kita pilih chrome
6. tunggu sebentar makan project akan muncul.
7. untuk membuat program, kita akan mengubah isi file lib/main.dart dalam hal ini membuat hello world.
8. import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Welcome to Flutter',
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Welcome to Flutter'),
        ),
        body: const Center(
          child: Text('Hello World'),
        ),
      ),
    );
  }
}

9. simpan dan jalankan file dengan cara buka terminal lagi kemudia ketik flutter run. maka akan muncul tulisan hellow world
10. kedudian untuk menambahkan external package buka file  pubspec.yaml  dan tambakan english_words sehingga menjadi dependencies:
11.
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
  english_words: ^4.0.0
11. kemudian jalankan flutter pub get pada terminal.
12. buka kembali file main.dart tambakan import 'package:english_words/english_words.dart'; sehingga menjadi class MyApp extends StatelessWidget {
	    @override
	    Widget build(BuildContext context) {
    final wordPair = WordPair.random();
	      return MaterialApp(
	        home: Scaffold(
	          appBar: AppBar(
	            title: const Text('Welcome to Flutter'),
	          ),
         body: const Center(
          child: Text('Hello World'),
        body: Center(
          child: Text(wordPair.asPascalCase),
	          ),
	       ),
	      ); 
        
13. kemudian masih difile yang sama akan ditambakan statefull widget dalam hal ini digunakan fungsi RandomWords dimana akan menampilkan random kata,


import 'package:english_words/english_words.dart';
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Welcome to Flutter',
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Welcome to Flutter'),
        ),
        body: Center(
          child: RandomWords(),
        ),
      ),
    );
  }
}

// #docregion _RandomWordsState, RWS-class-only
class _RandomWordsState extends State<RandomWords> {
  // #enddocregion RWS-class-only
  @override
  Widget build(BuildContext context) {
    final wordPair = WordPair.random();
    return Text(wordPair.asPascalCase);
  }
}
class RandomWords extends StatefulWidget {
  @override
  State<RandomWords> createState() => _RandomWordsState();
}

14. kemudian pada tahap ke 4 akan ditambahkan infinity scrolling menggunkaan fungsi List View.
15. untuk melakukan tersebut tambahkan kelas _suggestions  ke kelas _RandomWordsState dan juga tambahkan _biggerFont  untuk font
16. untuk kodenya 
  // Copyright 2018 The Flutter team. All rights reserved.
// Use of this source code is governed by a BSD-style license that can be
// found in the LICENSE file.

import 'package:english_words/english_words.dart';
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

// #docregion MyApp
class MyApp extends StatelessWidget {
  // #docregion build
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Startup Name Generator',
      home: RandomWords(),
    );
  }
  // #enddocregion build
}
// #enddocregion MyApp

// #docregion RWS-var
class _RandomWordsState extends State<RandomWords> {
  final _suggestions = <WordPair>[];
  final _biggerFont = const TextStyle(fontSize: 18.0);
  // #enddocregion RWS-var

  // #docregion _buildSuggestions
  Widget _buildSuggestions() {
    return ListView.builder(
        padding: const EdgeInsets.all(16.0),
        itemBuilder: /*1*/ (context, i) {
          if (i.isOdd) return const Divider(); /*2*/

          final index = i ~/ 2; /*3*/
          if (index >= _suggestions.length) {
            _suggestions.addAll(generateWordPairs().take(10)); /*4*/
          }
          return _buildRow(_suggestions[index]);
        });
  }
  // #enddocregion _buildSuggestions

  // #docregion _buildRow
  Widget _buildRow(WordPair pair) {
    return ListTile(
      title: Text(
        pair.asPascalCase,
        style: _biggerFont,
      ),
    );
  }
  // #enddocregion _buildRow

  // #docregion RWS-build
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Startup Name Generator'),
      ),
      body: _buildSuggestions(),
    );
  }
  // #enddocregion RWS-build
  // #docregion RWS-var
}
// #enddocregion RWS-var

class RandomWords extends StatefulWidget {
  @override
  State<RandomWords> createState() => _RandomWordsState();
}
