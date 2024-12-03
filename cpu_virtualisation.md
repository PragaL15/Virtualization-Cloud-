# Understanding CPU Virtualization

Along with memory, network input/output (I/O), and storage I/O, CPUs are some of the main resources used to help size and then determine how well a server is behaving. One of the core properties of virtualization, as defined by Popek and Goldberg, is that there should be little or no difference in the performance between the virtual machine and its physical counterpart. If any one of these resources is suffering contention or is constrained, then the entire performance of that virtual server appears degraded, even though only one of these resources may be bottlenecked. The CPU is the first of these that we will examine.

The first electronic computers were large, covering almost 2,000 square feet of space and weighing almost 30 tons. Most of the machine was directed at supporting the actual processing work—the calculations that provided results. Those initial computers were literally programmed by hand, having wires and patch panels that were reconfigured by an aptly named computer scientist to provide a certain set of calculations. When the program was changed, the wires were unplugged and reconnected in a different arrangement to accommodate the updated calculation set. Today’s microprocessors are both more powerful and faster by orders of magnitude than those room-sized behemoths.

The CPU is the computer inside the computer, and its function is to execute the commands passed to it from the various programs running on the machine. Commands run on the CPU in the form of a relatively small instruction set. These instructions perform bits of work on the data that accompanies the instructions passed to the CPU. The speed at which these instructions execute directly relates to the apparent performance of the CPU, although it would be more accurate to say that performance is more a measure of the number of instructions executed in a certain amount of time rather than the actual number of instructions being executed. If a particular application’s workload requirements cannot execute within a certain amount of time, it appears slow; whether it is because the CPU is older or the application demands more processing time than is available is irrelevant. One solution to this issue is a well-known tradition: throw more hardware at the problem by adding a second CPU. There are other strategies to handle this—for example, hyperthreading, which we’ll cover shortly, and resource pooling, which we’ll cover in Chapter 14, “Understanding Applications in a Virtual Machine.”

In the context of virtualization, the question is, “How do you virtualize a CPU?” The short answer is, most times you don’t. There are virtualization solutions that attempt to emulate the CPU itself, but emulation often suffers from performance and scalability issues because large amounts of processing overhead are devoted to the effort. Instead, the hypervisor schedules slices of time on the available processors in the physical host server for the virtual instructions to run. 

## Virtual Machines using a Host CPU

If each virtual machine had only one virtual CPU and each physical server had only one physical processor, the model would be that simple. Of course, reality is much more complex. The first wrinkle is that most servers today are configured with more than one processor. That does not greatly affect this model aside from providing additional resources in the form of CPU time that can be allocated by the hypervisor. The next change is that most of today’s modern CPUs contain more than one processor in their makeup. Each of these processors in the CPU is called a core, and even today’s personal computers have multicore CPUs.

| # of Processors | Single Core | Dual Core | Quad Core |
|-----------------|-------------|-----------|-----------|
| 1               | 1           | 2         | 4         |
| 2               | 2           | 4         | 8         |
| 4               | 4           | 8         | 16        |
| 8               | 8           | 16        | 32        |

To distinguish between physical server CPUs and virtual machine CPUs, we’ll refer to the latter as vCPUs. What happens when you add vCPUs to virtual machines? If you have a virtual machine with two vCPUs, the hypervisor will need to schedule work on two physical CPUs. That means two physical CPUs would need to be available at the same time for the work to be performed. 

When you plan for how many virtual machines can fit on a host, one of the criteria is the number of vCPUs and physical CPUs. In this simple model, with four unicore physical CPUs on the host, you actually can allocate more than four vCPUs for the guests because individual guests don’t monopolize a physical CPU. If they did, you would need to assign them additional vCPUs.

### Configuring VM CPU Options

In the case of virtual CPUs, there are few items that you can adjust to affect the virtual machine’s performance. In fact, as part of the virtual machine, there is really only one parameter that you can adjust: the actual number of vCPUs.

To examine or change the number of processors in your virtual machine, you can perform the following steps:

1. Select Virtual Machine from the VMware Player menu bar.
2. Select Manage ➣ Virtual Machine Settings from the menu or Edit Virtual Machine Settings in the virtual machine window.
3. Select the Processors line on the left side of the screen in the Hardware window to display the Processor options.
4. By selecting the Number of Processor Cores drop-down menu, you can choose up to 32 vCPUs for your virtual machine.

### Tuning Practices for VM CPUs

Although a CPU is one of the core resources for correctly sizing and managing virtual machine performance, it is also the one with the fewest number of moving parts when it comes to tuning. Essentially, you can affect the number of vCPUs that you allocate to a virtual machine, and you have some ability to control how those vCPUs are seen by the virtual machine. Aside from that, there are few factors on the physical server that are changeable that affect how well the virtual machines perform.

#### Choosing Multiple vCPUs vs. a Single vCPU

When you’re building a virtual machine, one of your initial configuration choices is the number of virtual CPUs that will be allocated to the VM. The choice would seem to be fairly simple, either one or more than one, but this is one of the largest areas of discussion when it comes to virtual machine performance. As with physical servers, having multiple CPUs in virtual machines would provide more CPU resources to utilize; but as you have seen, having additional vCPUs can actually hinder performance because the additional vCPUs need to be scheduled simultaneously, which is not always possible on a busy system.

Before workloads are migrated to virtual infrastructures, a number of different performance tools can be run to determine a baseline of expected CPU performance. It’s best to begin with a single vCPU and then adjust upward if circumstances demand it, rather than to start with many and work downward.

# Hyperthreading

Hyperthreading is an Intel microprocessor technology that improves performance by making more efficient use of the processor scheduling. Prior to hyperthreading technology, only one set of instructions could be executed on a processor at a time. For each physical processor, hyperthreading presents two logical processors. Each logical processor can process an individual thread of work, so for each physical core, two threads of work can be scheduled. Hyperthreading doesn’t double the capability of a processor, but it might provide an additional 30 percent efficiency under the right circumstances.

A few prerequisites are required for hyperthreading to work. First, the processor must be an Intel microprocessor that is capable of hyperthreading. The operating system must support multiple processors, and it must be capable of supporting hyperthreading. Windows and Linux support hyperthreading, as do most hypervisors. This means that a hypervisor can schedule two threads of work on each physical processor or core on the physical server. 

Let’s check your system to see if hyperthreading is enabled:
1. From the Windows search box, enter **Task Manager**.
2. Select the **Task Manager** to open the application.
3. Click **More Details** on the bottom taskbar.
4. Choose the **Performance** tab at the top of the application.
5. As shown in Figure 7.3, if it isn’t already highlighted, select the **CPU** graph on the left panel.


In Figure 7.4, just below the performance graph, you can see that the example system contains two processor cores and four logical processors, which translates back to two threads per core. Hyperthreading is enabled on the physical system.


## Working with Intel and AMD Servers

When it comes to virtualization, questions often arise regarding which x86 chipset is best for performance. At present, the best answer is that no x86 chipset is particularly better than another. As a proof point, companies are not making hardware decisions based on the chipset in the server. Companies refresh their server hardware and improve the platforms on which they run either through a consolidation effort as they move to a virtualized environment or by replacing their virtualized environment. Sometimes these upgrades involve switching to a vendor that uses a different x86 microprocessor—for example, when going from Intel to AMD. From a performance standpoint, typically there is not that much fluctuation in CPU performance, but there is a potential change in operational performance.

Hypervisors will run just as well on either an AMD or Intel platform; in fact, there is no way to discern what chip you are running on from an operational standpoint. However, issues can arise when you are working in a mixed environment, supporting both Intel-based and AMD-based servers. 

In Chapter 13, “Understanding Availability,” you’ll learn about clustering hosts for increased performance and availability. For now, you just need to know that one feature of clustering is the ability to migrate a virtual machine from one physical server to another, while the virtual machine is still running, without interrupting the application on that virtual machine. This capability is used for dynamically load balancing virtual machines across a number of physical hosts and for evacuating a physical host so that maintenance can be done. 

This is true for a cluster made up of physical servers that share the same vendor microprocessor. In a mixed environment, the instruction sets of the different microprocessors are not identical, so you cannot live-migrate the virtual machines from an AMD host to an Intel host, or vice versa. To move a virtual machine from an AMD host to an Intel host, or the reverse, you need to shut down that virtual machine, and then you can restart it on the second host with the different chipset.
