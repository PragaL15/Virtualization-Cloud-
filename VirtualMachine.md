# Virtual Machine

## Analogy: Virtual Reality

Imagine a sophisticated virtual reality (VR) system where the user cannot distinguish between reality and the virtual world. If you were knocked out and woke up inside a holodeck on the Starship Enterprise, you might not realize that you're actually in a virtual environment. In the same way, a **hypervisor** fools a guest operating system into believing that it is directly interacting with the physical devices of the host machine. This process is known as hardware abstraction, and it allows the virtual machines (VMs) to function as if they are running on dedicated physical hardware.

![Abstracting Hardware from the Guests](https://path/to/figure2.6)

In reality, each guest only has access to a fraction of the physical host's resources. For example, while a host may have 256 GB of physical memory, a guest VM might only see 8 GB. Similarly, a guest might believe it has a 250 GB drive, while it is actually working with a portion of a larger storage system. Processing and network resources are also abstracted, with VMs seeing fewer virtual CPUs and network interfaces than the physical host has.

---

## Resource Allocation

A hypervisor acts as an intermediary between the guest operating systems and the physical devices. It not only abstracts the hardware but also balances the workload, ensuring each guest gets the necessary resources in a timely manner. This function can be likened to a traffic cop who manages the flow of vehicles to ensure smooth and equitable access to resources.

---

## Hypervisor as an Operating System

While the hypervisor is not a traditional operating system, it functions similarly by managing resources for virtual servers instead of user applications. For example, when a guest application makes a disk read request, it is handled by the guest operating system and passed to the hypervisor. The hypervisor then translates this request into a real-world I/O operation, passing it to the physical storage system. When the data returns, the hypervisor passes it back to the guest OS, which receives it as if it came from a local disk.

![Processing a Guest I/O](https://path/to/figure2.7)

In this way, the hypervisor manages storage I/O, network I/O, memory, and CPU work for all the guests hosted on the physical server. The hypervisor uses a scheduling process to ensure fair and timely access to these resources, and some hypervisors allow for prioritizing certain guests to ensure critical applications receive preferential treatment.

---

## Configuring Physical Hardware for Virtualization

When designing the physical infrastructure for a virtualized environment, it is essential to ensure that the host server has enough resources to support all the guests it will host. This includes not only the total resources required by the guests but also extra capacity to handle performance spikes, growth, and the hypervisor's own needs.

---

## Comparing Today's Hypervisors

In the early days of computing, there were many operating systems to choose from. Today, virtualization solutions are available from various vendors, each with its own strengths and target use cases. Some solutions, such as Oracle Solaris Zones, BSD Jails in FreeBSD, and IBM PowerVM, allow users to partition a single operating system into multiple secure environments. Others, like Virtuozzo and Docker, virtualize the operating system itself, allowing guests to share the same OS.

For this discussion, we'll focus on **x86 server virtualization**. The market for server virtualization has consolidated significantly, with only a few solutions dominating the space. 

---

## VMware ESX

Founded in 1998, VMware was the first company to develop a commercially available x86 virtualization solution. The company released its first product, **VMware Workstation 1.0**, in 1999, which allowed developers to create and work with virtual machines on Windows or Linux desktops. VMware's solutions have since evolved, making it a leading player in the server virtualization market.
