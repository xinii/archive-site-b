---
title: Operating system introduction and coding system of emacs
tags: [OS, Emacs, Coding, Japanese]
style: fill
color: light
description: WindowsとLinux、Emacs モードライン、set-buffer-file-coding-system
comments: true
---

Source: [新城 靖](http://www.coins.tsukuba.ac.jp/~yas/coins/literacy-2014/2014-05-30/)
（勉強文，内容変更あり）

## PC

PCには、いくつかの意味がある。

- 一般名詞: 個人用のコンピュータ(a personal computer)。パソコン。この意味なら、iMacやMac Bookも含む。

- 固有名詞: IBM社が最初に発売したコンピュータの名前(IBM PC)、および、その後継機や互換機。この意味なら、iMacやMac Bookを含まない。

#### デュアルブートとマルチブート

1台のコンピュータ・ハードウェアで、電源投入後に複数のOSを選択的に実行で
きることをマルチブートという。2つのOSの場合は、デュアル・ブートという。

#### シャットダウン

シャットダウンとは、安全にコンピュータの電源を切る（コンピュータを停止
させる）ことを意味する。いきなり電源コードを抜く等して切ると、不整合が
生じるので行ってはならない。

shutdown というコマンドもあるが、システム管理者しか使えないことが一般的
である。

## Windows

オペレーティング・システムの１つ。

Unix (MacOSX) との共通点：

- ファイルの考え方。木構造に基づきファイルに名前をつける。
- プロセスの考え方。
- ログイン（ログオン、サインイン）、ログアウト（ログオフ、サインアウト）
- コマンドラインでの利用(端末とコマンドプロンプト)
- ユーザとグループに基づくアクセス制御
- ウインドウの考え方

細かい相違点：

- ファイル名の区切りが「\」(ASCII 5c。「＼」か「￥」と表示される)」。
- テキスト・ファイルの漢字コードとしてShift_JIS が多く使われる。(UTF-8など、他のコードが使われることもある。)
- テキスト・ファイルの行末コードとして、ASCIIのCarriage Return + New Line (Line Feed) (CR+NL, 16進数で 0d+0a、^M+^J、C言語の表記で \r\n)が多く使われる。
- その他、多数

#### ドライブ」の考え方

Windows では、ファイルをディレクトリの木構造で扱うが、ディレクトリの木
構造と独立に「ドライブ」の名前(アルファベット１文字＋「:」)がつく。

「ドライブ」は、フロッピ・ディスクの時代には、複数の子供の「ディレクト
リ」の代わりにつかっていた。当時は、「ディレクトリ」は、ドライブに１個
しか存在しなかった。以下の例では、dir コマンド (ls コマンド相当) にドラ
イブ名を与えて実行している。

```
A> dir
（Aドライブのファイル一覧の表示）
A> dir b:
（Bドライブのファイル一覧の表示）
```

cd のように、作業中のドライブを切り替えることができる。
A> や B> は、プロンプトである。

```
A> b:
B> a:
A> 
```

Windowsの全身のMS-DOSにUnixと同様の木構造に基づくディレクトリがついたのは、1983年ごろ。

#### プログラムの実行

プログラムを実行するには、次のような方法がある。

- 「スタート」画面から探して選択する。
- 「スタート」画面の「すべてのプログラム」から探して選択する。
-  エクスプローラ(Explore)でプログラムが含まれているファイルを探してアイコンをダブルクリックする
- 「コマンドプロンプト」でプログラムの名前を打ち込む
- 「ファイル名を指定して実行」でプログラムの名前を打ち込む

#### コマンドプロンプト

MacOSXでiTermなどの端末を実行した時と同じ状態になる。

「スタートメニュー」から「アクセサリ→コマンドプロンプト」を選択する。

次のコマンドは、覚える。

- change directory: `cd`
- ディレクトリの表示。ls -l 相当: `dir`
- ディレクトリの表示。ls 相当: `dir /w`
- テキストファイルの表示: `type filename`

#### 移動プロファイル

Windows 8.1 (その前身の Windows 7/Vista/XP/2000/NT含む)は、
もともと「個人用(personal)」で使うために設計された Windows 95 以前のし
がらみをかなり背負っている。

「個人用(personal)」コンピュータでは、複数人用の設定を保存する必要がない。
すべての設定は一人のためのものである。

この考え方は、次のような時代に破綻した。

- １台の「個人用」コンピュータを、複数人で使う。
- ネットワークで、複数の(個人用)コンピュータを接続して使う。

Windows Vistaなどで、個人の設定は、「プロファイル」と呼ばれる。
ターゲットコンピューティング環境では、プロファイルをサーバに保存している。

- サインイン時(ログオン時)
  - サーバから個々のクライアント・パソコンにプロファイルを「コピー」する。
- 使用時
  - 個々のクライアント・パソコンにあるプロファイルを変更する。
- サインアウト時(ログオフ時)
  - 個々のクライアント・パソコンにあるプロファイルをサーバへ「コピー」しもどす。

コピーしもどす方法を「移動プロファイル(roaming profile)」という。

#### 移動プロファイルの問題点

- プロファイルが大きくなると、サインイン（ログオン）とサインアウト（ログオフ）に時間がかかるようになる。これを避けるには、大きなファイルを移動プロファイルに乗らない場所（H:ドライブ）に置くと良い。
- 「コピー」なので、一度に複数の Windows 機にサインイン（ログオン）すると問題が生じる。サインアウト（ログオフ）時に、プロファイルが上書きされる。その結果、最後にサインアウト（ログオフ）したものだけが有効で、先にサインアウト（ログオフ）したものは、上書きされて失われることがある。

これを避けるには、Windows にサインイン（ログオン）するのは、
1度に1つのコンピュータだけにする。

#### コンテキスト・メニュー

一般的なメニューは、特定の場所を押すと、常に同じものが表示される。これ
に対して、コンテキスト・メニューとは、ポイントしている対象に応じて、実
行可能な操作の一覧をメニューとして表示したものである。

Windows では、マウスの右ボタンをコンテキスト・メニューの表示に使う(右ク
リック)。通常の操作（クリック、ダブルクリック）は、左ボタンを使う。

表示した後、項目を選択するのは、右クリックでも左クリックでもよい。

MacOSX でも、複数ボタンのマウスでは、右ボタンでコンテキスト・メニューが
表示される。１ボタンのマウスでは、コントロール・キーを押しながらボタン
を押す。

## Linux

Linux は、Unix系のオペレーティング・システムの一種であり、
MacOSX と利用方法の共通性が高い。

Linux は、もともとは、オペレーティング・システムの中心部分（カーネル）
の名前である。さまざまな業者がカーネルと独自のプログラムとセットにして
配布している(distribution)。Red Hat は、その配布業者の１つである。
CentOS は、Red Hat社が配布しているLinux に互換性があるフリーのものであ
る。

OS

- Unix 系
  - MacOSX
  - Linux
    - Red Hat
    - Debian
    - Ubuntu
    - CentOS
  - Solaris, SunOS, Open Solaris, OpenIndiana
  - FreeBSD, NetBSD, OpenBSD
- Windows 系

ターゲットiMacとPC では、Linux CentOS が利用可能になっている。

Linux では、「GNOME端末」を開くと、MacOSX の「iTerm」と
似た状態になる。

Linux で使われる端末 GNOME端末は、
MacOSX iTerm と同じ文字コード(UTF-8)が使われている。
両方とも変更可能である。

GNOME（GNU Network Object Model Environment) は、見栄えのよいグラフィカ
ル・ユーザ・インタフェースを持つ、一揃えのプログラム群を開発するプロジェ
クトの１つ。「端末」以外にも、いくつもの「GNOME」が付くプログラムかある。

## Emacs

#### Emacs モードライン

Emacs を実行すると、一番下から2行目、白黒反転した行がある。
これをモードラインという。モードラインは、次のようになっている。

```
-UUE:----F1  literacy-a2.txt   Top L1     (Text) -------------------------------
-UUU:----F1  literacy-a2.txt   All L1     (Text) -------------------------------
```

UUE や UUU の1文字目と2文字目 UU は、端末の文字コー
ド(キーボード入力と画面への出力)が UTF-8 であることを意味する。Dock か
ら実行されるEmacs では、この2文字は表示されない。3文字目のEや
Uは、バッファの文字コード(ファイルに保存する時ににも使われる)を
意味する。

文字コードとしては、次のものがよく現れる。

| 文字コード | モードライン | Emacsの設定             |
|------------|--------------|-------------------------|
| UTF-8      | U, u         | utf-8-unix              |
| EUC-JP     | E            | euc-jp-unix             |
| JIS        | J            | iso-2022-jp-unix, junet |
| Shift_JIS  | S            | shift_jis-unix          |
| Laten 1    | 1            | iso-8859-1-unix         |

UUE や UUU の次の「:」は、行末のコードを意味する。
行末のコードとしては、次のものがよく現れる。

| emacsでの表記  モードライン | 制御コード(16進数) | 説明          | Controlキー          | C言語表記           |      |
|-----------------------------|--------------------|---------------|----------------------|---------------------|------|
| -unix                       | :, (Unix)          | 0a            | nl (new line)        | Control+j           | \n   |
| -mac                        | (Mac), /           | 0d            | cr (carriage return) | Control+m           | \r   |
| -dos                        | (DOS), \           | 0d 0a (2文字) | cr nl                | Control+m Control+j | \r\n |

注意1: The Unix Super Text の表 12-2 は、古い。

注意2: dos は、Windows (の前進の MS-DOS Microsoft Disk Operating
System, CP/Mで使われていたもの)の意味。

#### set-buffer-file-coding-system

Emacs は、日本語を含めて様々な言語を扱うことができる。
日本語を扱う時には、次のような文字コードを使うことができる。

- utf-8-unix
- euc-jp-unix
- iso-2022-jp-unix (JIS)
- shift_jis-unix
- shift_jis-dos (Windows でよく使われる)

ファイルに保存する時の文字コードを変更するには、次の機能を使う。
（M-x (Esc x)の後、補完機能が使える）

```
M-x set-buffer-file-coding-system
```

coding-system として、utf-8-unix, euc-jp-unix, iso-2022-jp-unix, shift_jis-unix,
shift_jis-dos などを指定する（タブ・キーによる補完機能が使える）。

```
Coding system for saving file (default nil): euc-jp-unix
```

coding-systemを変えた後、他のファイルに保存したい時には、
write-file (C-x C-w)
が便利。

```
Write file: ~/新しいファイル名
```

#### insert-file

Emacs にはファイルを挿入する機能`insert-file (C-x i)`がある。

## 実習

#### Softwares

- Firefox (Mozilla Firefox)
- Thunderbird (Mozilla Thunderbird)
- ペイント
- Tera Term
- その他

#### スタートティップのコンテキスト・メニュー

- 「エクプローラー」の実行
- 「コマンドプロンプト」の実行
- ファイル名を指定して実行
- サインアウト
- シャットダウン
- 再起動

#### 「エクスプローラー」を開く

「エクスプローラー」は、MacOSX の Finder と同様に、ファイルやディレクト
リをブラウザするためのプログラムである。これを、次のような方法で明示的
に実行しする。

- スタートティップのコンテキスト・メニューを使う。
- デスクトップに表示されているディレクトリ(フォルダ)をクリックし、右クリックで「コンテキスト・メニュー」を表示し、その中から「開く」を選択する。
- デスクトップに表示されている「ゴミ箱」をクリックし、
右クリックで「コンテキスト・メニュー」を表示し、
その中から「開く」を選択する。

#### 「PC(コンピュータ)」を開く

次の何れかの方法で、「PC(コンピュータ)」を開く

- 「エクスプローラー」を使う。
  - 「エクスプローラー」を開く。
  - 次にウィンドウの左側に表示されているメニューで「PC」を選ぶ。
- スタート画面の「全てのアプリケーション」から「PC」か「コンピュータ」を選ぶ。
- その他

#### Windowsコマンドプロンプト

コマンドプロンプトを実行する

次のコマンドを使う(「\」は、「(「＼」や「￥」と表示される)」。)

- dir
- dir/w
- dir \
- dir h:\
- cd
- c:
- h: 
- date
- time
- hostname
- ipconfig
- type file
- echo hello
- help help more | more
- set
- set | more
- mkdir
- rmdir
- start h:\
- start .
- explorer
- その他

コマンドは大文字で打っても小文字で打っても同じように動作することを確認
しする。more コマンドは、lv と同じようなページャであり、スペース・キー
で 1 ページ進み、q で終了する。

#### Windowsコマンドプロンプト(2)

「コマンドプロンプト」では、Unix のシェルと同様に、
標準入出力の切り替え(redirection リダイレクション)が行なえることを確認する

```
dir > files.txt
type files.txt
```

#### Windowsコマンドプロンプト(3)

「コマンドプロンプト」では、Unix bashのファイル名補完機能と同様に、

タブによるファイル名の補完が行われることを確かめする。また、ファイル
名を何も打っていない状態でタブを打つと、ディレクトリの内容が次々と切り
替わる。このことを確かめる。

#### Windowsタスクマネージャ

Control+Alt+Delete キーを使って、タスクマネジャを実行しする。「アプリ
ケーション」や「プロセス」のタブを調べする。

「プロセス」のタブでは、CPU 時間の順番やメモリ使用量の順番に並べ替えな
さい。

強制終了しても問題がなさそうな「アプリケーション」や「プロセス」を、強
制終了してみする。

#### Windows Tera Term による遠隔ログイン

Tera Term を用いて遠隔ログインをしする。

- Tera Term を実行する。「スタートメニュー」を表示し、「すべてのプログラム→Tera Term→Tera Term」と選択する。
- 実行したら「新しい接続」というウインドウが表示される。「ホスト」に遠隔ログインししたいコンピュータの名前を打ち込む。たとえば、
「www.coins.tsukuba.ac.jp」と打ち込む。「サービス」としては、SSH、「TCPポート#」としては、22を選択する。最後に「OK」ボタンを押す。
- 最初にあるホストに接続した時には、次のような警告が出る。ホストの公開鍵の指紋(fingerprint)を確認する。確認できれば、「このホストをknown hosts リストに追加する」のチェックボックスにチェックを入れる。最後に、「接続」ボタンを押す。
- 次に「SSH認証」のウインドウが表示される。「ユーザ名」にユーザ名を打つ。coins iMac では「チャレンジレスポンス認証を使う（キーボードインタラクティブ）」を選ぶ。他のホストでは、「プレインテキストを使う」をチェックして「パスフレーズ」にパスワードを打つ必要がある場合もある。あるいは、公開鍵と秘密鍵の組みを用意して、「RSA/DSA鍵を使う」を選ぶ方法も使える。dn 
- 次のウインドウでは、パスワードを打ち、「OK」ボタンを押す。
- ログインに成功した後には、「設定」メニューの「端末」で、次のような項目を必要や好みに応じて調整する。
  - 端末サイズを 80 x 40 程度に大きくする。
  - 「=ウインドウサイズ」にチェックを入れる。
  - 漢字(受信)や漢字(送信)を、遠隔ログインしているホストに合わせる。coins iMac やサーバでは、UTF-8 にする。
  - 必要なら、設定を保存する。

#### Windows遠隔ログイン後のコマンド

Tera Term、PuTTY、ssh等にターゲット内の別のコンピュータに遠隔ログインする。次のコマンドを実行して、遠隔ログインを行っていない時（ローカルでの実行結果）と比較しする。

- ps, ps ux, ps aux
- top (終了はq)
- hostname
- who、who am i
- w
- finger
- uname -a
- arch
- uptime
- last
- open ~
- firefox
- cd, pwd, ls (別のディレクトリに移動するとどうなるか)

#### Unix: nkfコマンド

nkf (network kanji finter)は、Unix (iMac, Linux)で動作する漢字コードを
変換するためのプログラムである( ターゲットWindows 8.1 では動作しない)。
man nkf参照。

Unix 側(MacOSX, Linux)で nkf を用いて、テキスト・ファイルの漢字コードを
変換してみする。

nkf は与えられたテキスト・ファイル(または標準入力)の漢字コードを自動的
に判定し、漢字コードの変換を行い、標準出力へ出力する。次の例は、
file.txt の漢字コードを UTF-8 に変換して別のファイル
file-utf8.txt に保存している。

```
$ nkf -w file.txt > file-utf8.txt
```

よく使うオプション

```
 -j
 出力を JIS に (標準)

 -e
 出力を EUC-JP に

 -s
 出力を Shift_JIS に

 -w
 出力を UTF-8 に

 --guess
 文字コードの推定を行い、（変換後のデータではなく）推定結果を表示する。
```

次の例は、テキストファイルfile.txtの漢字コードを UTF-8 に変換し
ようとしているが、この方法は
うまくいかない( 重要なファイルで試してみて
はいけない)。

```
$ nkf -w file.txt > file.txt
```

その理由は、標準出力の切り替え> を使った瞬間にファイルの内
容が消されるからである。漢字コードを変換したい時には、次のように一度、
別の一時ファイル(temporary file)に保存する。

```
$ ls -l file.txt 
(モードの確認)
$ ls tmpfile 
ls: tmpfile: No such file or directory
$ nkf -w file.txt > tmpfile 
$ mv tmpfile file.txt 
$ chmod モード file.txt 
```

ファイルのモードは保存されないので、必要なら ls -l で調べて、後でchmod で戻しする。

#### Windows でのテキスト・ファイルの作成

Windows で、次のような方法でテキスト・ファイルを作成しする。

- 「メモ帳」、または、「ワードパット」を使う
- 「コマンドプロンプト」で echo コマンドとリダイレクトで作る
```
H:\> echo hello >  file.txt
H:\> echo hi    >> file.txt
```
- 「コマンドプロンプト」で、copy コマンドを使って作る。コピー元としてconを指定すると、キーボードになる。
```
H:\> copy con file.txt
漢字
^Z
	１個のファイルをコピーしました。
H:\> 
```

`^Z`は、Control+Z。Unix の`^D`相当。キーボードからファイルの終わりを示す。
- その他

#### Windows+Unix: テキスト・ファイルの漢字コードの確認

Windows でテキスト・ファイルを作成すると、どのような文字コードが使われるか確認しする。

- Windows 側で作成したテキスト・ファイルを Unix 側の Emacs で開き、漢字コードを確認する。
- nkf コマンドを使う。
```
$ nkf --guess file.txt 
```
ただし、これらのプログラムを用いても、正しく表示されないこともある。

#### Windows+Unix: テキスト・ファイルの漢字コードの調整

- Windows 側で H: ドライブの下に漢字を含むテキストファイルを作成する。
- Windows で、PuTTY 、または、Tera Term を実行してUnix に遠隔ログインをしする。遠隔ログインした端末の中で、1.のファイルを、cat コマンドで画面に表示する。
- 文字化けしたら、nkf コマンド、lv コマンドを使って文字コードを変換して表示しする。

#### Linux: ログイン、ログアウト、再起動、シャットダウン

ターゲットiMac Linux で、次の操作を行ったり、行うことが可能なことを確認
しする。

- ログインする。
  - ログインの画面で、ユーザ名を打つ。
  - 続くウインドウでパスワードを打つ。
- ログアウトする。
  - 「システム」メニューから「ログアウト」を選択して、ログアウトする。
- シャットダウン、あるいは、再起動する。
  - ログインしている状態で、「システム」メニューから「シャットダウン」や「再起動」を選択する。
  - ログイン前にユーザ名やパスワードをを打つ状態で、画面の右下にある「電源ボタン」の形のボタンを押し、「再起動」や「シャットダウン」を選択する。

#### Linux: アプリケーションの実行

ターゲットLinux にログインすると、一番上に「アプリケーション」を含むメ
ニュー・バーが現れる。それを利用して、次のようなアプリケーションを実行
しする。

- 文字端末
  - 「アプリケーション」 メニューの「システムツール」項目で「GNOME端末」を選ぶ。
- Firefox
  - 文字端末の中で「firefox」というコマンドを実行する。
  - 一番上のメニューバーで、「Firefo ウェブ・ブラウザ」 のアイコンをクリックする。
- Emacs
  - 文字端末の中で「emacs (またはemacs -nw)」というコマンドを実行する。
  - 「アプリケーション」 メニューの「アクセサリ」項目で「Emacs テキスト・エディター」を選ぶ。

#### Linux: sshコマンドによる遠隔ログイン

GNOME端末の中で、ssh コマンドを実行し、ターゲット内のコンピュータに遠隔ログインする。

- 遠隔ログインするコンピュータ
- 実行するコマンド

#### Unix: Emacs M-x set-buffer-file-coding-system

Emacs を使って、ファイルの文字コードを変更することができる。このことを確認しする。

#### Unix: lv コマンドによる文字コード変換

lv コマンドは、ページャであるが、nkf の代わりに文字コード変換のプログラムとして利用することもできる。このことを確認しする。

```
$ lv -Oej file.txt > file-euc.txt 
$ lv -Oj  file.txt > file-jis.txt 
$ lv -Os  file.txt > file-shift_jis.txt 
$ lv -Ou8 file.txt > file-utf8.txt 
```

#### Windows PuTTY による iMac への遠隔ログイン

PuTTY は、Windows よく使われる SSH のクライアントである。
Tera Termと同様に
PuTTY を用いて遠隔ログインして利用しする。

- ターゲットWindowsで次の場所にある PuTTY(日本語版) を実行する。
  ```
  C:\Program Files (x86)\putty\puttyjp.exe
  ```
- PuTTYを実行すると、「PuTTY設定」のウインドウが現れる。
  左側の「カテゴリ」から「セッション」を選びする(実行直後には、
  最初からそうなっている。)。
- セッションでは、「ホスト名」に遠隔ログインししたい
  コンピュータの名前を打ち込む。
  たとえば、「www.coins.tsukuba.ac.jp」と
  打ち込む。
- 次に、左側の「カテゴリ」から「ウインドウ」の下の「変換」を選ぶ。
  「文字コードの設定:」で、接続先の文字コードを選ぶ。
  接続先が coins の iMac やサーバならば、「UTF-8」を選ぶ。
- 「セッション」に戻り、「開く」ボタンを押す。
- 最初にあるホストに接続した時には、次のような警告が出る。この時、接続先の公開鍵の fingerprint を確認してから
  「はい」か「いいいえ」を押す。
- login as:  に対してログイン名を打つ。
- Password:  に対してパスワードを打つ。
- ログイン後、コマンドを実行しする。

#### ターゲットPC: 再起動・電源オン直後の起動するOSの選択

ターゲットPC (iMacではない)で OS を選択するメニューを表示し、必要なOSを起動しする。

まず、次のいずれかの操作をする。

- Windows が動作している時には、Windows を再起動する。
- Linux が動作している時には、Linux を再起動する。
- 電源が切れている時には、電源を入れる。

ターゲットPC で、最初に起動した時に、次のような表示が出る。

```
GNU GRUB  version 0.97  (582K lower / 3490744K upper memory)
+-------------------------------------------------------------------+
| CentOS 6.5                                                        |
| Windows 8.1                                                       |
|                                                                   |
|                                                                   |
|                                                                   |
+-------------------------------------------------------------------+
    Use the ↑ and ↓ keys to select which entry is highlighted.
    Press enter to boot the selected OS, 'e' to edit the 
    commands before booting, 'a' to modify the kernel arguments
    before booting, or 'c' for a command-line.

The highlighted entry will be booted automatically in 9 seconds.
The highlighted entry will be booted automatically in 8 seconds.
The highlighted entry will be booted automatically in 7 seconds.
...
```

この表示が出ている間に、何かキー（↓など）を押す。
必要なOSを矢印キー「↑」「↓」で選んで、リターンキーを打つ。

#### Linux: GNOME端末、文字コードの変更

ターゲットLinuxでは、標準の文字コードが UTF-8 になっている。
これを別のもの、たとえば、「日本語 EUC」にしてみする。

- 「端末(T)」メニューから「文字コードの設定」を選ぶ。
- 「日本語 (EUC-JP)」を選ぶ。

「日本語 (EUC-JP)」等必要に文字コードがメニューに現れない時には、
「端末(T)」メニューから「文字コードの設定→追加と削除」で追加するとよい。

文字コードを変更したら、次のようにして効果を確かめる。

```
$ echo $LANG 
$ date 
$ locale 
$ LANG=ja_JP.eucJP 
$ locale 
$ date 
$ 
```

変更した文字コードを元に戻しする。

## WindowsとLinux、Emacs モードライン、set-buffer-file-coding-system

#### A
ターゲットWindowsで「コマンドプロンプト」を実行し、その中で次のようなコマンドを実行し、テキスト・ファイルを作成する
```
hostname  >  hostname-ipaddr1.text
ipconfig  >> hostname-ipaddr1.text
dir hostname-ipaddr1.text
(ファイルの大きさの確認)
type hostname-ipaddr1.text
(ファイルの内容の確認)
```

作成したファイルを、Unix 側(MacOSX iTerm、Tera Term、または、PuTTY)で次のように打ち、文字化けしないで表示されることを確認する
```
date
ls  -l hostname-ipaddr1.text
(ファイルの大きさの確認)
nkf -w hostname-ipaddr1.text
(ファイルの内容の確認)
```
最後の Unix 側の画面の表示の様子を、シェルのプロンプトも含めて提出しな
さい。nkf の代わりに lv コマンドをつかってもよい。端末の文字コードによっ
ては、nkf コマンドに与えるオプションを変更しする。たとえば、
UTF-8 の場合には、nkf -w としする。

#### B
ターゲットLinux で「GNOME端末」を実行しする。そこで次のようなコマンドを実行する。
```
hostname     >  hostname-ipaddr2.text
ifconfig -a  >> hostname-ipaddr2.text
date         >> hostname-ipaddr2.text
ls -l hostname-ipaddr2.text
(ファイルの大きさの確認)
cat hostname-ipaddr2.text
(ファイルの内容の確認)
```
このテキスト・ファイルを、レポートに含めする。Emacs insert-fileを使って、ファイルを挿入すると良い。
#### C
文書の作成と編集

- リボン
- ヘルプ
- 文字列の移動方法

#### D
次のことを行いう。

- Unix 側で、普通の方法で漢字とASCII文字含む3-5行のテキスト・ファイルを作成する。
- 作成したファイルの漢字コードと行末のコードを調べる。
- そのファイルの漢字コードを Shift-JIS に、行末コードを
  Windows のもの(CR+LN, 16 進数で 0d 0a、^M ^J、\r\n)に変換し、別の名前で保存する。
- 変更後のファイルを、Windows 側でメモ帳、または、ワードパットで開き、
  きちんと表示されることを確認する。

どのような方法で漢字コードを確認したか、どのような方法で
漢字コードと行末コードを変換したかを含めする。また、変換前と変換後の
ファイルについて、ls -l, nkf --guess, od -xc, hexdump -c コマンドの結果
を示し、きちんと変換されていることを示しす。

#### E
次のことを全て行う。

- ターゲットWindows 8.1 で Thunderbird を設定し、coins のメールの読み書きをできるようにする。
- ターゲットLinux で Thunderbird を設定し、coins のメールの読み書きをできるようにする。
- ターゲットPC (dahlia01 - dahlia30) で、Windows を動かす。
- ターゲットPC (dahlia01 - dahlia30) で、Linux を動かす。
- 設定した Thunderbird (Windows, Linuxの両方) で、自分宛にメールを送る。

レポートには、最後のメールのヘッダを含めることで、
これらのことを全て行ったことが分かるようにしする。次のヘッダの内容を含め、説明するとよい。

- User-Agent:
- Received: 
