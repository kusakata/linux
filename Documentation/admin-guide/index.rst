Linux カーネルユーザー・管理者ガイド
=================================================

以下は年月と共にカーネルに追加されてきたユーザー向けドキュメント集です。ただし、順序・系統づけられているとは言い難いものがあります — ひとつの首尾一貫したドキュメントとしては書かれていないためです。時間と共に急速に改善されていくことでしょう。

最初のセクションでは全体的な情報が記載されています。カーネル全体を説明している README やカーネルパラメータのドキュメントなどが含まれます。

.. toctree::
   :maxdepth: 1

   README
   kernel-parameters
   devices

以下のセクションでは CPU の脆弱性と、コンパイル時・起動時・実行時に設定できる緩和策について説明しています。

.. toctree::
   :maxdepth: 1

   l1tf

以下は特定の問題やバグを追跡しようとしているユーザーのためのドキュメントです。

.. toctree::
   :maxdepth: 1

   reporting-bugs
   security-bugs
   bug-hunting
   bug-bisect
   tainted-kernels
   ramoops
   dynamic-debug-howto
   init

アプリケーション開発者の興味を引くような情報がセクションの冒頭にあります。カーネル ABI の様々な面をカバーするドキュメントはこちらです。

.. toctree::
   :maxdepth: 1

   sysfs-rules

後はカーネルの特定の挙動を好みに合わせるために設定する方法を説明した様々な順不同のガイドになります。

.. toctree::
   :maxdepth: 1

   initrd
   cgroup-v2
   serial-console
   braille-console
   parport
   md
   module-signing
   sysrq
   unicode
   vga-softcursor
   binfmt-misc
   mono
   java
   ras
   bcache
   pm/index
   thunderbolt
   LSM/index
   mm/index

.. only::  subproject and html

   Indices
   =======

   * :ref:`genindex`
