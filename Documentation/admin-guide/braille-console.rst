Linux 点字コンソール
=====================

点字デバイスに起動初期段階 (ユーザー空間のスクリーンリーダーが起動する前) のメッセージを表示するには、通常のシリアルコンソールのサポート (:ref:`Documentation/admin-guide/serial-console.rst <serial_console>` を参照) と点字デバイスのサポート (:menuselection:`Device Drivers --> Accessibility support --> Console on braille device`) をコンパイルする必要があります。

そしてカーネルコマンドラインで ``console=brl`` オプションを指定してください。フォーマットは::

	console=brl,serial_options...

``serial_options...`` は :ref:`Documentation/admin-guide/serial-console.rst <serial_console>` の説明と同じです。

例えば点字デバイスが1番目のシリアルポートに接続されている場合は ``console=brl,ttyS0`` を使用し、ボーレートを 115200 に上書きする場合は ``console=brl,ttyS0,115200`` を使用します。

デフォルトでは、点字デバイスは最後のカーネルメッセージだけを表示します (コンソールモード)。前のメッセージを見たいときは、Insert キーを押して VT レビューモードに切り替えてください。レビューモードでは基本的な画面レビュー機能を提供します。方向キーで VT の中身を移動でき、:kbd:`PAGE-UP`/:kbd:`PAGE-DOWN` キーで画面の一番上・下に移動できます。また、:kbd:`HOME` キーでカーソルに戻ることができます。

``braille_console.sound=1`` カーネルパラメータを追加することで音によるフィードバックが有効になります。

わかりやすくするために、有効にできる点字コンソールはひとつだけと決まっており、他の ``console=brl,...`` は無視されます。また、:ref:`Documentation/admin-guide/serial-console.rst <serial_console>` で説明されているコンソールの選択には干渉しません。

現在のところ、VisioBraille デバイスだけがサポートされています。

Samuel Thibault <samuel.thibault@ens-lyon.org>
