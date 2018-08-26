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
   flexible-arrays
   librs
   genalloc
   errseq
   printk-formats
   circular-buffers
   mm-api
   gfp_mask-from-fs-io
   timekeeping
   boot-time-mm

カーネルデバッグのインターフェイス
===================================

.. toctree::
   :maxdepth: 1

   debug-objects
   tracepoint

.. only::  subproject

   Indices
   =======

   * :ref:`genindex`
