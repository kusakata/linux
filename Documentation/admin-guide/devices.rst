.. _admin_devices:

Linux 予約デバイス (4.x+ バージョン)
======================================

以下は Linux デバイスリストです。予約デバイス番号の公式レジストリであり Linux オペレーティングシステムの ``/dev`` ディレクトリノードです。

lanana.org に存在していたこのドキュメントの LaTeX 版はメンテナンスされていません。メインライン Linux カーネルのバージョンがマスタードキュメントです。アップデートはパッチとしてカーネルメンテナに送ってください (:ref:`Documentation/process/submitting-patches.rst <submittingpatches>` ドキュメントを参照)。文字・ブロックデバイスに関係しているメンテナが誰なのかは MAINTAINERS ファイルの "CHAR and MISC DRIVERS" と "BLOCK LAYER" セクションを見てください。

このドキュメントは Filesystem Hierarchy Standard (FHS) に組み込まれています。FHS は http://www.pathname.com/fhs/ で確認できます。

(68k/Amiga) と書かれているデバイスは Amiga プラットフォームの Linux/68k にのみ適用されます。(68k/Atari) と書かれているデバイスは Atari プラットフォームの Linux/68k にのみ適用されます。

このドキュメントはパブリックドメインです。しかしながら、著者に連絡を取ることができる以上、著者の許可なく変更を加えたバージョンを配布しないように要求します。


.. attention::

  デバイスドライバーの作者は以下を読んでください。

  Linux はデバイスの動的な番号割当をサポートしており、``sysfs`` と ``udev`` (``systemd``) を使用して命名を処理できます。ただしシリアル・ブートデバイスの領域ではいくつか例外が存在します。デバイス番号を要求する前に本当に必要であることを確認してください。

  メジャーナンバーあるいは場合によってマイナーナンバーを割り当てて欲しい場合 (例: バスマウス)、パッチを投稿して作者に上記のように送信してください。

  デバイスの説明は *以下のリストと同じ形式* にしてください。デバイスを公開して衝突を防ぐために必要な情報をすべて確保するためです。

  また、ときとして、「名前空間警察」として振る舞うこともあります。気を悪くしないでください。衝突が発生するような ``/dev`` の名前がしばしば投稿されているのです。変更によって前方互換性に問題が起こるような事態は避けるように努めています。したがって、デバイス名と番号を決定する前に、最低でも変更が難しくなるようなことになる **前** には相談するようにしてください。

  ご協力感謝します。

.. include:: devices.txt
   :literal:

追加 ``/dev/`` ディレクトリエントリ
--------------------------------------

This section details additional entries that should or may exist in
the /dev directory.  It is preferred that symbolic links use the same
form (absolute or relative) as is indicated here.  Links are
classified as "hard" or "symbolic" depending on the preferred type of
link; if possible, the indicated type of link should be used.

必須リンク
++++++++++++++++

以下のリンクは全ての環境に存在する必要があります:

=============== =============== =============== ===============================
/dev/fd		/proc/self/fd	symbolic	ファイル記述子
/dev/stdin	fd/0		symbolic	stdin ファイル記述子
/dev/stdout	fd/1		symbolic	stdout ファイル記述子
/dev/stderr	fd/2		symbolic	stderr ファイル記述子
/dev/nfsd	socksys		symbolic	Required by iBCS-2
/dev/X0R	null		symbolic	Required by iBCS-2
=============== =============== =============== ===============================

ノート: ``/dev/X0R`` は <letter X>-<digit 0>-<letter R> です。

推奨リンク
+++++++++++++++++

以下のリンクは全ての環境に存在することが推奨されています:


=============== =============== =============== ===============================
/dev/core	/proc/kcore	symbolic	後方互換
/dev/ramdisk	ram0		symbolic	後方互換
/dev/ftape	qft0		symbolic	後方互換
/dev/bttv0	video0		symbolic	後方互換
/dev/radio	radio0		symbolic	後方互換
/dev/i2o*	/dev/i2o/*	symbolic	後方互換
/dev/scd?	sr?		hard		Alternate SCSI CD-ROM name
=============== =============== =============== ===============================

ローカルで定義されるリンク
+++++++++++++++++++++++++++++

The following links may be established locally to conform to the
configuration of the system.  This is merely a tabulation of existing
practice, and does not constitute a recommendation.  However, if they
exist, they should have the following uses.

=============== =============== =============== ===============================
/dev/mouse	mouse port	symbolic	Current mouse device
/dev/tape	tape device	symbolic	Current tape device
/dev/cdrom	CD-ROM device	symbolic	Current CD-ROM device
/dev/cdwriter	CD-writer	symbolic	Current CD-writer device
/dev/scanner	scanner		symbolic	Current scanner device
/dev/modem	modem port	symbolic	Current dialout device
/dev/root	root device	symbolic	Current root filesystem
/dev/swap	swap device	symbolic	Current swap device
=============== =============== =============== ===============================

``/dev/modem`` should not be used for a modem which supports dialin as
well as dialout, as it tends to cause lock file problems.  If it
exists, ``/dev/modem`` should point to the appropriate primary TTY device
(the use of the alternate callout devices is deprecated).

For SCSI devices, ``/dev/tape`` and ``/dev/cdrom`` should point to the
*cooked* devices (``/dev/st*`` and ``/dev/sr*``, respectively), whereas
``/dev/cdwriter`` and /dev/scanner should point to the appropriate generic
SCSI devices (/dev/sg*).

``/dev/mouse`` may point to a primary serial TTY device, a hardware mouse
device, or a socket for a mouse driver program (e.g. ``/dev/gpmdata``).

ソケットとパイプ
+++++++++++++++++++

Non-transient sockets and named pipes may exist in /dev.  Common entries are:

=============== =============== ===============================================
/dev/printer	socket		lpd local socket
/dev/log	socket		syslog local socket
/dev/gpmdata	socket		gpm mouse multiplexer
=============== =============== ===============================================

マウントポイント
++++++++++++++++++

The following names are reserved for mounting special filesystems
under /dev.  These special filesystems provide kernel interfaces that
cannot be provided with standard device nodes.

=============== =============== ===============================================
/dev/pts	devpts		PTY slave filesystem
/dev/shm	tmpfs		POSIX shared memory maintenance access
=============== =============== ===============================================

ターミナルデバイス
--------------------

Terminal, or TTY devices are a special class of character devices.  A
terminal device is any device that could act as a controlling terminal
for a session; this includes virtual consoles, serial ports, and
pseudoterminals (PTYs).

All terminal devices share a common set of capabilities known as line
disciplines; these include the common terminal line discipline as well
as SLIP and PPP modes.

All terminal devices are named similarly; this section explains the
naming and use of the various types of TTYs.  Note that the naming
conventions include several historical warts; some of these are
Linux-specific, some were inherited from other systems, and some
reflect Linux outgrowing a borrowed convention.

A hash mark (``#``) in a device name is used here to indicate a decimal
number without leading zeroes.

仮想端末とコンソールデバイス
+++++++++++++++++++++++++++++++++++++++

Virtual consoles are full-screen terminal displays on the system video
monitor.  Virtual consoles are named ``/dev/tty#``, with numbering
starting at ``/dev/tty1``; ``/dev/tty0`` is the current virtual console.
``/dev/tty0`` is the device that should be used to access the system video
card on those architectures for which the frame buffer devices
(``/dev/fb*``) are not applicable. Do not use ``/dev/console``
for this purpose.

The console device, ``/dev/console``, is the device to which system
messages should be sent, and on which logins should be permitted in
single-user mode.  Starting with Linux 2.1.71, ``/dev/console`` is managed
by the kernel; for previous versions it should be a symbolic link to
either ``/dev/tty0``, a specific virtual console such as ``/dev/tty1``, or to
a serial port primary (``tty*``, not ``cu*``) device, depending on the
configuration of the system.

シリアルポート
++++++++++++++++

Serial ports are RS-232 serial ports and any device which simulates
one, either in hardware (such as internal modems) or in software (such
as the ISDN driver.)  Under Linux, each serial ports has two device
names, the primary or callin device and the alternate or callout one.
Each kind of device is indicated by a different letter.	 For any
letter X, the names of the devices are ``/dev/ttyX#`` and ``/dev/cux#``,
respectively; for historical reasons, ``/dev/ttyS#`` and ``/dev/ttyC#``
correspond to ``/dev/cua#`` and ``/dev/cub#``. In the future, it should be
expected that multiple letters will be used; all letters will be upper
case for the "tty" device (e.g. ``/dev/ttyDP#``) and lower case for the
"cu" device (e.g. ``/dev/cudp#``).

The names ``/dev/ttyQ#`` and ``/dev/cuq#`` are reserved for local use.

The alternate devices provide for kernel-based exclusion and somewhat
different defaults than the primary devices.  Their main purpose is to
allow the use of serial ports with programs with no inherent or broken
support for serial ports.  Their use is deprecated, and they may be
removed from a future version of Linux.

Arbitration of serial ports is provided by the use of lock files with
the names ``/var/lock/LCK..ttyX#``. The contents of the lock file should
be the PID of the locking process as an ASCII number.

It is common practice to install links such as /dev/modem
which point to serial ports.  In order to ensure proper locking in the
presence of these links, it is recommended that software chase
symlinks and lock all possible names; additionally, it is recommended
that a lock file be installed with the corresponding alternate
device.	 In order to avoid deadlocks, it is recommended that the locks
are acquired in the following order, and released in the reverse:

	1. The symbolic link name, if any (``/var/lock/LCK..modem``)
	2. The "tty" name (``/var/lock/LCK..ttyS2``)
	3. The alternate device name (``/var/lock/LCK..cua2``)

In the case of nested symbolic links, the lock files should be
installed in the order the symlinks are resolved.

Under no circumstances should an application hold a lock while waiting
for another to be released.  In addition, applications which attempt
to create lock files for the corresponding alternate device names
should take into account the possibility of being used on a non-serial
port TTY, for which no alternate device would exist.

疑似端末 (PTY)
++++++++++++++++++++++

Pseudoterminals, or PTYs, are used to create login sessions or provide
other capabilities requiring a TTY line discipline (including SLIP or
PPP capability) to arbitrary data-generation processes.	 Each PTY has
a master side, named ``/dev/pty[p-za-e][0-9a-f]``, and a slave side, named
``/dev/tty[p-za-e][0-9a-f]``.  The kernel arbitrates the use of PTYs by
allowing each master side to be opened only once.

Once the master side has been opened, the corresponding slave device
can be used in the same manner as any TTY device.  The master and
slave devices are connected by the kernel, generating the equivalent
of a bidirectional pipe with TTY capabilities.

Recent versions of the Linux kernels and GNU libc contain support for
the System V/Unix98 naming scheme for PTYs, which assigns a common
device, ``/dev/ptmx``, to all the masters (opening it will automatically
give you a previously unassigned PTY) and a subdirectory, ``/dev/pts``,
for the slaves; the slaves are named with decimal integers (``/dev/pts/#``
in our notation).  This removes the problem of exhausting the
namespace and enables the kernel to automatically create the device
nodes for the slaves on demand using the "devpts" filesystem.
