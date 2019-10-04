
.. The Linux Kernel documentation master file, created by
   sphinx-quickstart on Fri Feb 12 13:51:46 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

.. _linux_doc:

Arch Linux カーネルドキュメント
================================

こちらはカーネルのドキュメントツリーの最上部です。カーネルドキュメントはカーネル自体と同じように、まだまだ発展途上です。分散しているドキュメントを整理してまとめる作業が進行しています。ドキュメントの改善提案は歓迎されます。ドキュメントの編集に参加したい場合は vger.kernel.org の linux-doc メーリングリストに参加してください。

ライセンスに関するドキュメント
-------------------------------

以下のドキュメントでは Linux カーネルソースコードのライセンス (GPLv2) について説明しています。ソースツリーの個々のファイルのライセンスの宣言方法やライセンス全文へのリンクがあります。

* :ref:`kernel_licensing`

ユーザー向けのドキュメント
---------------------------

以下のマニュアルはカーネルの「ユーザー」向けに書かれています。特定の環境で最適の結果を得たい人が対象です。

.. toctree::
   :maxdepth: 2

   admin-guide/index
   kbuild/index

ファームウェア関連ドキュメント
------------------------------
以下はプラットフォームファームウェアに関するカーネルの情報です。

.. toctree::
   :maxdepth: 2

   firmware-guide/index

アプリケーション開発者向けのドキュメント
------------------------------------------

ユーザースペース API マニュアルにはアプリケーション開発者が知るべきカーネルインターフェイスについて説明しているドキュメントが記載されています。

.. toctree::
   :maxdepth: 2

   userspace-api/index
   ioctl/index


カーネル開発の始め方
----------------------------------

以下のマニュアルにはカーネルの開発に関するあらゆる情報が載っています。カーネルコミュニティは数千人の開発者からなる巨大なコミュニティであり、年間を通じて開発されています。巨大なコミュニティの常、物事がどのように運用されているのか知ることで変更をマージしてもらいやすくなるでしょう。

.. toctree::
   :maxdepth: 2

   process/index
   dev-tools/index
   doc-guide/index
   kernel-hacking/index
   trace/index
   maintainer/index
   fault-injection/index
   livepatch/index

カーネル API ドキュメント
--------------------------

以下のブックでは、カーネル開発者の視点から、カーネルサブシステムがどのように機能しているのか詳細に説明しています。情報のほとんどはカーネルソースから直接引用されており、必要に応じて補足を追加しています (あるいは追加することができた最低限 — 必要な補足が全て揃っているとは限りません)。

.. toctree::
   :maxdepth: 2

   driver-api/index
   core-api/index
   locking/index
   accounting/index
   block/index
   cdrom/index
   ide/index
   fb/index
   fpga/index
   hid/index
   i2c/index
   iio/index
   isdn/index
   infiniband/index
   leds/index
   media/index
   netlabel/index
   networking/index
   pcmcia/index
   power/index
   target/index
   timers/index
   spi/index
   w1/index
   watchdog/index
   virt/index
   input/index
   hwmon/index
   gpu/index
   security/index
   sound/index
   crypto/index
   filesystems/index
   vm/index
   bpf/index
   usb/index
   PCI/index
   misc-devices/index
   mic/index
   scheduler/index

アーキテクチャ個別のドキュメント
-----------------------------------

以下のブックでは特定のアーキテクチャの実装に関するプログラミングの詳細情報を提供しています。

.. toctree::
   :maxdepth: 2

   arm/index
   arm64/index
   ia64/index
   m68k/index
   mips/index
   nios2/nios2
   openrisc/index
   parisc/index
   powerpc/index
   riscv/index
   s390/index
   sh/index
   sparc/index
   x86/index
   xtensa/index

ファイルシステムのドキュメント
-------------------------------------

このセクションでは特定のファイルシステムのドキュメントを記載しています。

.. toctree::
   :maxdepth: 2

   filesystems/ext4/index

日本語訳
------------

この日本語訳は ArchWiki の副読本として日本 Arch Linux ユーザー会のメンテナが非公式に翻訳・編集しています。翻訳文の提案や改善は https://github.com/kusakata/linux で受け付けています。

総索引
==================

* :ref:`genindex`
