==========
投機制御
==========

多岐にわたる CPU に投機的実行に関する仕様上の欠陥が存在しており、脆弱性として特権領域を無視して様々な形でデータが漏洩する可能性があります。

カーネルは様々な方式でそのような脆弱性を緩和するコードを提供しています。緩和策はコンパイル時に設定することができたり、カーネルコマンドラインで指定することができます。

緩和策の中には非常に大きな代償を伴うものもありますが、特定のプロセスやタスクを制御された環境に制限することができます。これらの緩和策は `prctl(2) <https://man.kusakata.com/man/prctl.2.html>`_ で制御できます。

関連する prctl オプションは2つ存在します:

 * PR_GET_SPECULATION_CTRL

 * PR_SET_SPECULATION_CTRL

PR_GET_SPECULATION_CTRL
-----------------------

PR_GET_SPECULATION_CTRL は prctl(2) の arg2 で選択された投機実行の欠陥の状態を返します。返り値は 0-3 のビットで、以下の意味を持ちます:

====== ====================== ==================================================================================
ビット  定義                    説明
====== ====================== ====================================================================================================================================================================
0      PR_SPEC_PRCTL          緩和策は PR_SET_SPECULATION_CTRL によってタスク毎に制御可能。
1      PR_SPEC_ENABLE         投機実行は有効になっており、緩和策は無効になっている。
2      PR_SPEC_DISABLE        投機実行が無効になっており、緩和策が有効になっている。
3      PR_SPEC_FORCE_DISABLE  PR_SPEC_DISABLE と同じだが、解除が不可能。prctl(..., PR_SPEC_ENABLE) は失敗する。
4      PR_SPEC_DISABLE_NOEXEC PR_SPEC_DISABLE と同じだが、`execve(2) <https://man.kusakata.com/man/execve.2.html>`_ によって状態が消去される。
====== ====================== ====================================================================================================================================================================

全てのビットが 0 の場合、CPU は投機実行の欠陥の影響を受けません。

PR_SPEC_PRCTL が設定されている場合、タスク毎の緩和策の制御が可能です。設定されていない場合、投機実行の欠陥に対して prctl(PR_SET_SPECULATION_CTRL) を実行できません。

PR_SET_SPECULATION_CTRL
-----------------------

PR_SET_SPECULATION_CTRL allows to control the speculation misfeature, which
is selected by arg2 of `prctl(2) <https://man.kusakata.com/man/prctl.2.html>`_ per task. arg3 is used to hand
in the control value, i.e. either PR_SPEC_ENABLE or PR_SPEC_DISABLE or
PR_SPEC_FORCE_DISABLE.

共通のエラーコード
-------------------
======= =================================================================
値      意味
======= =================================================================
EINVAL  The prctl is not implemented by the architecture or unused
        prctl(2) arguments are not 0.

ENODEV  arg2 is selecting a not supported speculation misfeature.
======= =================================================================

PR_SET_SPECULATION_CTRL のエラーコード
---------------------------------------
======= =================================================================
値      意味
======= =================================================================
0       Success

ERANGE  arg3 is incorrect, i.e. it's neither PR_SPEC_ENABLE nor
        PR_SPEC_DISABLE nor PR_SPEC_FORCE_DISABLE.

ENXIO   Control of the selected speculation misfeature is not possible.
        See PR_GET_SPECULATION_CTRL.

EPERM   Speculation was disabled with PR_SPEC_FORCE_DISABLE and caller
        tried to enable it again.
======= =================================================================

投機欠陥の制御
----------------
- PR_SPEC_STORE_BYPASS: Speculative Store Bypass

  Invocations:
   * prctl(PR_GET_SPECULATION_CTRL, PR_SPEC_STORE_BYPASS, 0, 0, 0);
   * prctl(PR_SET_SPECULATION_CTRL, PR_SPEC_STORE_BYPASS, PR_SPEC_ENABLE, 0, 0);
   * prctl(PR_SET_SPECULATION_CTRL, PR_SPEC_STORE_BYPASS, PR_SPEC_DISABLE, 0, 0);
   * prctl(PR_SET_SPECULATION_CTRL, PR_SPEC_STORE_BYPASS, PR_SPEC_FORCE_DISABLE, 0, 0);
   * prctl(PR_SET_SPECULATION_CTRL, PR_SPEC_STORE_BYPASS, PR_SPEC_DISABLE_NOEXEC, 0, 0);

- PR_SPEC_INDIR_BRANCH: Indirect Branch Speculation in User Processes
                        (Mitigate Spectre V2 style attacks against user processes)

  Invocations:
   * prctl(PR_GET_SPECULATION_CTRL, PR_SPEC_INDIRECT_BRANCH, 0, 0, 0);
   * prctl(PR_SET_SPECULATION_CTRL, PR_SPEC_INDIRECT_BRANCH, PR_SPEC_ENABLE, 0, 0);
   * prctl(PR_SET_SPECULATION_CTRL, PR_SPEC_INDIRECT_BRANCH, PR_SPEC_DISABLE, 0, 0);
   * prctl(PR_SET_SPECULATION_CTRL, PR_SPEC_INDIRECT_BRANCH, PR_SPEC_FORCE_DISABLE, 0, 0);
