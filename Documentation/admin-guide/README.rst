Linux カーネルリリース 4.x <http://kernel.org/>
=================================================

以下は Linux バージョン 4 のリリースノートです。Linux は何なのかということから、カーネルのインストール方法、何か問題が起こった時の対処方法まで書かれているので、注意して読んでください。

Linux とは？
--------------

  Linux は Unix オペレーティングシステムのクローンであり、ネット上で緩く結びついているハッカーたちの助けを借りながら、Linus Torvalds によってスクラッチから書かれました。POSIX と Single UNIX Specification 規格に準拠しています。

  Linux には近代的な Unix が備えて然るべき機能が全て揃っています。真のマルチタスク、仮想メモリ、共有ライブラリ、動的ロード、共有のコピーオンライトな実行ファイル、適切なメモリ管理、IPv4 や IPv6 を含むマルチスタックネットワーク。

  Linux は GNU General Public License v2 の下で配布されています。詳しくは付属の COPYING ファイルを参照してください。

Linux が動作するハードウェアは？
---------------------------------

  Linux は当初32ビットの x86 ベース PC (386 以上) 向けに開発されていましたが、今日の Linux は Compaq Alpha AXP, Sun SPARC, UltraSPARC, Motorola 68000, PowerPC, PowerPC64, ARM, Hitachi SuperH, Cell, IBM S/390, MIPS, HP PA-RISC, Intel IA-64, DEC VAX, AMD x86-64 Xtensa, ARC アーキテクチャなどでも動作します。

  ページメモリ管理ユニット (PMMU) を搭載していて (GNU Compiler Collection, GCC に含まれている) GNU C コンパイラ (gcc) の移植が存在すれば、簡単に Linux を32ビット・64ビットのアーキテクチャに移植することができます。Linux は PMMU を搭載していないアーキテクチャにも数多く移植されていますが、機能はかなり制限されます。Linux は Linux 自身にも移植されています。カーネルをユーザー空間アプリケーションとして動作させることが可能であり、これは UserMode Linux (UML) と呼ばれます。

ドキュメント
-------------

 - Linux や UNIX に関するドキュメントはインターネット上に電子媒体として、あるいは書籍として大量に存在します。Linux FTP サイトのドキュメントサブディレクトリの LDP (Linux Documentation Project) 文書を閲覧することを推奨します。この README はシステムのドキュメントではありません: 他にもっとよい情報源がいくらでもあります。

 - Documentation/ サブディレクトリには様々な README ファイルが存在します: 基本的にはカーネルのインストールノート、例えばドライバーについての情報が含まれています。Documentation/00-INDEX は各ファイルに何の情報が含まれているか書かれているリストです。カーネルをアップグレードするときに発生する可能性がある問題についての情報は :ref:`Documentation/process/changes.rst <changes>` ファイルを参照してください。

カーネルソースのインストール
-----------------------------

 - 完全なソースをインストールする場合、カーネルの tarball を適当なパーミッションがあるディレクトリ (例: ホームディレクトリ) に配置して解凍してください::

     xz -cd linux-4.X.tar.xz | tar xvf -

   "X" は最新のカーネルのバージョンに置き換えてください。

   /usr/src/linux を使ってはいけません。ここにはライブラリのヘッダーファイルが使用するカーネルヘッダーが含まれています。ライブラリと一致している必要があるため、最新カーネル (kernel-du-jour) を置いてしまうと問題が発生します。

 - 4.x リリースからはパッチをあてることでアップグレードすることもできます。パッチは xz 形式で配布されています。パッチを使ってインストールするには、新しいパッチを全て取得して、カーネルソース (linux-4.X) の最上位ディレクトリに配置して、以下のコマンドを実行::

     xz -cd ../patch-4.x.xz | patch -p1

   "x" は現在のソースツリーのバージョン "X" 以上の全てのバージョンに置き換えてください (バージョンの順番通りに)。バックアップファイルは削除して (some-file-name~ や some-file-name.orig)、パッチの適用が失敗していないか確認すると良いでしょう (some-file-name# や some-file-name.rej)。適用が失敗したパッチが存在する場合、何かが間違っています。

   4.x カーネルのパッチとは異なり、4.x.y カーネル (別名 -stable カーネル) のパッチは積み上げ方式ではなく直接ベースの 4.x カーネルに適用します。例えば、ベースのカーネルが 4.0 で 4.0.3 のパッチを適用したい場合、あらかじめ 4.0.1 や 4.0.2 のパッチを適用する必要はありません。同じように、カーネルバージョン 4.0.2 を使用していて 4.0.3 にバージョンアップしたい場合、4.0.3 のパッチを適用する前に必ず 4.0.2 のパッチを逆適用してください (patch -R)。パッチの適用について詳しくは :ref:`Documentation/process/applying-patches.rst <applying_patches>` を見てください。

   また、patch-kernel スクリプトを使うことで上記の作業は自動化できます。現在のカーネルバージョンを認識してパッチが適用されます::

     linux/scripts/patch-kernel linux

   上記のコマンドの最初の引数はカーネルソースのディレクトリです。パッチはカレントディレクトリから適用されますが、二番目の引数で別のディレクトリを指定することもできます。

 - 古い .o ファイルや放置された依存関係が存在しないことを確認::

     cd linux
     make mrproper

   これでソースが正しくインストールされたはずです。

ソフトウェア要件
---------------------

   4.x カーネルをコンパイル・実行するには様々なソフトウェアパッケージの最新バージョンが必要です。最低限必要なバージョン番号とパッケージの更新の取得方法については :ref:`Documentation/process/changes.rst <changes>` を見てください。古いバージョンのパッケージを使用すると追跡するのが困難な分かりにくいエラーが発生する可能性があります。ビルドや操作時に問題が発生したときは単なるパッケージの更新だと思い込まないでください。

カーネルのビルドディレクトリ
------------------------------

   カーネルのコンパイル時、デフォルトでは全ての出力ファイルはカーネルソースコードと同じ場所に保存されます。``make O=output/dir`` オプションを使うことで (.config を含む) 出力ファイルのディレクトリを指定することができます。例::

     kernel source code: /usr/src/linux-4.X
     build directory:    /home/name/build/kernel

   カーネルを設定・ビルドするには::

     cd /usr/src/linux-4.X
     make O=/home/name/build/kernel menuconfig
     make O=/home/name/build/kernel
     sudo make O=/home/name/build/kernel modules_install install

   ``O=output/dir`` オプションを使用するときは、全ての make コマンドで同じく使うようにしてください。

カーネルの設定
----------------------

   マイナーバージョンのアップグレードでもこの手順を飛ばしてはいけません。リリース毎に新しい設定オプションが追加されており、設定ファイルを正しく設定しないと、おかしな問題が発生する可能性があります。出来る限り手間をかけないで既存の設定を新しいバージョンに持ち越したい場合、``make oldconfig`` を使ってください。新しい設定のみ、どうするか選択するように要求します。

 - 他の設定コマンド::

     "make config"      Plain text interface.

     "make menuconfig"  Text based color menus, radiolists & dialogs.

     "make nconfig"     Enhanced text based color menus.

     "make xconfig"     Qt based configuration tool.

     "make gconfig"     GTK+ based configuration tool.

     "make oldconfig"   Default all questions based on the contents of
                        your existing ./.config file and asking about
                        new config symbols.

     "make olddefconfig"
                        Like above, but sets new symbols to their default
                        values without prompting.

     "make defconfig"   Create a ./.config file by using the default
                        symbol values from either arch/$ARCH/defconfig
                        or arch/$ARCH/configs/${PLATFORM}_defconfig,
                        depending on the architecture.

     "make ${PLATFORM}_defconfig"
                        Create a ./.config file by using the default
                        symbol values from
                        arch/$ARCH/configs/${PLATFORM}_defconfig.
                        Use "make help" to get a list of all available
                        platforms of your architecture.

     "make allyesconfig"
                        Create a ./.config file by setting symbol
                        values to 'y' as much as possible.

     "make allmodconfig"
                        Create a ./.config file by setting symbol
                        values to 'm' as much as possible.

     "make allnoconfig" Create a ./.config file by setting symbol
                        values to 'n' as much as possible.

     "make randconfig"  Create a ./.config file by setting symbol
                        values to random values.

     "make localmodconfig" Create a config based on current config and
                           loaded modules (lsmod). Disables any module
                           option that is not needed for the loaded modules.

                           To create a localmodconfig for another machine,
                           store the lsmod of that machine into a file
                           and pass it in as a LSMOD parameter.

                   target$ lsmod > /tmp/mylsmod
                   target$ scp /tmp/mylsmod host:/tmp

                   host$ make LSMOD=/tmp/mylsmod localmodconfig

                           The above also works when cross compiling.

     "make localyesconfig" Similar to localmodconfig, except it will convert
                           all module options to built in (=y) options.

     "make kvmconfig"   Enable additional options for kvm guest kernel support.

     "make xenconfig"   Enable additional options for xen dom0 guest kernel
                        support.

     "make tinyconfig"  Configure the tiniest possible kernel.

   Linux カーネルのコンフィグツールについては Documentation/kbuild/kconfig.txt に詳しい情報が載っています。

 - ``make config`` のノート:

    - 不必要なドライバーを有効にするとカーネルが大きくなり、場合によっては問題が発生することがあります: 存在しないコントローラカードを探査することにより他のコントローラが混乱する場合があります。

    - 浮動小数点エミュレーションを有効にしてカーネルをコンパイルした場合でもコプロセッサが存在するときはコプロセッサが使われます: その場合は浮動小数点エミュレーションは使用されません。有効にするとカーネルは多少大きくなりますが、数値演算コプロセッサが存在していないマシンでもカーネルが動作するようになります。

    - "kernel hacking" 設定は大抵の場合はカーネルが大きくなったり遅くなったりします (あるいはその両方)。また、カーネルの問題を見つけるために頻繁に不良コードを破壊しようとするルーチンを設定するとカーネルは不安定になります (kmalloc())。通常は "development", "experimental", "debugging" 機能の質問に対しては 'n' と答えるべきでしょう。

カーネルのコンパイル
----------------------

 - 最低でも gcc 3.2 がインストールされていることを確認してください。詳しくは :ref:`Documentation/process/changes.rst <changes>` を参照。

   このカーネルでも a.out ユーザープログラムは動作させることができるので注意してください。

 - ``make`` を実行して圧縮済みのカーネルイメージを作成します。また、lilo をカーネルの makefile に合わせてインストールしている場合は ``make install`` を実行することもできますが、先に lilo の設定をチェックしたほうが良いでしょう。

   install を実行するときは root である必要がありますが、通常のビルドでは root は不要です。あなたの神、主の名 root をみだりに唱えてはならない。

 - カーネルの一部を ``modules`` として設定した場合、``make modules_install`` も実行する必要があります。

 - カーネルのコンパイル・ビルドの出力を詳細にする:

   通常、カーネルのビルドシステムは非常に出力が少ないモードで実行されます (ただし全く出力がされないわけではありません)。コンパイルやリンクなどが上手くいっているか確認する必要がある場合、"verbose" ビルドモードを使ってください。``make`` コマンドに ``V=1`` を指定することで使用できます。例::

     make V=1 all

   ビルドシステムにターゲットをリビルドする理由を出力して欲しいときは ``V=2`` を使ってください。デフォルトは ``V=0`` です。

 - 何か問題が発生したときに備えてカーネルのバックアップを作成する。特に開発リリース版の場合はデバッグされていない新しいコードが含まれているためバックアップは必須です。カーネルに対応するモジュールのバックアップも備えておいてください。動作しているカーネルと同じバージョン番号の新しいカーネルをインストールするときは、``make modules_install`` を実行する前にモジュールのバックアップを作成してください。

   また、コンパイルする前にカーネルコンフィグオプション "LOCALVERSION" を使うことで通常のカーネルバージョンの後ろに固有のサフィックスを追加できます。LOCALVERSION は "General Setup" メニューで設定できます。

 - 新しいカーネルを起動するには、カーネルイメージ (例: コンパイル後の .../linux/arch/x86/boot/bzImage) を通常の起動可能なカーネルが認識されるディレクトリにコピーする必要があります。

 - LILO などのブートローダーを使わずにフロッピーから直接カーネルを起動することはもはやサポートされていません。

   ハードドライブから Linux を起動する場合、LILO を使用することで /etc/lilo.conf ファイルに指定されているカーネルイメージを使うことができます。カーネルイメージファイルは通常の場合 /vmlinuz, /boot/vmlinuz, /bzImage, /boot/bzImage のいずれかです。新しいカーネルを使うには、古いイメージのコピーを保存して新しいイメージを古いイメージに上書きコピーしてください。そして LILO を再実行してローディングマップを更新してください。実行しなかった場合、新しいカーネルイメージを起動することができません。

   LILO を再インストールすると /sbin/lilo の実行が行われます。新しいカーネルが動作しないときは /etc/lilo.conf を編集して古いカーネルイメージ (/vmlinux.old など) のエントリを指定すると良いでしょう。詳しくは LILO のドキュメントを見てください。

   LILO の再インストール後、設定は全て完了です。システムをシャットダウンして、再起動してみてください。

   カーネルイメージのデフォルトのルートデバイス・ビデオモード・ラムディスク容量を変更する必要がある場合、``rdev`` プログラムを使ってください (または LILO のブートオプションを使ってください)。これらのパラメータを変更するのにカーネルを再コンパイルする必要はありません。

 - 新しいカーネルで再起動してください。

問題が起こったら
-----------------------

 - カーネルのバグらしき問題が発生したら、カーネル内の問題が起きている箇所を担当しているメンテナがいるかどうか MAINTAINERS ファイルをチェックして確認してください。誰も記載されていない場合、私 (torvalds@linux-foundation.org) にメールするか適当なメーリングリストやニュースグループに投稿してください。

 - バグを報告するときは、使用しているカーネルと問題の説明、あなたが使用している設定を伝えるようにしてください (本能に従ってください)。問題が新しい場合、私に教えてください。問題が古い場合、いつ初めて問題に気づいたのか教えてください。

 - バグが以下のようなメッセージで確認できる場合::

     unable to handle kernel paging request at address C0000010
     Oops: 0002
     EIP:   0010:XXXXXXXX
     eax: xxxxxxxx   ebx: xxxxxxxx   ecx: xxxxxxxx   edx: xxxxxxxx
     esi: xxxxxxxx   edi: xxxxxxxx   ebp: xxxxxxxx
     ds: xxxx  es: xxxx  fs: xxxx  gs: xxxx
     Pid: xx, process nr: xx
     xx xx xx xx xx xx xx xx xx xx

   あるいはカーネルのデバッグ情報やシステムログに何らかの情報が得られる場合は、正確に情報を教えてください。あなたにはダンプの意味がよくわからないとしても、問題をデバッグするのに役立つかもしれない情報が含まれています。ダンプの上のテキストも重要です: カーネルがなぜコードをダンプしたのかが書かれています (上の例であれば、カーネルポインタが原因です)。ダンプに関する詳しい情報は Documentation/admin-guide/bug-hunting.rst に存在します。

 - If you compiled the kernel with CONFIG_KALLSYMS you can send the dump
   as is, otherwise you will have to use the ``ksymoops`` program to make
   sense of the dump (but compiling with CONFIG_KALLSYMS is usually preferred).
   This utility can be downloaded from
   https://www.kernel.org/pub/linux/utils/kernel/ksymoops/ .
   Alternatively, you can do the dump lookup by hand:

 - In debugging dumps like the above, it helps enormously if you can
   look up what the EIP value means.  The hex value as such doesn't help
   me or anybody else very much: it will depend on your particular
   kernel setup.  What you should do is take the hex value from the EIP
   line (ignore the ``0010:``), and look it up in the kernel namelist to
   see which kernel function contains the offending address.

   To find out the kernel function name, you'll need to find the system
   binary associated with the kernel that exhibited the symptom.  This is
   the file 'linux/vmlinux'.  To extract the namelist and match it against
   the EIP from the kernel crash, do::

     nm vmlinux | sort | less

   This will give you a list of kernel addresses sorted in ascending
   order, from which it is simple to find the function that contains the
   offending address.  Note that the address given by the kernel
   debugging messages will not necessarily match exactly with the
   function addresses (in fact, that is very unlikely), so you can't
   just 'grep' the list: the list will, however, give you the starting
   point of each kernel function, so by looking for the function that
   has a starting address lower than the one you are searching for but
   is followed by a function with a higher address you will find the one
   you want.  In fact, it may be a good idea to include a bit of
   "context" in your problem report, giving a few lines around the
   interesting one.

   If you for some reason cannot do the above (you have a pre-compiled
   kernel image or similar), telling me as much about your setup as
   possible will help.  Please read the :ref:`admin-guide/reporting-bugs.rst <reportingbugs>`
   document for details.

 - Alternatively, you can use gdb on a running kernel. (read-only; i.e. you
   cannot change values or set break points.) To do this, first compile the
   kernel with -g; edit arch/x86/Makefile appropriately, then do a ``make
   clean``. You'll also need to enable CONFIG_PROC_FS (via ``make config``).

   After you've rebooted with the new kernel, do ``gdb vmlinux /proc/kcore``.
   You can now use all the usual gdb commands. The command to look up the
   point where your system crashed is ``l *0xXXXXXXXX``. (Replace the XXXes
   with the EIP value.)

   gdb'ing a non-running kernel currently fails because ``gdb`` (wrongly)
   disregards the starting offset for which the kernel is compiled.
