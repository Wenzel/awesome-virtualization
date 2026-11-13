# Awesome Virtualization [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

Resources for people who build, break and introspect hypervisors: CPU virtualization internals, hypervisor development, virtual machine introspection and hypervisor security.

Management platforms, desktop apps, containers, sandboxes and CPU emulators are out of scope; see [Related lists](#related-lists).

## Contents

- [Start here](#start-here)
- [Chronology](#chronology)
- [Foundations](#foundations)
    - [Specifications](#specifications)
    - [Books](#books)
    - [Courses](#courses)
    - [Papers](#papers)
- [Hypervisor internals](#hypervisor-internals)
    - [KVM](#kvm)
    - [Xen](#xen)
    - [QEMU](#qemu)
    - [Hyper-V](#hyper-v)
    - [VMware](#vmware)
    - [VirtualBox](#virtualbox)
- [Building hypervisors](#building-hypervisors)
    - [Tutorials](#tutorials)
    - [Teaching hypervisors](#teaching-hypervisors)
    - [Special-purpose hypervisors](#special-purpose-hypervisors)
    - [Production VMMs and research hypervisors](#production-vmms-and-research-hypervisors)
- [Introspection and debugging](#introspection-and-debugging)
    - [Tools](#tools)
    - [Papers and talks](#papers-and-talks)
- [Security](#security)
    - [Attacking hypervisors](#attacking-hypervisors)
    - [Fuzzing](#fuzzing)
    - [Confidential VMs](#confidential-vms)
    - [VM detection and malware analysis](#vm-detection-and-malware-analysis)
- [Related lists](#related-lists)

## Start here

Write your first hypervisor:

1. Read *Hardware and Software Support for Virtualization* for the concepts ([Books](#books)).
2. Keep the Intel SDM volume 3C and the VMCS layout open as references ([Specifications](#specifications)).
3. Follow *Hypervisor From Scratch* or *Hypervisor 101 in Rust* end to end ([Tutorials](#tutorials)).
4. Read SimpleVisor, then HyperPlatform or hvpp, to see complete small implementations ([Teaching hypervisors](#teaching-hypervisors)).
5. Read *MMU Virtualization via Intel EPT* before adding memory virtualization ([Tutorials](#tutorials)).
6. Compare with a production codebase such as Firecracker or NOVA ([Production VMMs and research hypervisors](#production-vmms-and-research-hypervisors)).

Start in hypervisor security:

1. Watch *Lessons Learned from Eight Years of Breaking Hypervisors* for the bug classes ([Attacking hypervisors](#attacking-hypervisors)).
2. Read *Hypervisor Vulnerability Research: State of the Art* for the attack surface of each hypervisor ([Attacking hypervisors](#attacking-hypervisors)).
3. Work through one full exploit write-up: *An EPYC escape* for KVM or the Quarkslab series for Xen ([Attacking hypervisors](#attacking-hypervisors)).
4. Read *First Steps in Hyper-V Research* to set up a debugging environment ([Hyper-V](#hyper-v)).
5. Read the HyperCube and Morphuzz papers, then run kAFL ([Fuzzing](#fuzzing)).
6. Learn what the hardware-isolated threat model changes with SEVered and Heckler ([Confidential VMs](#confidential-vms)).

## Chronology

| Date | Vendor | Milestone |
|---|---|---|
| 2005-11-13 | Intel | `VT-x` released on `Pentium 4` (models `662` and `672`) |
| 2006-05-23 | AMD | `AMD-V` released on `Orleans` and `Windsor` processors |
| 2007-09-10 | AMD | `Barcelona` adds `RVI` (*Rapid Virtualization Indexing*), a.k.a. *Nested Page Tables*, AMD's `SLAT` |
| 2008-11 | Intel | `Nehalem` adds `EPT` (*Extended Page Tables*, Intel's `SLAT`) and `VPID` (*Virtual Processor ID*) |
| 2010-01-07 | Intel | `Westmere` adds `unrestricted guest` (*real mode support*) |
| 2013-06-04 | Intel | `Haswell` adds `VMCS Shadowing`, `VMFUNC`, `#VE` and `EPTP` switching |
| 2017-06-21 | AMD | `EPYC` adds `Secure Encrypted Virtualization` (*SEV*) |
| 2017 | AMD | Documents `Encrypted State` (*SEV-ES*) |
| 2019 | AMD | Documents `Secure Nested Paging` (*SEV-SNP*) |
| 2019-08-01 | Intel | `Ice Lake` adds `EPT SPP` (*EPT-Based Sub-Page Write Protection*) and virtualization of the `Intel Processor Trace` output buffer using EPT |
| 2020-03 | Intel | Documents `Hypervisor-Managed Linear Address Translation` (*HLAT*) |
| 2021-03 | AMD | `EPYC Milan` ships `SEV-SNP` |
| 2021-03 | Arm | Announces the `Confidential Compute Architecture` (*CCA*) and its `Realm Management Extension` (*RME*) with Armv9-A |
| 2023-01 | Intel | `Sapphire Rapids` ships `Trust Domain Extensions` (*TDX*) |
| 2024 | Linux | KVM gains `SEV-SNP` host support (6.11) |
| 2025 | Linux | KVM gains `TDX` host support (6.16) |

## Foundations

### Specifications

- [Intel 64 and IA-32 Architectures Software Developer's Manual](https://www.intel.com/content/www/us/en/developer/articles/technical/intel-sdm.html) - The reference for VT-x; volume 3C covers VMX operation, the VMCS, VM entries and exits, and EPT.
- [VMCS Layout](https://github.com/ayoubfaouzi/cpu-internals/blob/main/VMCS-Layout.pdf) - Every VMCS field and its encoding on a single page.
- [VMX Caps](https://htmlpreview.github.io/?https://github.com/honorarybot/VmxCaps/blob/master/vmx.html) - Table of the VMX capabilities reported by Intel processors. Unmaintained since 2020.
- [VIRTIO specification](https://github.com/oasis-tcs/virtio-spec) - OASIS standard for paravirtualized devices, implemented by every mainstream hypervisor.
- [RISC-V Instruction Set Manual](https://github.com/riscv/riscv-isa-manual) - The privileged volume defines the hypervisor (H) extension.

### Books

- [Hardware and Software Support for Virtualization](https://www.amazon.com/Hardware-Software-Virtualization-Synthesis-Architecture/dp/1627056939) - Bugnion, Nieh and Tsafrir, 2017. The best single text on CPU, memory and I/O virtualization on x86 and Arm.
- [Virtual Machines: Versatile Platforms for Systems and Processes](https://www.amazon.com/Virtual-Machines-Versatile-Platforms-Architecture/dp/1558609105) - Smith and Nair, 2005. Broad taxonomy of process and system virtual machines, including binary translation.
- [Mastering KVM Virtualization](https://www.amazon.com/Mastering-Virtualization-Humble-Devassy-Chirammal/dp/1784399051) - Chirammal, Mukhedkar and Vettathu, 2016. Operations-oriented, with a chapter on KVM and QEMU internals.

### Courses

- [Advanced Operating Systems: memory virtualization](https://www.youtube.com/watch?v=-y9J78wSJHY&list=PLGvfHSgImk4aP4moOrG-KEqVO8gRFh4rb&index=122) - Georgia Tech on Udacity. Lecture videos on shadow page tables, ballooning and memory sharing.
- [Full Virtualization](https://www.youtube.com/watch?v=fYH8A3RjPwY) - Geoffrey Challen, 2017. Undergraduate lecture on trap-and-emulate and why x86 was hard to virtualize.
- [Xen and the Art of Virtualization](https://www.youtube.com/watch?v=2moUsgMOie4) - Geoffrey Challen, 2017. Lecture walking through the Xen paper and paravirtualization.
- [Advanced x86: Virtualization with Intel VT-x](http://opensecuritytraining.info/AdvancedX86-VTX.html) - David Weinstein, OpenSecurityTraining. Slides and labs for a full VT-x course.
- [From Kernel to VMM](https://www.youtube.com/watch?v=FSw8Ff1SFLM) - Jacob Torrey, Dartmouth. Introduction to what a VMM adds on top of a kernel.
- [Virtualization and Cloud Computing lectures](https://www.youtube.com/playlist?list=PLDW872573QAbcpQ7VSUdcm4o3tgnQYBE8) - Mythili Vutukuru, IIT Bombay. Graduate course covering CPU, memory and I/O virtualization.

### Papers

- [Formal Requirements for Virtualizable Third Generation Architectures](https://doi.org/10.1145/361011.361073) - Popek and Goldberg, CACM 1974. Defines when an architecture can be virtualized by trap-and-emulate.
- [Xen and the Art of Virtualization](https://doi.org/10.1145/945445.945462) - Barham et al., SOSP 2003. Introduces paravirtualization on x86.
- [A Comparison of Software and Hardware Techniques for x86 Virtualization](https://doi.org/10.1145/1168857.1168860) - Adams and Agesen, ASPLOS 2006. Binary translation against first-generation VT-x, and why hardware was not yet faster.
- [kvm: the Linux Virtual Machine Monitor](https://www.kernel.org/doc/ols/2007/ols2007v1-pages-225-230.pdf) - Kivity et al., Ottawa Linux Symposium 2007. The original KVM design in six pages.
- [Dynamic Binary Translation from x86-32 Code to x86-64 Code for Virtualization](https://dspace.mit.edu/handle/1721.1/53095) - Yu-hsin Chen, MIT thesis, 2009. Detailed design of a binary translator inside a VMM.
- [The Evolution of an x86 Virtual Machine Monitor](https://doi.org/10.1145/1899928.1899930) - Agesen et al., SIGOPS OSR 2010. How VMware's monitor changed as hardware support arrived.
- [The Turtles Project: Design and Implementation of Nested Virtualization](https://www.usenix.org/conference/osdi10/turtles-project-design-and-implementation-nested-virtualization) - Ben-Yehuda et al., OSDI 2010. How KVM runs hypervisors inside guests.
- [Bringing Virtualization to the x86 Architecture with the Original VMware Workstation](https://doi.org/10.1145/2382553.2382554) - Bugnion et al., ACM TOCS 2012. Retrospective on virtualizing x86 before hardware support.
- [KVM/ARM: The Design and Implementation of the Linux ARM Hypervisor](https://doi.org/10.1145/2541940.2541946) - Dall and Nieh, ASPLOS 2014. Split-mode virtualization on Arm.
- [MemoryRanger Prevents Hijacking FILE_OBJECT Structures in Windows Kernel](https://igorkorkin.blogspot.com/2019/04/memoryranger-prevents-hijacking.html) - Igor Korkin, 2019. Uses EPT to isolate kernel drivers from each other.
- [Protecting Cloud Virtual Machines from Hypervisor and Host Operating System Exploits](https://www.usenix.org/conference/usenixsecurity19/presentation/li-shih-wei) - Li et al., USENIX Security 2019. HypSec shrinks the KVM trusted computing base to a small core.
- [Firecracker: Lightweight Virtualization for Serverless Applications](https://www.usenix.org/conference/nsdi20/presentation/agache) - Agache et al., NSDI 2020. Design rationale for a minimal KVM-based VMM.

## Hypervisor internals

### KVM

- [KVM documentation](https://docs.kernel.org/virt/kvm/index.html) - Kernel documentation for the KVM API, MMU, nested virtualization and per-architecture details.
- [KVM website](http://www.linux-kvm.org/page/Main_Page) - Project wiki.
- [KVM Forum](http://www.linux-kvm.org/page/KVM_Forum) - Yearly developer conference; slides and videos for every edition.
- [How VT-x, KVM and QEMU Work Together](https://binarydebt.wordpress.com/2018/10/14/intel-virtualisation-how-vt-x-kvm-and-qemu-work-together) - Binary Debt, 2018. Follows a guest from QEMU through the KVM ioctls down to VMX.

### Xen

- [Xen website](https://www.xenproject.org/) - Project home.
- [Xen documentation](https://xenbits.xenproject.org/docs/) - Hypercall interfaces, design documents and man pages for each release.

### QEMU

- [QEMU website](https://www.qemu.org/) - Project home.
- [QEMU documentation](https://www.qemu.org/docs/master/) - System emulation, device models and developer internals.
- [QEMU Starter](https://github.com/TunaCici/QEMU_Starter) - Beginner's guide to running and configuring QEMU. Unmaintained since 2023.

### Hyper-V

- [Virtualization documentation](https://learn.microsoft.com/en-us/virtualization/) - Official Microsoft documentation.
- [Hypervisor Top Level Functional Specification](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/tlfs/tlfs) - Microsoft. The guest-visible interface: hypercalls, synthetic MSRs and partitions.
- [Hyper-V Internals](http://hvinternals.blogspot.com) - Arthur Khudyaev's blog, reverse engineering the hypervisor and its components.
- [Hyper-V internals research history](https://github.com/gerhart01/Hyper-V-Internals/blob/master/HyperResearchesHistory.md) - Chronological index of public Hyper-V research since 2006.
- [Battle of SKM and IUM](https://web.archive.org/web/20210531175722/http://www.alex-ionescu.com/blackhat2015.pdf) - Alex Ionescu, Black Hat USA 2015. How Windows 10 builds Virtualization Based Security on Hyper-V.
- [Virtualization Based Security - Part 1: The boot process](https://web.archive.org/web/20201112015140/https://blog.amossys.fr/virtualization-based-security-part1.html) - Amossys, 2017. How VBS starts from the boot loader. ([part 2: kernel communications](https://web.archive.org/web/20201111203054/https://blog.amossys.fr/virtualization-based-security-part2.html))
- [Hyper-V and its Memory Manager](http://www.andrea-allievi.com/files/Recon_2017_Montreal_HyperV_public.pptx) - Andrea Allievi, REcon 2017. Internals of the hypervisor's memory management.
- [First Steps in Hyper-V Research](https://www.microsoft.com/en-us/msrc/blog/2018/12/first-steps-in-hyper-v-research) - MSRC, 2018. Architecture overview and how to set up hypervisor debugging.
- [Hyper-V Internals and LIS](https://re.alisa.sh/notes/Hyper-V-LIS.html) - Alisa Esage, 2020. Notes on VMBus and the Linux Integration Services.

### VMware

- [Understanding Full Virtualization, Paravirtualization and Hardware Assist](https://web.archive.org/web/20201205015458/https://www.vmware.com/techpapers/2007/understanding-full-virtualization-paravirtualizat-1008.html) - VMware white paper, 2007. Short comparison of the three approaches.
- [The Architecture of VMware ESXi](https://web.archive.org/web/20191114094020/https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/techpaper/ESXi_architecture.pdf) - VMware white paper, 2008. VMkernel, user worlds and the management stack.

### VirtualBox

- [VirtualBox website](https://www.virtualbox.org/) - Project home.
- [VirtualBox technical documentation](https://www.virtualbox.org/wiki/Technical_documentation) - Developer wiki on the source tree, VMM and device emulation.

## Building hypervisors

### Tutorials

- [Hypervisor From Scratch](https://rayanfam.com/topics/hypervisor-from-scratch-part-1) - Sina Karvandi. Eight-part series building a VT-x hypervisor for Windows: VMX entry, VMCS setup, EPT, virtualizing a running system and hidden hooks.
- [5 Days to Virtualization](https://revers.engineering/day-0-virtual-environment-setup-scripts-and-windbg/) - Daax Rynd. Six-part series from environment setup to a VM-exit handler with CPUID emulation.
- [MMU Virtualization via Intel EPT](https://revers.engineering/mmu-ept-technical-details/) - Daax Rynd. Follow-up series on paging structures, EPT setup and EPT violations.
- [Hypervisor 101 in Rust](https://github.com/tandasat/Hypervisor-101-in-Rust) - Satoshi Tanda. One-day course that builds a fuzzing hypervisor for Intel and AMD, with exercises.

### Teaching hypervisors

Small enough to read in full. Many are no longer maintained and may not build on current toolchains; the code is still the best reference.

- [Blue Pill](http://www.invisiblethingslab.com/resources/bh07/nbp-0.32-public.zip) - Invisible Things Lab, 2007. Source of New Blue Pill, the hypervisor rootkit that moves a running OS into a VM.
- [SimpleVisor](https://github.com/ionescu007/SimpleVisor) - Alex Ionescu, 2016. Minimal VT-x hypervisor for Windows and UEFI, written to be read.
- [HyperPlatform](https://github.com/tandasat/HyperPlatform) - Satoshi Tanda, 2016. VT-x platform for Windows kernel monitoring. Archived.
- [SimpleSvm](https://github.com/tandasat/SimpleSvm) - Satoshi Tanda, 2017. The AMD SVM counterpart to SimpleVisor.
- [MiniVisorPkg](https://github.com/tandasat/MiniVisorPkg) - Satoshi Tanda, 2020. VT-x hypervisor built as both a UEFI and a Windows driver.
- [hvpp](https://github.com/wbenny/hvpp) - Petr Beneš, 2018. VT-x hypervisor in modern C++ with EPT hooking examples. Unmaintained since 2021.
- [ksm](https://github.com/asamy/ksm) - Ahmed Samy, 2017. VT-x hypervisor for Windows and Linux using EPT, `#VE` and `VMFUNC`. Unmaintained since 2021.
- [gbhv](https://github.com/Gbps/gbhv) - Gbps, 2018. Heavily commented VT-x hypervisor with EPT hooking. Unmaintained since 2023.
- [NoirVisor](https://github.com/Zero-Tang/NoirVisor) - Zero Tang, 2018. Supports both VT-x and AMD-V, with nested virtualization.
- [kHypervisor](https://github.com/KelvinMsft/kHypervisor) - Kelvin Chan, 2016. Nested VMM built on HyperPlatform. Unmaintained since 2021.
- [HyperBone](https://github.com/DarthTon/HyperBone) - DarthTon, 2016. Minimal VT-x hypervisor with hooks. Unmaintained since 2019.
- [hypervisor-for-beginners](https://github.com/rohaaan/hypervisor-for-beginners) - Rohan, 2017. Step-by-step VT-x samples. Unmaintained since 2017.
- [zpp_hypervisor](https://github.com/eyalz800/zpp_hypervisor) - Eyal Z, 2019. Simple VT-x hypervisor in C++ written as a learning exercise.
- [rustyvisor](https://github.com/iankronquist/rustyvisor) - Ian Kronquist, 2016. Early VT-x hypervisor in Rust. Unmaintained since 2022.
- [mythril](https://github.com/mythril-hypervisor/mythril) - Type-1 VT-x hypervisor in Rust, 2019. Unmaintained since 2022.
- [illusion-rs](https://github.com/memN0ps/illusion-rs) - UEFI blue-pill hypervisor in Rust with EPT hooks, by memN0ps. Archived.
- [matrix-rs](https://github.com/memN0ps/matrix-rs) - Windows kernel blue-pill hypervisor in Rust, by memN0ps. Archived.
- [HOSS](http://www.cs.unc.edu/~porter/hoss/) - Don Porter, 2014. Extends MIT's JOS teaching OS into a hypervisor, with guided lab exercises.

### Special-purpose hypervisors

- [ramooflax](https://github.com/airbus-seclab/ramooflax) - Airbus, 2011. Pre-boot hypervisor for remotely debugging a whole machine. Unmaintained since 2018.
- [VivienneVMM](https://github.com/changeofpace/VivienneVMM) - Stealthy hardware-breakpoint debugging through a VT-x hypervisor, by changeofpace. Unmaintained since 2020.
- [MemoryRanger](https://github.com/IgorKorkin/MemoryRanger) - Igor Korkin, 2019. Runs kernel drivers in separate EPT enclaves to stop data-only attacks.
- [applepie](https://github.com/gamozolabs/applepie) - Brandon Falk, 2018. Fuzzing hypervisor built on Bochs and the Windows Hypervisor Platform. Unmaintained since 2019.
- [orange_slice](https://github.com/gamozolabs/orange_slice) - Brandon Falk, 2019. Research kernel and hypervisor in Rust aiming at deterministic execution. Unmaintained since 2021.
- [Barbervisor](https://github.com/Cisco-Talos/Barbervisor) - Cisco Talos, 2020. Bare-metal VT-x hypervisor in Rust for snapshot fuzzing. Unmaintained since 2020.
- [vbh](https://github.com/intel/vbh) - Intel, 2019. Thin hypervisor for virtualization-based hardening of a Linux kernel. Archived.

### Production VMMs and research hypervisors

- [Firecracker](https://github.com/firecracker-microvm/firecracker) - AWS, 2018. Minimal KVM-based VMM in Rust behind Lambda and Fargate.
- [Cloud Hypervisor](https://github.com/cloud-hypervisor/cloud-hypervisor) - 2019. Rust VMM for cloud workloads on KVM and Microsoft Hypervisor.
- [crosvm](https://github.com/google/crosvm) - Google, 2017. The ChromeOS and Android VMM, where the Rust VMM ecosystem started.
- [rust-vmm](https://github.com/rust-vmm/community) - 2018. Shared Rust crates (KVM bindings, virtio, guest memory) used by the three VMMs above.
- [OpenVMM](https://github.com/microsoft/openvmm) - Microsoft, 2024. Rust VMM that also runs as OpenHCL, the paravisor used for Azure confidential VMs.
- [uhyve](https://github.com/hermit-os/uhyve) - 2019. Minimal hypervisor for the Hermit unikernel.
- [Android pKVM](https://source.android.com/docs/core/virtualization) - Google. Protected KVM on Arm64, which removes the host kernel from the guest's trusted computing base.
- [NOVA](https://github.com/udosteinberg/NOVA) - Udo Steinberg, 2010. Microhypervisor with a small trusted computing base for x86 and Arm.
- [Hedron](https://github.com/cyberus-technology/hedron) - Cyberus Technology, 2020. NOVA derivative. Unmaintained since 2023.
- [BitVisor](https://www.bitvisor.org/) - University of Tsukuba, 2008. Thin hypervisor that mediates I/O for a single guest. ([GitHub mirror](https://github.com/matsu/bitvisor))
- [Xvisor](https://github.com/xvisor/xvisor) - 2010. Monolithic type-1 hypervisor for Arm, RISC-V and x86.
- [Jailhouse](https://github.com/siemens/jailhouse) - Siemens, 2013. Linux-based static partitioning hypervisor. No commits since 2024.
- [Bao](https://github.com/bao-project/bao-hypervisor) - 2020. Static partitioning hypervisor for Arm and RISC-V mixed-criticality systems.
- [ACRN](https://github.com/projectacrn/acrn-hypervisor) - Intel, 2018. Type-1 hypervisor for embedded and IoT devices.
- [Bareflank](https://github.com/Bareflank/hypervisor) - Assured Information Security, 2015. SDK for building custom hypervisors. No commits since 2024.
- [Boxy](https://github.com/Bareflank/boxy) - Assured Information Security, 2018. Bareflank-based hypervisor for running guest VMs, the predecessor of MicroV. Unmaintained since 2020.
- [MicroV](https://github.com/Bareflank/MicroV) - Assured Information Security, 2020. Micro-VM hypervisor built on Bareflank. No commits since 2024.
- [GiantVM](https://github.com/GiantVM/giantvm.github.io) - Shanghai Jiao Tong University, 2017. Distributed hypervisor that spans one VM across several hosts.
- [napoca](https://github.com/bitdefender/napoca) - Bitdefender, 2020. Type-1 hypervisor designed to host memory introspection. Archived.
- [Intel HAXM](https://github.com/intel/haxm) - Intel, 2017. VT-x accelerator for QEMU on Windows and macOS. Archived.
- [NEMU](https://github.com/intel/nemu) - Intel, 2018. Stripped-down QEMU fork, superseded by Cloud Hypervisor. Archived.

## Introspection and debugging

### Tools

- [LibVMI](https://github.com/libvmi/libvmi) - The reference VMI library: read and write guest memory and receive hardware events on Xen and KVM.
- [libmicrovmi](https://github.com/Wenzel/libmicrovmi) - Rust library exposing one low-level VMI API across Xen, KVM, VirtualBox and memory dumps.
- [KVM-VMI](https://github.com/KVM-VMI/kvm-vmi) - KVM and QEMU patches that add an introspection API, with setup instructions.
- [DRAKVUF](https://drakvuf.com) - Agentless dynamic malware analysis on Xen using `altp2m` and LibVMI.
- [HVMI](https://github.com/bitdefender/hvmi) - Bitdefender's commercial introspection engine, open-sourced in 2020. Archived.
- [HyperDbg](https://github.com/HyperDbg/HyperDbg) - Hypervisor-based kernel and user-mode debugger for Windows with EPT hooks and scripting.

### Papers and talks

- [A Virtual Machine Introspection Based Architecture for Intrusion Detection](https://www.ndss-symposium.org/ndss2003/virtual-machine-introspection-based-architecture-intrusion-detection/) - Garfinkel and Rosenblum, NDSS 2003. The paper that founded VMI.
- [Hypervisor Memory Forensics](http://www.s3.eurecom.fr/docs/raid13_graziano.pdf) - Graziano, Lanzi and Balzarotti, RAID 2013. Finding hypervisors and nested guests in a physical memory dump. ([slides](http://s3.eurecom.fr/~emdel/talks/grazianolanzi_hitb.pdf))
- [Hypervisor-based, hardware-assisted system monitoring](https://www.youtube.com/watch?v=yTAVS0-qJRU) - Virus Bulletin conference. Monitoring malware from outside the guest with hardware virtualization.
- [Hypervisor-based Memory Introspection at the Next Level](https://www.usenix.org/conference/atc15/technical-session/presentation/lutas) - Lutas et al., USENIX ATC 2015. User-mode memory introspection and protection of live VMs.
- [Zero-Footprint Guest Memory Introspection from Xen](https://www.youtube.com/watch?v=GGjPU6jHi_w) - Mihai Donțu and Ravi Sahita, Xen Project Developer Summit. Agentless introspection with `#VE` and `VMFUNC`. ([slides](https://www.slideshare.net/xen_com_mgr/zero-footprint-guest-memory-introspection-from-xen), [update](http://events17.linuxfoundation.org/sites/events/files/slides/Zero-Footprint%20Guest%20Memory%20Introspection%20with%20Xen.pdf))
- [Virtual Machine Introspection to Detect and Protect](https://www.youtube.com/watch?v=EZPXy314q3E) - Tamas K. Lengyel, Hacktivity. Practical VMI on Xen with LibVMI and DRAKVUF.
- [Bringing Commercial Grade Virtual Machine Introspection to KVM](https://www.youtube.com/watch?v=sUPSogabV-o) - Mihai Donțu, KVM Forum 2017. The design of the KVM introspection API.
- [Who Watches The Watcher? Detecting Hypervisor Introspection from Unprivileged Guests](https://web.archive.org/web/20200724055450/https://dfrws.org/sites/default/files/session-files/paper_who_watches_the_watcher_detecting_hypervisor_introspection_from_unprivileged_guests.pdf) - Tuzel et al., DFRWS 2018. Timing side channels that reveal an introspecting hypervisor.
- [Patchguard: Detection of Hypervisor Based Introspection](https://revers.engineering/patchguard-detection-of-hypervisor-based-instrospection-p1/) - Reverse Engineering blog. How Windows kernel patch protection detects hypervisor hooks. ([part 2](https://revers.engineering/patchguard-detection-of-hypervisor-based-instrospection-p2/))
- [HyperDbg: Reinventing Hardware-Assisted Debugging](https://arxiv.org/abs/2207.05676) - Karvandi et al., CCS 2022. Design of a debugger built on VT-x and EPT rather than OS debugging APIs.
- [The Reversing Machine: Reconstructing Memory Assumptions](https://arxiv.org/abs/2405.00298) - Karvandi et al., 2024. Hypervisor-based memory tracing to defeat anti-analysis techniques.
- [Reversing with HyperDbg (Dbg3301)](https://www.youtube.com/playlist?list=PLUFkSN0XLZ-kF1f143wlw8ujlH2A45nZY) - OpenSecurityTraining2. Free video course on using HyperDbg.

## Security

### Attacking hypervisors

- [The Arms Race Over Virtualization](https://www.youtube.com/watch?v=nWvg7NKwOjg) - Thomas Ptacek, Reflections Projections 2007. Hypervisor rootkits and how to detect them.
- [Lessons Learned from Eight Years of Breaking Hypervisors](https://www.youtube.com/watch?v=PJWJjb0uxXE) - Rafal Wojtczuk, Black Hat Europe 2014. Taxonomy of hypervisor bug classes; the best starting point. ([slides](https://www.blackhat.com/docs/eu-14/materials/eu-14-Wojtczuk-Lessons-Learned-From-Eight-Years-Of-Breaking-Hypervisors.pdf))
- [Attacking Hypervisors Using Firmware And Hardware](https://www.youtube.com/watch?v=nyW3eTobXAI) - Bulygin et al., Black Hat USA 2015. Reaching the hypervisor through firmware interfaces and hardware emulation. ([slides](http://c7zero.info/stuff/AttackingHypervisorsViaFirmware_bhusa15_dc23.pdf))
- [Software Attacks on Hypervisor Emulation of Hardware](https://www.youtube.com/watch?v=c4DnlP88D2Y) - Oleksandr Bazhaniuk, Troopers 2017. Fuzzing CPU and device emulation with CHIPSEC. ([slides](https://www.troopers.de/downloads/troopers17/TR17_Attacking_hypervisor_through_hardwear_emulation.pdf))
- [Glitches in the Matrix - Escape via NMI](https://web.archive.org/web/20220522220504/https://www.cpl0.com/blog/?p=46) - Blog post, with Windows kernel code, on using non-maskable interrupts to escape a hypervisor's control.
- [Hypervisor Vulnerability Research: State of the Art](https://alisa.sh/slides/HypervisorVulnerabilityResearch2020.pdf) - Alisa Esage, 2020. Attack surface and known bug classes of each mainstream hypervisor.

#### KVM

- [Virtualization under attack: Breaking out of KVM](https://www.youtube.com/watch?v=J7TmDGlBqpg) - Nelson Elhage, DEF CON 19, 2011. Full guest-to-host exploit for a QEMU device emulation bug. ([slides](https://media.defcon.org/DEF%20CON%2019/DEF%20CON%2019%20presentations/DEF%20CON%2019%20-%20Elhage-Virtualization-Under-Attack.pdf))
- [Performant Security Hardening of KVM](https://www.youtube.com/watch?v=vj5PA_D03Vg) - Steve Rutherford, KVM Forum 2016. How Google reduces the KVM attack surface in production. ([slides](http://www.linux-kvm.org/images/3/3d/01x02-Steve_Rutherford-Performant_Security_Hardening_of_KVM.pdf))
- [An EPYC escape: Case-study of a KVM breakout](https://projectzero.google/2021/06/an-epyc-escape-case-study-of-kvm.html) - Felix Wilhelm, Project Zero, 2021. Guest-to-host escape through a bug in KVM's own AMD nested virtualization code.

#### Xen

- [Subverting the Xen hypervisor](https://invisiblethingslab.com/resources/bh08/part1.pdf) - Rafal Wojtczuk, Black Hat USA 2008. Modifying the running hypervisor through DMA.
- [Preventing and Detecting Xen Hypervisor Subversions](https://invisiblethingslab.com/resources/bh08/part2.pdf) - Rutkowska and Wojtczuk, Black Hat USA 2008. Defences against the attacks of part one, and their limits.
- [Bluepilling the Xen Hypervisor](https://invisiblethingslab.com/resources/bh08/part3.pdf) - Rutkowska and Tereshkin, Black Hat USA 2008. Nesting a malicious hypervisor underneath Xen.
- [Ouroboros: Tearing Xen Hypervisor With the Snake](https://www.youtube.com/watch?v=kt3kX94kWcM) - Shangcong Luan, Black Hat USA 2016. Exploiting a paravirtualized memory management bug. ([slides](https://www.blackhat.com/docs/us-16/materials/us-16-Luan-Ouroboros-Tearing-Xen-Hypervisor-With-The-Snake.pdf))
- [Xenpwn: Breaking Paravirtualized Devices](https://www.youtube.com/watch?v=qxz8MzE3QME) - Felix Wilhelm, Black Hat USA 2016. Finding double fetches in shared-memory device backends. ([paper](https://www.blackhat.com/docs/us-16/materials/us-16-Wilhelm-Xenpwn-Breaking-Paravirtualized-Devices-wp.pdf))
- [Advanced Exploitation: Xen Hypervisor VM Escape](https://www.youtube.com/watch?v=6Ld5CiInrcI) - Shangcong Luan, HITB Amsterdam 2016. Walk-through of a Xen guest-to-host exploit.
- [Xen exploitation part 1: XSA-105, from nobody to root](https://blog.quarkslab.com/xen-exploitation-part-1-xsa-105-from-nobody-to-root.html) - Quarkslab, 2016. Privilege escalation inside a guest through an instruction emulation bug.
- [Xen exploitation part 2: XSA-148, from guest to host](https://blog.quarkslab.com/xen-exploitation-part-2-xsa-148-from-guest-to-host.html) - Quarkslab, 2016. Full escape through a page table validation bug.
- [Pandavirtualization: Exploiting the Xen hypervisor](https://projectzero.google/2017/04/pandavirtualization-exploiting-xen.html) - Jann Horn, Project Zero, 2017. Exploiting XSA-212 from a paravirtualized guest.

#### VMware

- [Cloudburst: Hacking 3D And Breaking Out Of VMware](https://www.youtube.com/watch?v=NnYNaLSiOxY) - Kostya Kortchinsky, Black Hat USA 2009. Guest-to-host exploit through the virtual GPU.
- [The Great Escapes of VMware](https://www.blackhat.com/docs/eu-17/materials/eu-17-Mandal-The-Great-Escapes-Of-Vmware-A-Retrospective-Case-Study-Of-Vmware-G2H-Escape-Vulnerabilities.pdf) - Mandal and Zhang, Black Hat Europe 2017. Retrospective study of VMware guest-to-host escape vulnerabilities.
- [Out of the Truman Show: VM Escape in VMware Gracefully](https://www.slideshare.net/MSbluehat/bluehat-v17-out-of-the-truman-show-vm-escape-in-vmware-gracefully) - BlueHat v17, 2017. Guest-to-host escape in VMware Workstation.
- [Analyzing a Patch of a Virtual Machine Escape on VMware](https://web.archive.org/web/20180220095129/https://securingtomorrow.mcafee.com/mcafee-labs/analyzing-patch-of-a-virtual-machine-escape-on-vmware/) - McAfee Labs. Patch diffing a fixed escape to locate the bug.
- [A bunch of Red Pills: VMware Escapes](https://keenlab.tencent.com/en/2018/04/23/A-bunch-of-Red-Pills-VMware-Escapes/) - Keen Lab, 2018. The bug chain used against VMware Workstation at Pwn2Own 2017.
- [Wandering through the Shady Corners of VMware Workstation/Fusion](https://web.archive.org/web/20201111232031/https://comsecuris.com/blog/posts/vmware_vgpu_shader_vulnerabilities/) - Comsecuris. Vulnerabilities in the virtual GPU shader translator.
- [Control Register Access Exiting and Crashing VMware](https://howtohypervise.blogspot.com/2018/10/control-register-access-exiting-and.html) - How to Hypervise, 2018. A nested virtualization bug found while writing a hypervisor.
- [VMSA-2025-0004](https://support.broadcom.com/web/ecx/support-content-notification/-/external/content/SecurityAdvisories/0/25390) - Broadcom, 2025. Advisory for the three-bug ESXi escape chain (CVE-2025-22224, 22225, 22226) exploited in the wild.

#### VirtualBox

- [Breaking Out of VirtualBox through 3D Acceleration](https://www.youtube.com/watch?v=i29bAx6W1uI) - Francisco Falcon, REcon 2014. Memory corruption in the Chromium 3D service. ([slides](https://www.coresecurity.com/system/files/publications/2016/05/corelabs-Breaking_Out_of_VirtualBox_through_3D_Acceleration-Francisco_Falcon.pdf))
- [CVE-2017-3558: Guest-to-Host Privilege Escalation via Broken Length Handling in slirp Copy](https://www.exploit-db.com/exploits/41904/) - Jann Horn, Project Zero, 2017. Heap overflow in the NAT networking code, with exploit.
- [Unboxing your VirtualBox](https://www.youtube.com/watch?v=fFaWE3jt7qU) - Niklas Baumstark, Insomni'hack 2018. Attack surface review and exploitation of the 3D and guest services. ([slides](https://raw.githubusercontent.com/phoenhex/files/master/slides/unboxing_your_virtualboxes.pdf))
- [Better slow than sorry - VirtualBox 3D acceleration considered harmful](https://phoenhex.re/2018-07-27/better-slow-than-sorry) - Bugs and an exploit for the 3D acceleration service, by phoenhex, 2018.
- [VirtualBox 3D Acceleration: An Accelerated Attack Surface](https://www.zerodayinitiative.com/blog/2018/8/28/virtualbox-3d-acceleration-an-accelerated-attack-surface) - Zero Day Initiative, 2018. How the Chromium protocol is exposed to guests.
- [CVE-2018-2844: From Compiler Optimization to Code Execution](https://www.voidsecurity.in/2018/08/from-compiler-optimization-to-code.html) - Reno Robert, 2018. A double fetch introduced by the compiler, turned into a VM escape.
- [VirtualBox VMSVGA VM Escape](https://www.voidsecurity.in/2018/11/virtualbox-vmsvga-vm-escape.html) - Reno Robert, 2018. Exploiting the VMware-compatible SVGA device.
- [VirtualBox NAT DHCP/BOOTP server vulnerabilities](https://www.voidsecurity.in/2018/11/virtualbox-nat-dhcpbootp-server.html) - Reno Robert, 2018. Memory disclosure and corruption in the built-in DHCP server.
- [SSD Advisory - Oracle VirtualBox Multiple Guest to Host Escape Vulnerabilities](https://ssd-disclosure.com/ssd-advisory-oracle-virtualbox-multiple-guest-to-host-escape-vulnerabilities/) - SSD Secure Disclosure. Details and proof of concept for several escapes.

#### Hyper-V

- [Security Assessment of Microsoft Hyper-V](https://static.ernw.de/whitepaper/ERNW_Newsletter_43_HyperV_en.pdf) - ERNW, 2014. Early public review of the Hyper-V attack surface.
- [Ring 0 to Ring -1 Exploitation with Hyper-V IPC](https://www.youtube.com/watch?v=_NaRZvrs8xY) - Alex Ionescu, SyScan 2015. Hypercalls and VMBus as an attack surface. ([slides](https://web.archive.org/web/20201109023702/https://alex-ionescu.com/syscan2015.pdf/))
- [VBS and VSM Internals](https://raw.githubusercontent.com/saaramar/Publications/master/BluehatIL_VBS_meetup/VBS_Internals.pdf) - Saar Amar, BlueHat IL, 2018. How the hypervisor enforces virtual trust levels.
- [A Dive in to Hyper-V Architecture & Vulnerabilities](https://github.com/Microsoft/MSRC-Security-Research/blob/master/presentations/2018_08_BlackHatUSA/A%20Dive%20in%20to%20Hyper-V%20Architecture%20and%20Vulnerabilities.pdf) - Joly and Bialek, Black Hat USA 2018. Architecture overview and case studies of fixed bugs.
- [Hardening Hyper-V through offensive security research](https://i.blackhat.com/us-18/Thu-August-9/us-18-Rabet-Hardening-Hyper-V-Through-Offensive-Security-Research.pdf) - Jordan Rabet, Black Hat USA 2018. Exploiting a vmswitch bug and the mitigations that followed.
- [Breaking VSM by Attacking SecureKernel](https://i.blackhat.com/USA-20/Thursday/us-20-Amar-Breaking-VSM-By-Attacking-SecureKernal.pdf) - Amar and King, Black Hat USA 2020. Fuzzing and exploiting the secure kernel from the normal world.

### Fuzzing

- [kAFL](https://github.com/IntelLabs/kAFL) - Coverage-guided fuzzer for kernels, firmware and hypervisors using Intel PT and VM snapshots.
- [Hyper-Cube: High-Dimensional Hypervisor Fuzzing](https://www.ndss-symposium.org/ndss-paper/hyper-cube-high-dimensional-hypervisor-fuzzing/) - Schumilo et al., NDSS 2020. A custom guest OS that fuzzes every hypervisor interface at once.
- [Nyx: Greybox Hypervisor Fuzzing using Fast Snapshots and Affine Types](https://www.usenix.org/conference/usenixsecurity21/presentation/schumilo) - Schumilo et al., USENIX Security 2021. Coverage-guided fuzzing of hypervisors run nested. ([code](https://nyx-fuzz.com/))
- [V-Shuttle: Scalable and Semantics-Aware Hypervisor Virtual Device Fuzzing](https://doi.org/10.1145/3460120.3484811) - Pan et al., CCS 2021. Handles the nested structures that devices read through DMA.
- [Morphuzz: Bending (Input) Space to Fuzz Virtual Devices](https://www.usenix.org/conference/usenixsecurity22/presentation/bulekov) - Bulekov et al., USENIX Security 2022. The generic device fuzzer now part of QEMU.
- [ViDeZZo](https://github.com/HexHive/ViDeZZo) - Liu et al., IEEE S&P 2023. Virtual device fuzzing that models dependencies between messages.
- [HyperPill: Fuzzing for Hypervisor-bugs by Leveraging the Hardware Virtualization Interface](https://www.usenix.org/conference/usenixsecurity24/presentation/bulekov) - Bulekov et al., USENIX Security 2024. Snapshots any x86 hypervisor and fuzzes it through VM exits.
- [hAFL1](https://github.com/SB-GC-Labs/hAFL1) - Hadar and Harpaz, 2021. kAFL-based fuzzer for Hyper-V's vmswitch that found CVE-2021-28476. Unmaintained since 2021.
- [Growing Hypervisor 0day with Hyperseed](https://github.com/microsoft/MSRC-Security-Research/blob/master/presentations/2019_02_OffensiveCon/2019_02%20-%20OffensiveCon%20-%20Growing%20Hypervisor%200day%20with%20Hyperseed.pdf) - King and Denbow, OffensiveCon 2019. Microsoft's internal hypercall fuzzer and the bugs it found.
- [Fuzzing para-virtualized devices in Hyper-V](https://www.microsoft.com/en-us/msrc/blog/2019/01/fuzzing-para-virtualized-devices-in-hyper-v) - MSRC, 2019. Fuzzing VMBus device backends from a guest.
- [Writing a Hyper-V Bridge for Fuzzing](https://www.alex-ionescu.com/writing-a-hyper-v-bridge-for-fuzzing-part-1-wdf/) - Alex Ionescu, 2019. Building a driver that issues arbitrary hypercalls from user mode.

### Confidential VMs

- [AMD Secure Encrypted Virtualization](https://www.amd.com/en/developer/sev.html) - Specifications and white papers for SEV, SEV-ES and SEV-SNP.
- [Intel Trust Domain Extensions](https://www.intel.com/content/www/us/en/developer/tools/trust-domain-extensions/overview.html) - Specifications and documentation for TDX.
- [Arm Confidential Compute Architecture](https://www.arm.com/architecture/security-features/arm-confidential-compute-architecture) - Specifications for realms, the RMM and the Realm Management Extension.
- [COCONUT-SVSM](https://github.com/coconut-svsm/svsm) - Secure VM Service Module in Rust, running at the most privileged level inside an SEV-SNP guest.
- [SEVered: Subverting AMD's Virtual Machine Encryption](https://arxiv.org/abs/1805.09604) - Morbitzer et al., EuroSec 2018. A malicious hypervisor remaps guest pages to extract encrypted memory.
- [CacheWarp](https://cachewarpattack.com/) - Zhang et al., USENIX Security 2024. Software fault injection against SEV-ES and SEV-SNP by reverting guest cache lines.
- [WeSee](https://ahoi-attacks.github.io/wesee/) - Schlüter et al., IEEE S&P 2024. Injecting `#VC` exceptions to read, write and execute inside SEV-SNP guests.
- [Heckler](https://ahoi-attacks.github.io/heckler/) - Schlüter et al., USENIX Security 2024. Injecting interrupts to break SEV-SNP and TDX guests.

### VM detection and malware analysis

- [VMAware](https://github.com/NotRequiem/VMAware) - C++ library and tool implementing a large catalogue of VM detection techniques.
- [al-khaser](https://github.com/ayoubfaouzi/al-khaser) - Proof-of-concept collection of the anti-VM, anti-debug and anti-sandbox tricks used by malware.
- [Reverse Engineering By Crayon: Hypervisor Based Malware Analysis and Visualization](https://www.youtube.com/watch?v=i3I8wtrjYY4) - Quist and Liebrock, DEF CON 17, 2009. Tracing malware from a modified hypervisor.
- [Hypervisors In Ur Toolbox: Monitoring N Controlling System Events With HyperPlatform](https://www.youtube.com/watch?v=oSkP5k0Bkgk) - Satoshi Tanda, Nullcon 2017. Using a thin hypervisor as a malware analysis tool.
- [How to hide a hook: A hypervisor for rootkits](http://phrack.org/issues/69/15.html#article) - Phrack 69, 2016. Hiding kernel hooks with split EPT views.

## Related lists

- [awesome-vm-escape](https://github.com/winmin/awesome-vm-escape) - VM and QEMU escape exploits and write-ups.
- [awesome-hyper-v-exploitation](https://github.com/shogunlab/awesome-hyper-v-exploitation) - Hyper-V exploitation, fuzzing and vulnerability research.
- [awesome-confidential-computing](https://github.com/bpradipt/awesome-confidential-computing) - Confidential computing projects, attestation and the wider ecosystem.
- [awesome-proxmox-ve](https://github.com/Corsinvest/awesome-proxmox-ve) - Proxmox VE documentation and tools.
- [awesome-sandbox](https://github.com/restyler/awesome-sandbox) - Code sandboxing for AI, including microVM-based sandboxes.
