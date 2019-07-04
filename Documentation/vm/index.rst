=====================================
Linux メモリ管理ドキュメント
=====================================

こちらは Linux のメモリ管理 (mm) サブシステムのドキュメント集です。メモリの割当についてのみ知りたい場合は、:ref:`memory_allocation` を見てください。

MM 機能のユーザーガイド
===========================

以下のドキュメントは Linux のメモリ管理の様々な機能を制御・設定するためのガイドです。

.. toctree::
   :maxdepth: 1

   swap_numa
   zswap

カーネル開発者 MM ドキュメント
==================================

The below documents describe MM internals with different level of
details ranging from notes and mailing list responses to elaborate
descriptions of data structures and algorithms.

.. toctree::
   :maxdepth: 1

   active_mm
   balance
   cleancache
   frontswap
   highmem
   hmm
   hwpoison
   hugetlbfs_reserv
   ksm
   memory-model
   mmu_notifier
   numa
   overcommit-accounting
   page_migration
   page_frags
   page_owner
   remap_file_pages
   slub
   split_page_table_lock
   transhuge
   unevictable-lru
   z3fold
   zsmalloc
