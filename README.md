# Awesome Virtualization [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

A curated list of awesome resources about virtualization.

## Table of Contents

- [Chronology](#chronology)
- [Books](#books)
- [Courses](#courses)
- [Papers](#papers)
- [Research Projects](#research-projects)
- [Mainstream Hypervisors Documentation](#mainstream-hypervisors-documentation)
    - [KVM](#kvm)
    - [Xen](#Xen)
    - [QEMU](#qemu)
    - [VMware](#vmware)
    - [VirtualBox](#virtualbox)
    - [Hyper-V](#hyper-v)
- [Hypervisor Development](#hypervisor-development)
- [Virtual Machine Introspection](#virtual-machine-introspection)
- [Attacking Hypervisors](#attacking-hypervisors)
- [Malware Analysis](#malware-analysis)

## Chronology

- 2005-November-13: Intel `VT-x` released on `Pentium 4` (Model `662` and `672`) processors
- 2006-May-23: AMD `AMD-V` released on `Orleans` and `Windsor` processors
- 2007-September-10 : AMD `Barcelona` offer support for `RVI` (`SLAT`)
- 2008-November: Intel `Nehalem` offer support for `EPT` (`SLAT`)
- 2010-January-7: Intel `Westmere` offer support for `unrestricted guests`
- 2013-June-4: Intel `haswell` offer support for `VMCS Shadowing`

## Books

- [Intel® 64 and IA-32 architectures software developer's manual volume 3C](https://software.intel.com/sites/default/files/managed/7c/f1/326019-sdm-vol-3c.pdf)
- [Virtual Machines: Versatile Platforms for Systems and Processes](https://www.amazon.com/Virtual-Machines-Versatile-Platforms-Architecture/dp/1558609105)
- [Mastering KVM Virtualization](https://www.amazon.com/Mastering-Virtualization-Humble-Devassy-Chirammal/dp/1784399051)

## Courses

- [Memory Virtualization playlist by Udacity](https://www.youtube.com/watch?v=-y9J78wSJHY&list=PLGvfHSgImk4aP4moOrG-KEqVO8gRFh4rb&index=122)
- [Full Virtualization by Geoffrey Challen](https://www.youtube.com/watch?v=2moUsgMOie4)
- [Xen and the Art of Virtualization by Geoffrey Challen](https://www.youtube.com/watch?v=fYH8A3RjPwY)
- [Container Virtualization by Geoffrey Challen](https://www.youtube.com/watch?v=nanHh0t4ssE)
- [Open Security Training Advanced VT-x course](http://opensecuritytraining.info/AdvancedX86-VTX.html)
- [From Kernel to VMM](https://www.youtube.com/watch?v=FSw8Ff1SFLM)

## Papers

- [A comparison of software and hardware techniques for x86 virtualization by K. Adams and O. Agesen (2006)](https://www.vmware.com/pdf/asplos235_adams.pdf)
- [Bringing Virtualization to the x86 Architecture with the Original VMware Workstation by Edouard Bugnion, Scott Devine, Mendel Rosenblum, Jeremy Sugerman, And Edward Y. Wang](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.423.4009&rep=rep1&type=pdf)
- [The evolution of an x86 virtual machine monitor by O. Agesen, A. Garthwaite, J. Sheldon, and P. Subrahmanyam](http://web.mit.edu/6.033/2011/wwwdocs/papers/agesen.pdf)
- [Formal Requirements for Virtualizable Third Generation Architectures by Gerald J. Popek & Robert P. Goldberg](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.141.4815&rep=rep1&type=pdf)
- [Modern Operating System 4th Edition (Chapter: Virtualization and the cloud) by Andrew Tanembaum](https://www.pearson.com/us/higher-education/program/Tanenbaum-Modern-Operating-Systems-4th-Edition/PGM80736.html)
- [Xen and the Art of Virtualization by Paul Barham, Boris Dragovic, Keir Fraser, Steven Hand, Tim Harris, Alex Ho, Rolf Neugebauer, Ian Pratt, Andrew Warfield](http://www.cs.yale.edu/homes/yu-minlan/teach/csci599-fall12/papers/xen.pdf)
- [Understanding Full Virtualization, Paravirtualization and Hardware Assisted Virtualization by VMWare](https://www.vmware.com/techpapers/2007/understanding-full-virtualization-paravirtualizat-1008.html)
- [Dynamic Binary Translation from x86-32 code to x86-64 code for Virtualization by Yu-hsin Chen.](https://dspace.mit.edu/handle/1721.1/53095)
- [MemoryRanger Prevents Hijacking FILE_OBJECT Structures in Windows Kernel by Igor Korkin (2019)](https://igorkorkin.blogspot.com/2019/04/memoryranger-prevents-hijacking.html)

## Research Projects

- 2008: [BitVisor](https://bitbucket.org/bitvisor/bitvisor/)
- 2010: [Xvisor](http://xhypervisor.org/)
- 2011:
    - [ramooflax](https://github.com/airbus-seclab/ramooflax)
    - [TinyVM](https://github.com/jakogut/tinyvm)
- 2013: [jailhouse](https://github.com/siemens/jailhouse)
- 2014: [HOSS](http://www.cs.unc.edu/~porter/hoss/)
- 2015: [Bareflank](https://github.com/Bareflank/hypervisor)
- 2016:
    - [SimpleVisor](https://github.com/ionescu007/SimpleVisor)
    - [HyperPlatform](https://github.com/tandasat/HyperPlatform)
    - [kHypervisor](https://github.com/Kelvinhack/kHypervisor)
    - [rustyvisor](https://github.com/iankronquist/rustyvisor)
    - [HyperBone](https://github.com/DarthTon/HyperBone)
- 2017:
    - [hypervisor-for-beginners](https://github.com/rohaaan/hypervisor-for-beginners)
    - [Intel HAXM](https://github.com/intel/haxm)
    - [ksm](https://github.com/asamy/ksm)
    - [crosvm](https://github.com/dgreid/crosvm)
    - [Firecracker](https://github.com/firecracker-microvm/firecracker)
- 2018:
    - [hvpp](https://github.com/wbenny/hvpp)
    - [ACRN](https://projectacrn.github.io/)
    - [gbhv](https://github.com/Gbps/gbhv)
    - [applepie](https://github.com/gamozolabs/applepie)
    - [boxy](https://github.com/Bareflank/boxy)
    - [nemu](https://github.com/intel/nemu)
    - [gvisor](https://github.com/google/gvisor)
 - 2019:
    - [rust-vmm](https://github.com/rust-vmm/community)
    - [MemoryRanger](https://github.com/IgorKorkin/MemoryRanger)
    - [ZeldaOS.x86_64](https://github.com/chillancezen/ZeldaOS.x86_64)
    - [vbh](https://github.com/intel/vbh)
    - [HypSec](https://www.usenix.org/system/files/sec19-li-shih-wei.pdf)
    - [zpp_hypervisor](https://github.com/eyalz800/zpp_hypervisor)

## Mainstream Hypervisors Documentation

### KVM

- [KVM website](http://www.linux-kvm.org/page/Main_Page)
- [KVM forum](http://www.linux-kvm.org/page/KVM_Forum)
- [set of KVM documentations](http://www.linux-kvm.org/page/Documents)
- [How VT-x, KVM and QEMU Work Together](https://binarydebt.wordpress.com/2018/10/14/intel-virtualisation-how-vt-x-kvm-and-qemu-work-together)

### Xen

- [Xen website](https://www.xenproject.org/)

### QEMU

- [QEMU website](https://www.qemu.org/)

### VMware

- [The Architecture of VMware ESXi](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/techpaper/ESXi_architecture.pdf)

### VirtualBox

- [VirtualBox website](https://www.virtualbox.org/)
- [VirtualBox documentation](https://www.virtualbox.org/wiki/Technical_documentation)

### Hyper-V

- 2015:
    - [Battle of SKM and IUM](http://www.alex-ionescu.com/blackhat2015.pdf)
    - [Ring 0 to Ring -1 Attacks](http://www.alex-ionescu.com/syscan2015.pdf)
- 2017:
    - [Virtualization Based Security - Part 1: The boot process](https://blog.amossys.fr/virtualization-based-security-part1.html)
    - [Virtualization Based Security - Part 2: kernel communications](https://blog.amossys.fr/virtualization-based-security-part2.html)
    - [Hyper-V and its Memory Manager](http://www.andrea-allievi.com/files/Recon_2017_Montreal_HyperV_public.pptx)
- 2018:
    - [A Dive in to Hyper-V Architecture & Vulnerabilities](https://github.com/Microsoft/MSRC-Security-Research/blob/master/presentations/2018_08_BlackHatUSA/A%20Dive%20in%20to%20Hyper-V%20Architecture%20and%20Vulnerabilities.pdf)
    - [Hardening Hyper-V through offensive security research - Black Hat](https://i.blackhat.com/us-18/Thu-August-9/us-18-Rabet-Hardening-Hyper-V-Through-Offensive-Security-Research.pdf)
    - [First Steps in Hyper-V Research](https://msrc-blog.microsoft.com/2018/12/10/first-steps-in-hyper-v-research/)
- 2019:
    - [Growing Hypervisor 0day with Hyperseed](http://paper.vulsee.com/OffensiveCon2019/2019_02%20-%20OffensiveCon%20-%20Growing%20Hypervisor%200day%20with%20Hyperseed.pdf)
    - [VBS and VSM Internals](https://raw.githubusercontent.com/saaramar/Publications/master/BluehatIL_VBS_meetup/VBS_Internals.pdf)


- [Virtualization Documentation](https://docs.microsoft.com/fr-fr/virtualization/)
- [Hyper-V technet](https://technet.microsoft.com/en-us/library/mt169373(v=ws.11).aspx)
- [Hyper-V Internals](http://hvinternals.blogspot.com)


## Hypervisor Development

### Hypervisor From Scratch

- [Part 1: Basic Concepts & Configure Testing Environment](https://rayanfam.com/topics/hypervisor-from-scratch-part-1)
- [Part 2: Entering VMX Operation](https://rayanfam.com/topics/hypervisor-from-scratch-part-2)
- [Part 3: Setting up Our First Virtual Machine](https://rayanfam.com/topics/hypervisor-from-scratch-part-3)
- [Part 4: Address Translation Using Extended Page Table (EPT)](https://rayanfam.com/topics/hypervisor-from-scratch-part-4)
- [Part 5: Setting up VMCS & Running Guest Code](https://rayanfam.com/topics/hypervisor-from-scratch-part-5)
- [Part 6: Virtualizing An Already Running System](https://rayanfam.com/topics/hypervisor-from-scratch-part-6)

### 5 Days to Virtualization

- [Day 0: Virtual Environment Setup, Scripts, and WinDbg ](https://revers.engineering/day-0-virtual-environment-setup-scripts-and-windbg/)
- [Day 1: Introduction to Virtualization, Type Definitions, and Support Testing](https://revers.engineering/day-1-introduction-to-virtualization/)
- [Day 2: Entering VMX Operation, Explaining Implementation Requirements](https://revers.engineering/day-2-entering-vmx-operation/)
- [Day 3: The VMCS, Component Encoding, and Multiprocessor Initialization](https://revers.engineering/day-3-multiprocessor-initialization-error-handling-the-vmcs/)
- [Day 4: VMCS Initialization, Segmentation, and Operation Visualization](https://revers.engineering/day-4-vmcs-segmentation-ops/)
- [Day 5: The VM-exit Handler, Event Injection, Context Modifications, and CPUID Emulation](https://revers.engineering/day-5-vmexits-interrupts-cpuid-emulation/)

## Virtual Machine Introspection

- [Zero-Footprint Guest Memory Introspection from Xen by Mihai Dontu](https://www.youtube.com/watch?v=GGjPU6jHi_w) - [[Slides]](https://www.slideshare.net/xen_com_mgr/zero-footprint-guest-memory-introspection-from-xen) [[Update]](http://events17.linuxfoundation.org/sites/events/files/slides/Zero-Footprint%20Guest%20Memory%20Introspection%20with%20Xen.pdf)
- [Hypervisor memory introspection at the next level](https://www.usenix.org/sites/default/files/conference/protected-files/atc15_slides_lutas.pdf)
- [Bringing Commercial Grade Virtual Machine Introspection to KVM by Mihai Donțu](https://www.youtube.com/watch?v=sUPSogabV-o) - [[Slides]](http://events17.linuxfoundation.org/sites/events/files/slides/Zero-Footprint%20Guest%20Memory%20Introspection%20with%20Xen.pdf)
- [Hypervisor-based, hardware-assisted system monitoring](https://www.youtube.com/watch?v=yTAVS0-qJRU)
- [Virtual Machine Introspection to Detect and Protect](https://www.youtube.com/watch?v=EZPXy314q3E)
- [Hypervisor Memory Forensics](http://www.s3.eurecom.fr/docs/raid13_graziano.pdf) - [[Slides]](http://s3.eurecom.fr/~emdel/talks/grazianolanzi_hitb.pdf)
- [Who Watches The Watcher? Detecting Hypervisor Introspection from Unprivileged Guests](https://dfrws.org/sites/default/files/session-files/paper_who_watches_the_watcher_detecting_hypervisor_introspection_from_unprivileged_guests.pdf)

## Attacking Hypervisors

- [Blackhat 2010 - Hacking the Hypervisor](https://www.youtube.com/watch?v=sTC9x5hYYFo&t=3s)
- [Software Attacks on Hypervisor Emulation of Hardware](https://www.youtube.com/watch?v=c4DnlP88D2Y) - [[Slides]](https://www.troopers.de/downloads/troopers17/TR17_Attacking_hypervisor_through_hardwear_emulation.pdf)
- [Lessons Learned from Eight Years of Breaking Hypervisors](https://www.youtube.com/watch?v=PJWJjb0uxXE) - [[Slides]](https://www.blackhat.com/docs/eu-14/materials/eu-14-Wojtczuk-Lessons-Learned-From-Eight-Years-Of-Breaking-Hypervisors.pdf)
- [Attacking Hypervisors Using Firmware And Hardware](https://www.youtube.com/watch?v=nyW3eTobXAI) - [[Slides]](http://c7zero.info/stuff/AttackingHypervisorsViaFirmware_bhusa15_dc23.pdf)
- [The Arms Race Over Virtualization](https://www.youtube.com/watch?v=nWvg7NKwOjg) - [[Slides]](https://www.blackhat.com/docs/us-16/materials/us-16-Luan-Ouroboros-Tearing-Xen-Hypervisor-With-The-Snake.pdf)

### KVM

- [Virtualization under attack: Breaking out of KVM](https://www.youtube.com/watch?v=J7TmDGlBqpg) - [[Slides]](http://www.hakim.ws/DEFCON19/Speakers/Elhage/DEFCON-19-Elhage-Virtualization-Under-Attack.pdf)
- [Performant Security Hardening of KVM by Steve Rutherford](https://www.youtube.com/watch?v=vj5PA_D03Vg) - [[Slides]](http://www.linux-kvm.org/images/3/3d/01x02-Steve_Rutherford-Performant_Security_Hardening_of_KVM.pdf)

### Xen

- [Ouroboros: Tearing Xen Hypervisor With the Snake](https://www.youtube.com/watch?v=kt3kX94kWcM) 
- [Subverting the Xen hypervisor](https://invisiblethingslab.com/resources/bh08/part1.pdf)
- [Preventing and Detecting Xen Hypervisor Subversions](https://invisiblethingslab.com/resources/bh08/part2.pdf)
- [Bluepilling the Xen Hypervisor](https://invisiblethingslab.com/resources/bh08/part3.pdf)
- [XenPwn: Breaking paravirtualized devices](https://www.youtube.com/watch?v=qxz8MzE3QME) - [[Slide]](https://www.blackhat.com/docs/us-16/materials/us-16-Wilhelm-Xenpwn-Breaking-Paravirtualized-Devices-wp.pdf)
- [Advanced Exploitation: Xen Hypervisor VM Escape ](https://www.youtube.com/watch?v=6Ld5CiInrcI)
- [Xen exploitation part 1: XSA-105, from nobody to root](https://blog.quarkslab.com/xen-exploitation-part-1-xsa-105-from-nobody-to-root.html)
- [Xen exploitation part 2: XSA-148, from guest to host](https://blog.quarkslab.com/xen-exploitation-part-2-xsa-148-from-guest-to-host.html)

### VMware

- [Cloudburst: Hacking 3D And Breaking Out Of Vmware](https://www.youtube.com/watch?v=NnYNaLSiOxY)
- [The Great Escapes Of Vmware: A Retrospective Case Study Of VMWare Guest-To-Host Escape Vulnerabilities](https://www.blackhat.com/docs/eu-17/materials/eu-17-Mandal-The-Great-Escapes-Of-Vmware-A-Retrospective-Case-Study-Of-Vmware-G2H-Escape-Vulnerabilities.pdf)
- [Out of the Truman Show: VM Escape in VMware Gracefully](https://www.slideshare.net/MSbluehat/bluehat-v17-out-of-the-truman-show-vm-escape-in-vmware-gracefully)
- [Control Register Access Exiting and Crashing VMware](https://howtohypervise.blogspot.com/2018/10/control-register-access-exiting-and.html)

### VirtualBox

- [Unboxing your virtualBox](https://www.youtube.com/watch?v=fFaWE3jt7qU) - [[Slides]](https://raw.githubusercontent.com/phoenhex/files/master/slides/unboxing_your_virtualboxes.pdf)
- [Breaking Out of VirtualBox through 3D Acceleration](https://www.youtube.com/watch?v=i29bAx6W1uI) - [[Slides]](https://www.coresecurity.com/system/files/publications/2016/05/corelabs-Breaking_Out_of_VirtualBox_through_3D_Acceleration-Francisco_Falcon.pdf)
- [VirtualBox VMSVGA VM Escape](https://www.voidsecurity.in/2018/11/virtualbox-vmsvga-vm-escape.html)
- [VirtualBox NAT DHCP/BOOTP server vulnerabilities](https://www.voidsecurity.in/2018/11/virtualbox-nat-dhcpbootp-server.html)

### Hyper-V

- [Ring 0 to Ring -1 Exploitation with Hyper-V IPC](https://www.youtube.com/watch?v=_NaRZvrs8xY)
- [Hardening Hyper-V through offensive security research - Black Hat](https://i.blackhat.com/us-18/Thu-August-9/us-18-Rabet-Hardening-Hyper-V-Through-Offensive-Security-Research.pdf)
- [Growing Hypervisor 0day with Hyperseed](http://paper.vulsee.com/OffensiveCon2019/2019_02%20-%20OffensiveCon%20-%20Growing%20Hypervisor%200day%20with%20Hyperseed.pdf)
- [A Dive in to Hyper-V Architecture & Vulnerabilities](https://github.com/Microsoft/MSRC-Security-Research/blob/master/presentations/2018_08_BlackHatUSA/A%20Dive%20in%20to%20Hyper-V%20Architecture%20and%20Vulnerabilities.pdf)
- [Security Assessment of Microsoft Hyper-V](https://static.ernw.de/whitepaper/ERNW_Newsletter_43_HyperV_en.pdf)
- [VBS and VSM Internals](https://raw.githubusercontent.com/saaramar/Publications/master/BluehatIL_VBS_meetup/VBS_Internals.pdf)
- [Fuzzing para-virtualized devices in Hyper-V](https://msrc-blog.microsoft.com/2019/01/28/fuzzing-para-virtualized-devices-in-hyper-v/)
- [Writing a Hyper-V Bridge for Fuzzing](http://www.alex-ionescu.com/?p=377)
- [Awesome Hyper-V Exploitation](https://github.com/shogunlab/awesome-hyper-v-exploitation)

## CVEs

- [Wandering through the Shady Corners of VMware Workstation/Fusion](https://comsecuris.com/blog/posts/vmware_vgpu_shader_vulnerabilities/)
- [CVE-2018-2844: From Compiler Optimization to Code Execution - VirtualBox VM Escape](https://www.voidsecurity.in/2018/08/from-compiler-optimization-to-code.html)
- [CVE-2017-3558: Oracle VM VirtualBox - Guest-to-Host Privilege Escalation via Broken Length Handling in slirp Copy](https://www.exploit-db.com/exploits/41904/)
- [Better slow than sorry - VirtualBox 3D acceleration considered harmful](https://phoenhex.re/2018-07-27/better-slow-than-sorry)
- [Analyzing a Patch of a Virtual Machine Escape on VMware](https://securingtomorrow.mcafee.com/mcafee-labs/analyzing-patch-of-a-virtual-machine-escape-on-vmware/)
- [VirtualBox 3D Acceleration: An Acceleration Attack Surface](https://www.zerodayinitiative.com/blog/2018/8/28/virtualbox-3d-acceleration-an-accelerated-attack-surface)
- [A bunch of Red Pills: VMware Escapes](https://keenlab.tencent.com/en/2018/04/23/A-bunch-of-Red-Pills-VMware-Escapes/)
- [SSD Advisory – Oracle VirtualBox Multiple Guest to Host Escape Vulnerabilities](https://blogs.securiteam.com/index.php/archives/3649)
- [Pandavirtualization: Exploiting the Xen hypervisor](https://googleprojectzero.blogspot.com/2017/04/pandavirtualization-exploiting-xen.html)


## Malware analysis

- [DEFCON 17: Reverse Engineering By Crayon: Hypervisor Based Malware Analysis and Visualization](https://www.youtube.com/watch?v=i3I8wtrjYY4)
- [Hypervisors In Ur Toolbox: Monitoring N Controlling System Events With HyperPlatform](https://www.youtube.com/watch?v=oSkP5k0Bkgk)
- [How to hide a hook: A hypervisor for rootkits](http://phrack.org/issues/69/15.html#article)
