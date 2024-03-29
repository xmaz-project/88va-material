# SASIハードディスク

SASIハードディスクは BIOS/PC-Engine にてサポートされている。ハードディスクからの起動も可。

* インタフェースボード
  * VA用
    * [PC-88VA-21 5インチ固定ディスクインタフェースボード](https://support.nec-lavie.jp/product-info?prodId=PC-88VA-21)
  * その他、PC-9801VM対応のCバスボードなら基本的に動くと思われる。
* ハードディスクドライブ
  * 5M, 10M, 20M, 40M

補足
* インタフェースボード上のROMは利用しないため、ジャンパスイッチなどの設定で可能なら切り離してよい。
* 2台まで接続可能。
* 使用するリソース
  * I/Oポート 0080h, 0082h
  * 割込みチャンネル IR9 (UINT3)
  * DMAチャンネル #0 か？

## 接続確認

PC-Engine起動後、SASIハードディスクに割り当てられたドライブレターを確認する。
フロッピーから起動した場合はA:, B:がフロッピー、C:, D: がSASIハードディスクとなる。

* ASSIGNコマンドで確認 (PC-Engine 1.1 のみ利用可。)
  ```
  ASSIGN
  ```
  接続しているドライブが表示される。
  ```
  A:  FD0
  B:  FD1
  C:  HD0   ← この「HD0」が表示されればOK。
  ```
* DIRコマンドで確認
  ```
  DIR C:
  ```
  次のような応答ならハードディスクが認識されていない。
  ```
  ドライブ名が間違っています。ドライブ名は A: から B: の範囲で指定してください。
  ```

## 初期化

### フォーマット

PC-Engineシステムディスクの`HDFORM.COM`を利用する。フォーマットするドライブを引数に指定する。
```
HDFORM C:
ドライブ C: のハードディスク（ユニット＃１ ４０Mバイトタイプ）をフォーマットし
ます。
よろしいですか <Y/N>?
```

### システムファイルのコピー

起動ディスクとして使う場合は `SYS` コマンドでシステムファイルをコピーする。
転送先のドライブを引数に指定する。
転送元はカレントドライブとなる。
たとえば A: にシステムディスクを挿入して、
```
A:
SYS C:
```

転送先の領域にすでにファイルがあると転送できない。転送先のドライブは空にしておくのがよい。

## 起動設定

セットアップ画面 (PCキーを押しながら電源ON) で設定する。

## 関連情報

* [3.1    ＨＤＤで３２Ｍバイト以上使うとおかしくなったのですが？](http://www.pc88.gr.jp/vafaq/view.php/article/88va/vafaq/34)
* [3.2    ＶＡで使えるＨＤＤを教えてください。](http://www.pc88.gr.jp/vafaq/view.php/article/88va/vafaq/35)

## TODO

* DMAチャンネル
* 正規のシステムディスクがない場合、`HDFORM.COM` の代替は？
