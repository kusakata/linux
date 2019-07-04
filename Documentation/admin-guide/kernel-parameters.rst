.. _kernelparameters:

カーネルのコマンドラインパラメータ
====================================

以下は __setup(), core_param(), module_param() マクロによって実装されているカーネルパラメータの英語辞書順 (句読点を無視して大文字・小文字を区別しないで文字よりも先に数字が来ます) のリストと説明です。

カーネルはカーネルコマンドラインの "--" までのパラメータをパースします。パラメータが認識されずコマンドラインに '.' が含まれていない場合、パラメータは init に渡されます: '=' が付くパラメータは init の環境に渡され、他のパラメータはコマンドライン引数として init に渡されます。"--" 以後の文字列は init の引数として渡されます。

モジュールパラメータは2つの方法で指定することができます: モジュール名のプリフィックスを付けてカーネルコマンドラインで指定するか、modprobe を使用します。例::

	(kernel command line) usbcore.blinkenlights=1
	(modprobe command line) modprobe usbcore blinkenlights=1

カーネルに組み込まれたモジュールのパラメータはカーネルコマンドラインで指定する必要があります。modprobe はカーネルコマンドライン (/proc/cmdline) を見てからモジュールをロードするときにモジュールパラメータを収集するため、カーネルコマンドラインはローダブルモジュールに対しても使用できます。

パラメータ名のハイフン (ダッシュ) とアンダーバーは同じ意味を持ちます::

	log_buf_len=1M print-fatal-signals=1

上記のパラメータは以下のように入力することもできます::

	log-buf-len=1M print_fatal_signals=1

値に空白が入るときはダブルクオーテーションで囲うことができます。例::

	param="spaces in here"

cpu lists:
----------

一部のカーネルパラメータ (例: isolcpus, nohz_full, irqaffinity, rcu_nocbs) では値として CPU のリストを入力します。リストのフォーマットは以下の通り:

	<cpu number>,...,<cpu number>

または:

	<cpu number>-<cpu number>
	(must be a positive range in ascending order)

もしくは上記を組み合わせて:

   <cpu number>,...,<cpu number>-<cpu number>

特殊なケースとして使用する CPU をグループに分割して、グループの最初から同じ数ずつ使用させることができます:

	<cpu number>-cpu number>:<used size>/<group size>

例えば以下のパラメータをコマンドラインに追加した場合:

	isolcpus=1,2,10-20,100-2000:2/25

最後のアイテムは CPU の 100,101,125,126,150,151,... を表します。



このドキュメントでは最新のパラメータ全てを網羅できていません。"modinfo -p ${modulename}" コマンドを実行することでローダブルモジュールの全てのパラメータのリストが表示されます。カーネルにロードされた後、ローダブルモジュールのパラメータには /sys/module/${modulename}/parameters/ からアクセスできるようになります。一部のパラメータは ``echo -n ${value} > /sys/module/${modulename}/parameters/${parm}`` コマンドを実行することで動的に変更することができます。

下に記載しているパラメータはカーネルのビルド時のオプションを有効にして、該当するハードウェアが存在する場合にのみ使用することができます。角括弧のテキストはパラメータが利用できる条件について説明しています::

	ACPI	ACPI support is enabled.
	AGP	AGP (Accelerated Graphics Port) is enabled.
	ALSA	ALSA sound support is enabled.
	APIC	APIC support is enabled.
	APM	Advanced Power Management support is enabled.
	ARM	ARM architecture is enabled.
	ARM64	ARM64 architecture is enabled.
	AX25	Appropriate AX.25 support is enabled.
	CLK	Common clock infrastructure is enabled.
	CMA	Contiguous Memory Area support is enabled.
	DRM	Direct Rendering Management support is enabled.
	DYNAMIC_DEBUG Build in debug messages and enable them at runtime
	EDD	BIOS Enhanced Disk Drive Services (EDD) is enabled
	EFI	EFI Partitioning (GPT) is enabled
	EIDE	EIDE/ATAPI support is enabled.
	EVM	Extended Verification Module
	FB	The frame buffer device is enabled.
	FTRACE	Function tracing enabled.
	GCOV	GCOV profiling is enabled.
	HW	Appropriate hardware is enabled.
	IA-64	IA-64 architecture is enabled.
	IMA     Integrity measurement architecture is enabled.
	IOSCHED	More than one I/O scheduler is enabled.
	IP_PNP	IP DHCP, BOOTP, or RARP is enabled.
	IPV6	IPv6 support is enabled.
	ISAPNP	ISA PnP code is enabled.
	ISDN	Appropriate ISDN support is enabled.
	ISOL	CPU Isolation is enabled.
	JOY	Appropriate joystick support is enabled.
	KGDB	Kernel debugger support is enabled.
	KVM	Kernel Virtual Machine support is enabled.
	LIBATA  Libata driver is enabled
	LP	Printer support is enabled.
	LOOP	Loopback device support is enabled.
	M68k	M68k architecture is enabled.
			These options have more detailed description inside of
			Documentation/m68k/kernel-options.txt.
	MDA	MDA console support is enabled.
	MIPS	MIPS architecture is enabled.
	MOUSE	Appropriate mouse support is enabled.
	MSI	Message Signaled Interrupts (PCI).
	MTD	MTD (Memory Technology Device) support is enabled.
	NET	Appropriate network support is enabled.
	NUMA	NUMA support is enabled.
	NFS	Appropriate NFS support is enabled.
	OSS	OSS sound support is enabled.
	PV_OPS	A paravirtualized kernel is enabled.
	PARIDE	The ParIDE (parallel port IDE) subsystem is enabled.
	PARISC	The PA-RISC architecture is enabled.
	PCI	PCI bus support is enabled.
	PCIE	PCI Express support is enabled.
	PCMCIA	The PCMCIA subsystem is enabled.
	PNP	Plug & Play support is enabled.
	PPC	PowerPC architecture is enabled.
	PPT	Parallel port support is enabled.
	PS2	Appropriate PS/2 support is enabled.
	RAM	RAM disk support is enabled.
	RDT	Intel Resource Director Technology.
	S390	S390 architecture is enabled.
	SCSI	Appropriate SCSI support is enabled.
			A lot of drivers have their options described inside
			the Documentation/scsi/ sub-directory.
	SECURITY Different security models are enabled.
	SELINUX SELinux support is enabled.
	APPARMOR AppArmor support is enabled.
	SERIAL	Serial support is enabled.
	SH	SuperH architecture is enabled.
	SMP	The kernel is an SMP kernel.
	SPARC	Sparc architecture is enabled.
	SWSUSP	Software suspend (hibernation) is enabled.
	SUSPEND	System suspend states are enabled.
	TPM	TPM drivers are enabled.
	TS	Appropriate touchscreen support is enabled.
	UMS	USB Mass Storage support is enabled.
	USB	USB support is enabled.
	USBHID	USB Human Interface Device support is enabled.
	V4L	Video For Linux support is enabled.
	VMMIO   Driver for memory mapped virtio devices is enabled.
	VGA	The VGA console has been enabled.
	VT	Virtual terminal support is enabled.
	WDT	Watchdog support is enabled.
	XT	IBM PC/XT MFM hard disk support is enabled.
	X86-32	X86-32, aka i386 architecture is enabled.
	X86-64	X86-64 architecture is enabled.
			More X86-64 boot options can be found in
			Documentation/x86/x86_64/boot-options.txt .
	X86	Either 32-bit or 64-bit x86 (same as X86-32+X86-64)
	X86_UV	SGI UV support is enabled.
	XEN	Xen support is enabled

さらに、以下のテキストはオプションに以下の意味があります::

	BUGS=	Relates to possible processor bugs on the said processor.
	KNL	Is a kernel start-up parameter.
	BOOT	Is a boot loader parameter.

BOOT と書かれたパラメータはブートローダーによって認識されます。カーネルには直接的な効果がありません。特に必要がない場合はブートローダーパラメータの構文は変更しないでください。<Documentation/x86/boot.txt> も参照。

ここではアーキテクチャ固有のカーネルパラメータについては列挙していません。<Documentation/x86/x86_64/boot-options.txt> などを見てください。

以下に記載しているカーネルパラメータは全て大文字・小文字を区別します。また、パラメータの名前に = が付いている場合は環境変数としてパラメータが入力され、付いていない場合はシステムが立ち上がったときにプログラムによって /proc/cmdline から読み込むことができるカーネル引数となります。

カーネルパラメータの数に制限はありませんが、コマンドラインの文字数 (パラメータと空白を含む) は最大長があります。この制限はアーキテクチャによって異なり、256文字から4096文字です。./include/asm/setup.h ファイルで COMMAND_LINE_SIZE として定義されています。

最後に、カーネルパラメータの値として数字の後に [KMG] が使われることがあります。'K', 'M', 'G' はバイナリの単位 'Kilo', 'Mega', 'Giga' をあらわし、それぞれ 2^10, 2^20, 2^30 バイトと等しくなっています。これらの接尾辞は省略できます:

.. include:: kernel-parameters.txt
   :literal:

Todo
----

	DRM ドライバーを追加。
