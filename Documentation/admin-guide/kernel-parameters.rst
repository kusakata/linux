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

Note that for the special case of a range one can split the range into equal
sized groups and for each group use some amount from the beginning of that
group:

	<cpu number>-cpu number>:<used size>/<group size>

For example one can add to the command line following parameter:

	isolcpus=1,2,10-20,100-2000:2/25

where the final item represents CPUs 100,101,125,126,150,151,...



This document may not be entirely up to date and comprehensive. The command
"modinfo -p ${modulename}" shows a current list of all parameters of a loadable
module. Loadable modules, after being loaded into the running kernel, also
reveal their parameters in /sys/module/${modulename}/parameters/. Some of these
parameters may be changed at runtime by the command
``echo -n ${value} > /sys/module/${modulename}/parameters/${parm}``.

The parameters listed below are only valid if certain kernel build options were
enabled and if respective hardware is present. The text in square brackets at
the beginning of each description states the restrictions within which a
parameter is applicable::

	ACPI	ACPI support is enabled.
	AGP	AGP (Accelerated Graphics Port) is enabled.
	ALSA	ALSA sound support is enabled.
	APIC	APIC support is enabled.
	APM	Advanced Power Management support is enabled.
	ARM	ARM architecture is enabled.
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

In addition, the following text indicates that the option::

	BUGS=	Relates to possible processor bugs on the said processor.
	KNL	Is a kernel start-up parameter.
	BOOT	Is a boot loader parameter.

Parameters denoted with BOOT are actually interpreted by the boot
loader, and have no meaning to the kernel directly.
Do not modify the syntax of boot loader parameters without extreme
need or coordination with <Documentation/x86/boot.txt>.

There are also arch-specific kernel-parameters not documented here.
See for example <Documentation/x86/x86_64/boot-options.txt>.

Note that ALL kernel parameters listed below are CASE SENSITIVE, and that
a trailing = on the name of any parameter states that that parameter will
be entered as an environment variable, whereas its absence indicates that
it will appear as a kernel argument readable via /proc/cmdline by programs
running once the system is up.

The number of kernel parameters is not limited, but the length of the
complete command line (parameters including spaces etc.) is limited to
a fixed number of characters. This limit depends on the architecture
and is between 256 and 4096 characters. It is defined in the file
./include/asm/setup.h as COMMAND_LINE_SIZE.

Finally, the [KMG] suffix is commonly described after a number of kernel
parameter values. These 'K', 'M', and 'G' letters represent the _binary_
multipliers 'Kilo', 'Mega', and 'Giga', equaling 2^10, 2^20, and 2^30
bytes respectively. Such letter suffixes can also be entirely omitted:

.. include:: kernel-parameters.txt
   :literal:

Todo
----

	Add more DRM drivers.
