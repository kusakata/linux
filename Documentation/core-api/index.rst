======================
コア API ドキュメント
======================

このページはコアカーネル API のマニュアルの冒頭です。このマニュアルの文章の改筆 (と執筆) は大歓迎です。

コアユーティリティ
====================

.. toctree::
   :maxdepth: 1

   kernel-api
   assoc_array
   atomic_ops
   cachetlb
   refcount-vs-atomic
   cpu_hotplug
   idr
   local_ops
   workqueue
   genericirq
   xarray
   librs
   genalloc
   errseq
   packing
   printk-formats
   circular-buffers
   generic-radix-tree
   memory-allocation
   mm-api
   gfp_mask-from-fs-io
   timekeeping
   boot-time-mm
   memory-hotplug
   protection-keys
   ../RCU/index
   gcc-plugins


カーネルデバッグのインターフェイス
===================================

.. toctree::
   :maxdepth: 1

   debug-objects
   tracepoint

.. only:: subproject and html

   Indices
   =======

   * :ref:`genindex`
