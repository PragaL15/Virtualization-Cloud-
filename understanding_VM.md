# Understanding Virtual Machines

Virtual machines are the fundamental components of virtualization. They are the containers for traditional operating systems and applications that run on top of a hypervisor on a physical server. Inside a virtual machine, things seem very much like the inside of a physical server—but outside, things are very different. In this chapter, we will examine these differences, focus on how virtual machines work in relation to the physical machines they reside on, and take the initial steps in understanding how virtual machines are managed.

- Describing a virtual machine
- Understanding how a virtual machine works
- Working with virtual machines

## Describing a Virtual Machine

A virtual machine, also referred to as a VM, has many of the same characteristics as a physical server. Like an actual server, a VM supports an operating system and is configured with a set of resources to which the applications running on the VM can request access. Unlike a physical server (where only one operating system runs at any one time and few, usually related, applications run), many VMs can run simultaneously inside a single physical server, and these VMs can also run many different operating systems supporting many different applications. Also, unlike a physical server, a VM is in actuality nothing more than a set of files that describe and comprise the virtual server.

The main files that make up a VM are the configuration file and the virtual disk files. The configuration file describes the resources that the VM can utilize: it enumerates the virtual hardware that makes up that particular VM. Figure 3.1 is a simplified illustration of a virtual machine. If you think of a virtual machine as an empty server chassis, the configuration file lists which hardware devices would be in that chassis: CPU, memory, storage, networking, CD drive, etc. In fact, as you will see when we build a new virtual machine, it is exactly like a new physical server just off the factory line—some (virtual) iron waiting for software to give it direction and purpose. In Chapter 4, “Creating a Virtual Machine,” we will do exactly that.


Virtual machines have access to various hardware resources, but from their point of view, they don’t know that these devices don’t actually exist. They access virtual devices, software constructs that represent physical resources abstracted by the hypervisor. The virtual devices they deal with are standard devices—in other words, they are the same within each virtual machine, which makes them portable across various hardware platforms, virtualization solutions, or vendor solutions, as you will see later in the chapter.

In a virtual machine, as in a physical machine, you can configure various types and amounts of peripheral devices. The bulk of this text will cover how to configure and manage these devices. But the real key to understanding virtual machines is to understand that there are two different views of a VM: one from the inside and one from the outside.

### Inside vs. Outside the Virtual Machine

From outside the virtual machine, what you can see is the composition and configuration of the host server. Whether it is a laptop PC running VMware Fusion, Parallels Desktop, or VMware Workstation or it’s a full-fledged enterprise-class server from Dell, HP, IBM, or Cisco running VMware vSphere or Microsoft Hyper-V, the resources to which you have access are all of the system devices.

From inside a virtual machine, the view is identical to being inside a physical machine. From the operating system’s point of view or an application’s point of view, storage, memory, network, and processing are all available for the asking. If you are running Windows and open up the various Control Panel utilities to examine your system, you will find very little that would make you think twice.

Storage devices, C: drives, D: drives, etc., are where they should be; network connections are visible and functional; and system services are running. There is some amount of memory in the server along with one or more CPUs, possibly a CD drive, monitor, and keyboard. Everything looks just as it ought to, until you dig down and look at Windows Device Manager, as shown in Figure 3.2.


Here you can see where real and virtual begin to diverge. Examining the network adapter and the storage adapter reveals industry-standard devices. The display adapter is not the same as your actual monitor. It is created as a standard device driver to be used with any monitor. The disk drives and the DVD/CD drives also use specialized virtual drivers. What happens is that the hypervisor underneath presents the virtual machines with generic resources to which they connect. These specialized device drivers, which we’ll examine closer in Chapter 5, “Installing Windows on a Virtual Machine,” are added later to help optimize that connection.

## Examining CPUs in a Virtual Machine

Virtual machines are configured to run with one or more processors, depending on the anticipated demand on the system. In the simplest case, a VM will have one CPU, and, as you saw earlier, if you examine the hardware from the VM’s standpoint, you will see that only one CPU is available. From the host’s standpoint, what has been assigned is the virtual machine’s ability to schedule CPU cycles on the host’s available CPUs. In this case, illustrated in Figure 3.3, the single CPU VM can schedule a single CPU’s worth of capacity. The host does not reserve a CPU solely for the use of a particular VM; instead, when the VM needs processing resources, the hypervisor takes the request, schedules the operations, and passes the results back to the VM through the appropriate device driver.


It is important to remember that usually the host has many more CPUs available than any one VM; in addition, the hypervisor is scheduling time on those processors on behalf of the VMs, rather than a VM actually having a dedicated CPU. One of the main reasons for virtualization in the first place was to gain more efficient use of the resources through consolidation, and a dedicated CPU would defeat that purpose. On another quick note, most servers today have multiple-socket CPUs, and each one of those sockets contains one or more cores. For our purposes, a VM looks at a core as a single virtual CPU.

## Examining Memory in a Virtual Machine

Random-access memory (RAM), or memory resources, is probably the simplest to understand in the virtual environment. Just as in a physical machine, having enough memory resources in a virtual machine is often the difference between success and failure when evaluating an application’s performance. As digital consumers, we are all aware of the value of adequate memory resources, whether it be for our smartphones, tablets, laptops, or other personal electronic devices.

More memory is usually better, but there is a fine balance between enough memory and too much memory in a shared virtual environment. As with CPU utilization, hypervisor vendors have added sophisticated memory management techniques to obtain the best use from the available physical memory. As shown in Figure 3.4, a virtual machine is allocated a specific amount of memory, and that is all that it can utilize, even though there might be orders of magnitude more memory available on the physical machine.


Unlike physical machines, when a virtual machine requires more memory, you can merely reconfigure the amount, and the VM will have access to the added capacity, sometimes without even needing a reboot. You will learn more about managing and configuring memory resources in Chapter 8, “Managing Memory for a Virtual Machine.”

## Examining Network Resources in a Virtual Machine

Like its physical counterpart, virtual networking provides a VM with a way to communicate with the outside world. Each virtual machine can be configured with one or more network interface cards (NICs) that represent a connection to a network. These virtual NIC cards, however, don’t connect with the physical NIC cards in the host system. The hypervisor supports the creation of a virtual network that connects the virtual NICs to a network that is composed of virtual switches. It is this virtual network that the physical NICs connect to, as shown in Figure 3.5.


This virtual network is also a vital tool in creating secure environments for the virtual machines that share a host. From a security standpoint, VM-to-VM communications can occur across a virtual switch and never leave the physical host. If a second VM’s virtual NIC connects to a virtual switch and that switch is not connected to a physical NIC, the only way to communicate with that VM is through the first VM, building a protective buffer between the outside world and that VM.

## Examining Storage in a Virtual Machine

Virtual servers need storage to work with, and like the resources you’ve seen so far, what gets presented to the virtual machine and what the virtual machine believes it is seeing are very different. As shown in Figure 3.7, a virtual machine running Windows will see a C: drive, a D: drive, and maybe many others. In actuality, those “drives” are merely carved-out regions of disk space on a shared storage device, and the hypervisor manages the presentation to the VM.


As the virtual machine talks to a virtual SCSI disk adapter, the hypervisor passes data blocks to and from the physical storage. That actual connection, from the host to the storage, whether it is local storage on the host or on a storage area network (SAN), is abstracted from the virtual machines.


Virtual machines usually don’t have to worry about whether they are connected to their storage resources via Fibre Channel, iSCSI, or the Network File System (NFS) protocol because that is configured and managed at the host. You will learn more about managing and configuring storage resources in Chapter 9, “Managing Storage for a Virtual Machine.”

## Examining Virtual Machine Disk Files

A virtual disk, sometimes called a virtual hard disk, is the file or set of files that represent the storage for a virtual machine. For example, a virtual machine that uses VMware Workstation or VMware vSphere might use a .vmdk file for its virtual disk.

The hypervisor will access these files as though they are physical disks and will present them to the VM as virtual devices. The operating system inside the virtual machine will treat these devices like any other disk, and the application running inside the VM will write to them as it would to a hard disk.

These virtual disks can be stored in one of two ways:

- **Monolithic disk** – A single file, typically used with VMware Workstation or VMware Fusion
- **Split disk** – Several files that make up the disk, typically used with VMware vSphere

The size of the virtual disk is set when the virtual machine is created, but it is not necessarily the same size as the file that represents the virtual disk. You can configure the size of the virtual disk to grow or shrink dynamically as data is written to it or if you manually adjust it. As you will see later, the use of thin or thick provisioning can impact the size of the virtual disk.

# Working with Virtual Machines

Virtual machines exist as two physical entities: the files that make up the configuration of the virtual machines and the instantiation in memory that makes up a running VM once it has been started. In many ways, working with a running virtual machine is similar to working with an actual physical server. Like a physical server, you can interact with it through some type of network connection to load, manage, and monitor the environment or the various applications that the server supports. Also like a physical server, you can modify the hardware configuration, adding or subtracting capability and capacity, though the methods for doing that and the flexibility for doing that are very different between a physical server and a virtual machine.

We’ll defer the “working with a running VM” discussion until Chapter 4 and focus for now on understanding why the fact that VMs exist as data files is a key enabler in managing and maintaining them. Since the inception of the computer, data files have been the method of storing information. Because of that history and knowledge, managing files is routine. If someone needs to move a spreadsheet from one place to another, they move the file. If they need to back up a document, they copy that file and move the copy to another device for archiving. If someone builds a presentation that will serve as a base for many other presentations, they write-lock that presentation and allow other people to duplicate it for their use. By leveraging these same file properties, you can do some remarkable things with virtual machines.

## Understanding Virtual Machine Clones

Server provisioning takes considerable resources in terms of time, manpower, and money. Before server virtualization, the process of ordering and acquiring a physical server could take weeks, or even months in certain organizations, not to mention the cost, which often would be thousands of dollars. Once the server physically arrived, additional provisioning time was required. A server administrator would need to perform a long list of chores, including loading an operating system, loading whatever other patches that operating system needed to be up-to-date, configuring additional storage, installing whatever corporate tools and applications the organization decided were crucial to managing its infrastructure, acquiring network information, and connecting the server to the network infrastructure. Finally, the server could be handed off to an application team to install and configure the actual application that would be run on the server. The additional provisioning time could be days, or longer, depending on the complexity of what needed to be installed and what organizational mechanisms were in place to complete the process.

Contrast this with a virtual machine. If you need a new server, you can clone an existing one, as shown in Figure 3.11. The process involves little more than copying the files that make up the existing server. Once that copy exists, the guest operating system only needs some customization in the form of unique system information, such as a system name and IP address, before it can be instantiated. Without those changes, two VMs with the same identity would be running in the network and application space, and that would wreak havoc on many levels. Tools that manage virtual machines have provisions built in to help with the customizations during cloning, which can make the actual effort itself nothing more than a few mouse clicks.

Although it may take only a few moments to request the clone, it will take some time to enact the copy of the files and the guest customization. Depending on a number of factors, it might take minutes or even hours. But, if we contrast this process with the provisioning of a physical server, which takes weeks or longer to acquire and set up, a virtual machine can be built, configured, and provided in mere minutes, at a considerable savings in both work hours and cost. We’ll work more with VM clones in Chapter 11, “Copying a Virtual Machine.”



## Understanding Templates

Similar to clones, virtual machine templates are another mechanism to rapidly deliver fully configured virtual servers. A template is a mold, a preconfigured, preloaded virtual machine that is used to stamp out copies of a commonly used server. Figure 3.12 shows the Enable Template Mode check box to enable this capability. The difference between a template and a clone is that the clone is running and a template is not. In most environments, a template cannot run, and to make changes to it (applying patches, for example), a template must first be converted back to a virtual machine. You would then start the virtual machine, apply the necessary patches, shut down the virtual machine, and then convert the VM back to a template. Like cloning, creating a VM from a template also requires a unique identity to be applied to the newly created virtual machine. As in cloning, the time to create a virtual machine from a template is orders of magnitude quicker than building and provisioning a new physical server. Unlike a clone, when a VM is converted to a template, the VM it is created from is gone.


Templates are used to do more than just deliver “empty” virtual machines, servers that are composed of the configured virtual machine with an operating system installed; they can deliver VMs that have applications installed and configured as well. When users need their programs to be loaded, a VM created from a prebuilt template can deliver that application or suite of applications to users, ready for immediate use. In fact, many application vendors are beginning to deliver those applications in the form of virtual machine templates that can be downloaded and then deployed in a minimum amount of time. We will look more closely at templates in Chapter 11.

## Understanding Snapshots

Snapshots are pretty much just what they sound like, a capturing of a VM’s state at a particular point in time. They provide a stake in the ground that you can easily return to in the event that some change made to the VM caused a problem you’d like to undo. If you have ever played any adventure games, the concept of a save point is analogous to a snapshot. Figure 3.13 is a basic illustration of how snapshots work. A snapshot preserves the state of a VM, its data, and its hardware configuration. Once you snapshot a VM, changes that are made no longer go to the virtual machine disk. They go instead to a delta disk, sometimes called a child disk. This delta disk accumulates all changes until one of two things happens: another snapshot or a consolidation, ending the snapshot process. If another snapshot is taken, a second delta disk is created, and all subsequent changes are written there. If a consolidation is done, the delta disk changes are merged with the base virtual machine files and become the updated VM. Finally, you can revert to the state of a VM at the time when a snapshot was taken, unrolling all of the changes that have been made since that time.

![Snapshot disk chain](image-placeholder.jpg)

Snapshots are useful in test and development areas, allowing developers to try riskier or unknown processes with the ability to restore their environment to a known healthy state. Snapshots can be used to test a patch or an update where the outcome is unsure, and they provide an easy way to undo what was applied. Snapshots are not a substitute for proper backups. Applying multiple snapshots to a VM is fine for a test environment but can cause large headaches and performance issues in a production system. We’ll work more closely with snapshots in Chapter 11.

## Understanding OVF

Another way to package and distribute virtual machines is using the Open Virtualization Format (OVF). OVF is a standard created by an industry-wide group of people representing key vendors in the various areas of virtualization. The purpose of the standard is to create a platform and vendor-neutral format to bundle up virtual machines into one or more files that can be easily transported from one virtualization platform to another. Put another way, this offers a way to create a VM on a Xen-based system, export it to the neutral OVF standard, and then import it into a VMware or Hyper-V environment. Most virtualization vendors have options to export virtual machines to the OVF format, as well as have the ability to import OVF-formatted VMs into their own formats.

The OVF standard supports two different methods for packaging virtual machines. The OVF template creates a number of files that represent the virtual machine, much as the virtual machine itself is composed of a number of files. The OVF standard also supports a second format, OVA, which will encapsulate all of the information in a single file. In fact, the standard states, “An OVF package may be stored as a single file using the TAR format. The extension of that file shall be .ova (open virtual appliance or application).”

## Understanding Containers

While containers are not virtual machines, they are close enough in functionality and prevalent enough in application development and business computing that they are worth including here. Like virtual machines, containers offer a platform-independent package to bundle, deliver, and deploy applications. Unlike virtual machines, containers do their abstraction at the operating system level, rather than the hardware level. This means containers can wrap up multiple workloads in a single receptacle, usually supporting a single application.

Although containers do provide great portability and lower resource overhead than virtual machine infrastructure, they do have some limitations. The container model, because it abstracts at the operating system level, has a limitation that all of the workloads in a container must run the same operating system or kernel where a hypervisor can support virtual machines or various operating systems side-by-side. The isolation between workloads in a container is also not nearly as robust as what hypervisors and virtual machines provide.

In certain use cases, containers can offer more rapid deployment and lower overhead than virtual machines. The most popular open-source container technology is Docker (www.docker.com). Working with other like-minded companies, Docker has done a lot to develop standardization within containers in addition to providing numerous other tools and related management technologies to legitimize containers as a mainstream solution.

Much the way virtual machines and virtualization disrupted traditional computing, container technologies are disrupting virtualization.


## Summary

A virtual machine is a simulated server that runs on top of a hypervisor. It has all the elements of a physical machine, including CPU, memory, storage, network, and peripheral devices. From the inside, a VM appears like a traditional machine running an operating system, but the hardware it uses is virtualized by the hypervisor. Understanding how these components work and how they differ from physical servers is key to managing and configuring virtual machines.
