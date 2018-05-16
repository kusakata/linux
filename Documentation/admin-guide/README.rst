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

 - Verbose kernel compile/build output:

   Normally, the kernel build system runs in a fairly quiet mode (but not
   totally silent).  However, sometimes you or other kernel developers need
   to see compile, link, or other commands exactly as they are executed.
   For this, use "verbose" build mode.  This is done by passing
   ``V=1`` to the ``make`` command, e.g.::

     make V=1 all

   To have the build system also tell the reason for the rebuild of each
   target, use ``V=2``.  The default is ``V=0``.

 - Keep a backup kernel handy in case something goes wrong.  This is
   especially true for the development releases, since each new release
   contains new code which has not been debugged.  Make sure you keep a
   backup of the modules corresponding to that kernel, as well.  If you
   are installing a new kernel with the same version number as your
   working kernel, make a backup of your modules directory before you
   do a ``make modules_install``.

   Alternatively, before compiling, use the kernel config option
   "LOCALVERSION" to append a unique suffix to the regular kernel version.
   LOCALVERSION can be set in the "General Setup" menu.

 - In order to boot your new kernel, you'll need to copy the kernel
   image (e.g. .../linux/arch/x86/boot/bzImage after compilation)
   to the place where your regular bootable kernel is found.

 - Booting a kernel directly from a floppy without the assistance of a
   bootloader such as LILO, is no longer supported.

   If you boot Linux from the hard drive, chances are you use LILO, which
   uses the kernel image as specified in the file /etc/lilo.conf.  The
   kernel image file is usually /vmlinuz, /boot/vmlinuz, /bzImage or
   /boot/bzImage.  To use the new kernel, save a copy of the old image
   and copy the new image over the old one.  Then, you MUST RERUN LILO
   to update the loading map! If you don't, you won't be able to boot
   the new kernel image.

   Reinstalling LILO is usually a matter of running /sbin/lilo.
   You may wish to edit /etc/lilo.conf to specify an entry for your
   old kernel image (say, /vmlinux.old) in case the new one does not
   work.  See the LILO docs for more information.

   After reinstalling LILO, you should be all set.  Shutdown the system,
   reboot, and enjoy!

   If you ever need to change the default root device, video mode,
   ramdisk size, etc.  in the kernel image, use the ``rdev`` program (or
   alternatively the LILO boot options when appropriate).  No need to
   recompile the kernel to change these parameters.

 - Reboot with the new kernel and enjoy.

問題が起こったら
-----------------------

 - If you have problems that seem to be due to kernel bugs, please check
   the file MAINTAINERS to see if there is a particular person associated
   with the part of the kernel that you are having trouble with. If there
   isn't anyone listed there, then the second best thing is to mail
   them to me (torvalds@linux-foundation.org), and possibly to any other
   relevant mailing-list or to the newsgroup.

 - In all bug-reports, *please* tell what kernel you are talking about,
   how to duplicate the problem, and what your setup is (use your common
   sense).  If the problem is new, tell me so, and if the problem is
   old, please try to tell me when you first noticed it.

 - If the bug results in a message like::

     unable to handle kernel paging request at address C0000010
     Oops: 0002
     EIP:   0010:XXXXXXXX
     eax: xxxxxxxx   ebx: xxxxxxxx   ecx: xxxxxxxx   edx: xxxxxxxx
     esi: xxxxxxxx   edi: xxxxxxxx   ebp: xxxxxxxx
     ds: xxxx  es: xxxx  fs: xxxx  gs: xxxx
     Pid: xx, process nr: xx
     xx xx xx xx xx xx xx xx xx xx

   or similar kernel debugging information on your screen or in your
   system log, please duplicate it *exactly*.  The dump may look
   incomprehensible to you, but it does contain information that may
   help debugging the problem.  The text above the dump is also
   important: it tells something about why the kernel dumped code (in
   the above example, it's due to a bad kernel pointer). More information
   on making sense of the dump is in Documentation/admin-guide/bug-hunting.rst

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
