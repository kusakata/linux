===============================
Linux Security Module 使用方法
===============================

Linux Security Module (LSM) フレームワークは新しいカーネル拡張によってフックされる様々なセキュリティチェックのためのメカニズムを提供します。"module" という名前はやや的を外れています。これらの拡張はローダブルカーネルモジュールではないためです。LSM フレームワークは CONFIG_DEFAULT_SECURITY でビルド時に選択します。また、カーネルに複数の LSM を組み込んだ場合、起動時に ``"security=..."`` カーネルコマンドライン引数で上書きすることができます。

The primary users of the LSM interface are Mandatory Access Control
(MAC) extensions which provide a comprehensive security policy. Examples
include SELinux, Smack, Tomoyo, and AppArmor. In addition to the larger
MAC extensions, other extensions can be built using the LSM to provide
specific changes to system operation when these tweaks are not available
in the core functionality of Linux itself.

Without a specific LSM built into the kernel, the default LSM will be the
Linux capabilities system. Most LSMs choose to extend the capabilities
system, building their checks on top of the defined capability hooks.
For more details on capabilities, see ``capabilities(7)`` in the Linux
man-pages project.

A list of the active security modules can be found by reading
``/sys/kernel/security/lsm``. This is a comma separated list, and
will always include the capability module. The list reflects the
order in which checks are made. The capability module will always
be first, followed by any "minor" modules (e.g. Yama) and then
the one "major" module (e.g. SELinux) if there is one configured.

.. toctree::
   :maxdepth: 1

   apparmor
   LoadPin
   SELinux
   Smack
   tomoyo
   Yama
