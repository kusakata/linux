.. SPDX-License-Identifier: GPL-2.0

Linux カーネルライセンス規則
==============================

Linux カーネルは GNU General Public License version 2 のみ (GPL-2.0) で配布されています。ライセンスの文言は LICENSES/preferred/GPL-2.0 にあります。ただし COPYING で説明されているように LICENSES/exceptions/Linux-syscall-note の記載があるシステムコールは例外です。

このドキュメントファイルではライセンスを明確にするために各ソースファイルに注釈を付ける方法を説明しています。カーネルのライセンスは置き換わりません。

COPYING ファイルで説明しているライセンスはカーネルソース全体に適用されますが、個別のソースコードでは GPL-2.0 と互換性のある他のライセンスが使われている場合があります::

    GPL-1.0+  :  GNU General Public License v1.0 以上
    GPL-2.0+  :  GNU General Public License v2.0 以上
    LGPL-2.0  :  GNU Library General Public License v2 のみ
    LGPL-2.0+ :  GNU Library General Public License v2 以上
    LGPL-2.1  :  GNU Lesser General Public License v2.1 のみ
    LGPL-2.1+ :  GNU Lesser General Public License v2.1 以上

さらに、個々のファイルはデュアルライセンスで配布することができます。例えば、GPL と互換性のあるライセンスと BSD や MIT などの許容的ライセンスのデュアルライセンスなど。

ユーザースペースプログラムのカーネルインターフェイスを記述する User-space API (UAPI) ヘッダーファイルは特殊です。カーネルの COPYING ファイルにあるように、システムコールインターフェイスには明確な境界があり、システムコールを使用してカーネルと対話するソフトウェアまで GPL の要件が拡大されることはありません。UAPI ヘッダーは Linux カーネルで動作する実行ファイルを作成する全てのソースファイルに含める必要があるため、特別なライセンス表記で例外が設けられています。

ソースファイルのライセンスを宣言するときはファイルの一番上に適当な定型文のコメントを挿入するのが一般的です。書式や typo などのため、こういった「定型文」をライセンス管理のために使用するツールで確認することは容易ではありません。

定型文の代わりになるものとして各ソースファイルで Software Package Data Exchange (SPDX) ライセンス識別子を使用するという方法があります。SPDX ライセンス識別子はプログラムで簡単にパースすることができ、ファイルがどのライセンスで配布されているのか正確・簡潔に記述できます。SPDX ライセンス記述子は Linux Foundation の SPDX Workgroup で管理されており業界・ツールベンダー・法務チームなどパートナーの承認を得ています。詳しい情報は https://spdx.org/ を見てください。

Linux カーネルは全てのソースファイルに対して正確な SPDX 記述子を必要とします。カーネル内で使われている有効な記述子については `ライセンス記述子`_ セクションで説明しています。また、公式 SPDX ライセンスリスト https://spdx.org/licenses/ とライセンス文章を載せています。

ライセンス識別子の書式
-------------------------

1. 配置:

   SPDX ライセンス識別子はカーネルファイルのできるかぎり上部に追加します。大部分のファイルでは1行目が使われますが、最初の行に '#!PATH_TO_INTERPRETER' と記述する必要があるスクリプトでは SPDX 記述子は2行目に配置します。

|

2. 形式:

   SPDX ライセンス記述子はコメントの形で追加します。コメントの形式はファイルのタイプによって変わります::

      C ソース:	// SPDX-License-Identifier: <SPDX License Expression>
      C ヘッダー:	/* SPDX-License-Identifier: <SPDX License Expression> */
      ASM:	/* SPDX-License-Identifier: <SPDX License Expression> */
      スクリプト:	# SPDX-License-Identifier: <SPDX License Expression>
      .rst:	.. SPDX-License-Identifier: <SPDX License Expression>
      .dts{i}:	// SPDX-License-Identifier: <SPDX License Expression>

   標準のコメントスタイルを特定のツールが処理できないときは、ツールが認識できる適切なコメント方式を使用します。C ヘッダーファイルで "/\* \*/" 形式のコメントが使われているのはそのためです。.lds ファイルが生成されるときに 'ld' が C++ コメントをパースできずにビルドが失敗するという現象が以前は存在していました。今ではもう解決されている問題ですが、いまでも古いアセンブラツールでは C++ スタイルコメントを扱えない場合があります。

|

3. 構文:

   <SPDX License Expression> は SPDX License List にあるライセンス識別子の SPDX 省略形、あるいは複数のライセンス識別子の SPDX 省略形の組み合わせで、組み合わせるときはライセンスの例外が適用される場合を "WITH" で区切ります。複数のライセンスが適用されるときは、副表現を "AND" と "OR" キーワードで分割したり "(" と ")" で囲ったりします。

   [L]GPL のような 'or later' オプションが存在するライセンスでは "+" を使って 'or later' オプションを示します::

      // SPDX-License-Identifier: GPL-2.0+
      // SPDX-License-Identifier: LGPL-2.1+

   ライセンスに修正が必要なときは WITH を使います。例えば、Linux カーネルの UAPI ファイルは以下のように例外を使っています::

      // SPDX-License-Identifier: GPL-2.0 WITH Linux-syscall-note
      // SPDX-License-Identifier: GPL-2.0+ WITH Linux-syscall-note

   カーネルには他にも以下のように WITH 例外を使っている箇所があります::

      // SPDX-License-Identifier: GPL-2.0 WITH mif-exception
      // SPDX-License-Identifier: GPL-2.0+ WITH GCC-exception-2.0

   例外は特定のライセンス識別子と組み合わせて使う必要があります。有効なライセンス識別子は exception テキストファイルのタグに記載されています。詳しくは `ライセンス識別子`_ チャプターの `例外`_ セクションを見てください。

   OR はファイルがデュアルライセンスでどちらか片方のライセンスが選択される場合に使用します。例えば、一部の dtsi ファイルはデュアルライセンスで配布されています::

      // SPDX-License-Identifier: GPL-2.0 OR BSD-3-Clause

   デュアルライセンスのファイルのライセンス表現の例::

      // SPDX-License-Identifier: GPL-2.0 OR MIT
      // SPDX-License-Identifier: GPL-2.0 OR BSD-2-Clause
      // SPDX-License-Identifier: GPL-2.0 OR Apache-2.0
      // SPDX-License-Identifier: GPL-2.0 OR MPL-1.1
      // SPDX-License-Identifier: (GPL-2.0 WITH Linux-syscall-note) OR MIT
      // SPDX-License-Identifier: GPL-1.0+ OR BSD-3-Clause OR OpenSSL

   AND はファイルに複数のライセンスが存在し、ファイルを使うときは全てのライセンスが適用されるときに使用します。例えば、他のプロジェクトから継承されたコードでカーネルに含める許可が得られているが、元々のライセンスの効果は失われていない場合::

      // SPDX-License-Identifier: (GPL-2.0 WITH Linux-syscall-note) AND MIT

   複数のライセンスが適用される他の例::

      // SPDX-License-Identifier: GPL-1.0+ AND LGPL-2.1+

ライセンス識別子
-------------------

The licenses currently used, as well as the licenses for code added to the
kernel, can be broken down into:

1. _`推奨ライセンス`:

   Whenever possible these licenses should be used as they are known to be
   fully compatible and widely used.  These licenses are available from the
   directory::

      LICENSES/preferred/

   in the kernel source tree.

   The files in this directory contain the full license text and
   `Metatags`_.  The file names are identical to the SPDX license
   identifier which shall be used for the license in source files.

   Examples::

      LICENSES/preferred/GPL-2.0

   Contains the GPL version 2 license text and the required metatags::

      LICENSES/preferred/MIT

   Contains the MIT license text and the required metatags

   _`Metatags`:

   The following meta tags must be available in a license file:

   - Valid-License-Identifier:

     One or more lines which declare which License Identifiers are valid
     inside the project to reference this particular license text.  Usually
     this is a single valid identifier, but e.g. for licenses with the 'or
     later' options two identifiers are valid.

   - SPDX-URL:

     The URL of the SPDX page which contains additional information related
     to the license.

   - Usage-Guidance:

     Freeform text for usage advice. The text must include correct examples
     for the SPDX license identifiers as they should be put into source
     files according to the `License identifier syntax`_ guidelines.

   - License-Text:

     All text after this tag is treated as the original license text

   File format examples::

      Valid-License-Identifier: GPL-2.0
      Valid-License-Identifier: GPL-2.0+
      SPDX-URL: https://spdx.org/licenses/GPL-2.0.html
      Usage-Guide:
        To use this license in source code, put one of the following SPDX
	tag/value pairs into a comment according to the placement
	guidelines in the licensing rules documentation.
	For 'GNU General Public License (GPL) version 2 only' use:
	  SPDX-License-Identifier: GPL-2.0
	For 'GNU General Public License (GPL) version 2 or any later version' use:
	  SPDX-License-Identifier: GPL-2.0+
      License-Text:
        Full license text

   ::

      SPDX-License-Identifier: MIT
      SPDX-URL: https://spdx.org/licenses/MIT.html
      Usage-Guide:
	To use this license in source code, put the following SPDX
	tag/value pair into a comment according to the placement
	guidelines in the licensing rules documentation.
	  SPDX-License-Identifier: MIT
      License-Text:
        Full license text

|

2. 非推奨ライセンス:

   These licenses should only be used for existing code or for importing
   code from a different project.  These licenses are available from the
   directory::

      LICENSES/other/

   in the kernel source tree.

   The files in this directory contain the full license text and
   `Metatags`_.  The file names are identical to the SPDX license
   identifier which shall be used for the license in source files.

   Examples::

      LICENSES/other/ISC

   Contains the Internet Systems Consortium license text and the required
   metatags::

      LICENSES/other/ZLib

   Contains the ZLIB license text and the required metatags.

   Metatags:

   The metatag requirements for 'other' licenses are identical to the
   requirements of the `Preferred licenses`_.

   File format example::

      Valid-License-Identifier: ISC
      SPDX-URL: https://spdx.org/licenses/ISC.html
      Usage-Guide:
        Usage of this license in the kernel for new code is discouraged
	and it should solely be used for importing code from an already
	existing project.
        To use this license in source code, put the following SPDX
	tag/value pair into a comment according to the placement
	guidelines in the licensing rules documentation.
	  SPDX-License-Identifier: ISC
      License-Text:
        Full license text

|

3. _`例外`:

   Some licenses can be amended with exceptions which grant certain rights
   which the original license does not.  These exceptions are available
   from the directory::

      LICENSES/exceptions/

   in the kernel source tree.  The files in this directory contain the full
   exception text and the required `Exception Metatags`_.

   Examples::

      LICENSES/exceptions/Linux-syscall-note

   Contains the Linux syscall exception as documented in the COPYING
   file of the Linux kernel, which is used for UAPI header files.
   e.g. /\* SPDX-License-Identifier: GPL-2.0 WITH Linux-syscall-note \*/::

      LICENSES/exceptions/GCC-exception-2.0

   Contains the GCC 'linking exception' which allows to link any binary
   independent of its license against the compiled version of a file marked
   with this exception. This is required for creating runnable executables
   from source code which is not compatible with the GPL.

   _`Exception Metatags`:

   The following meta tags must be available in an exception file:

   - SPDX-Exception-Identifier:

     One exception identifier which can be used with SPDX license
     identifiers.

   - SPDX-URL:

     The URL of the SPDX page which contains additional information related
     to the exception.

   - SPDX-Licenses:

     A comma separated list of SPDX license identifiers for which the
     exception can be used.

   - Usage-Guidance:

     Freeform text for usage advice. The text must be followed by correct
     examples for the SPDX license identifiers as they should be put into
     source files according to the `License identifier syntax`_ guidelines.

   - Exception-Text:

     All text after this tag is treated as the original exception text

   File format examples::

      SPDX-Exception-Identifier: Linux-syscall-note
      SPDX-URL: https://spdx.org/licenses/Linux-syscall-note.html
      SPDX-Licenses: GPL-2.0, GPL-2.0+, GPL-1.0+, LGPL-2.0, LGPL-2.0+, LGPL-2.1, LGPL-2.1+
      Usage-Guidance:
        This exception is used together with one of the above SPDX-Licenses
	to mark user-space API (uapi) header files so they can be included
	into non GPL compliant user-space application code.
        To use this exception add it with the keyword WITH to one of the
	identifiers in the SPDX-Licenses tag:
	  SPDX-License-Identifier: <SPDX-License> WITH Linux-syscall-note
      Exception-Text:
        Full exception text

   ::

      SPDX-Exception-Identifier: GCC-exception-2.0
      SPDX-URL: https://spdx.org/licenses/GCC-exception-2.0.html
      SPDX-Licenses: GPL-2.0, GPL-2.0+
      Usage-Guidance:
        The "GCC Runtime Library exception 2.0" is used together with one
	of the above SPDX-Licenses for code imported from the GCC runtime
	library.
        To use this exception add it with the keyword WITH to one of the
	identifiers in the SPDX-Licenses tag:
	  SPDX-License-Identifier: <SPDX-License> WITH GCC-exception-2.0
      Exception-Text:
        Full exception text


All SPDX license identifiers and exceptions must have a corresponding file
in the LICENSE subdirectories. This is required to allow tool
verification (e.g. checkpatch.pl) and to have the licenses ready to read
and extract right from the source, which is recommended by various FOSS
organizations, e.g. the `FSFE REUSE initiative <https://reuse.software/>`_.
