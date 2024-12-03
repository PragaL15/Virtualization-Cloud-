# Hypervisors: An Overview

## What is a Hypervisor?
At its core, a **hypervisor** is an arbiter of resources, acting as software that resides between the physical server's hardware and the virtual machines (VMs) running on it. Its primary functions include:

- Resource allocation to virtual machines.
- Providing a virtual environment for workloads.
- Enabling virtual networks for communication between VMs and the external world.
- Offering clustering capabilities for high availability.

The term **virtual machine monitor (VMM)** was originally used, but as hypervisors evolved, this term was replaced.

---

## Types of Hypervisors

### Type 1 Hypervisors
- **Definition**: "Bare-metal" hypervisors that run directly on the server hardware without an underlying operating system.
- **Advantages**:
  - Direct access to hardware resources for high efficiency.
  - Improved security and VM isolation.
  - Minimal processing overhead allows more VMs per host.
- **Use Case**: Ideal for dedicated server environments requiring maximum performance and reliability.
- **Examples**: VMware ESXi, Microsoft Hyper-V.

#### Architecture
1. The hypervisor communicates directly with hardware.
2. Guest VMs operate independently, with failures isolated to individual VMs.

---

### Type 2 Hypervisors
- **Definition**: Hypervisors that run as applications on top of an existing operating system.
- **Advantages**:
  - Easy installation and wide hardware compatibility inherited from the host OS.
- **Disadvantages**:
  - Additional layers (host OS and hypervisor) increase processing overhead.
  - Less reliable, as OS issues (e.g., patches, reboots) affect all hosted VMs.
- **Use Case**: Best for desktop development environments or small-scale testing.
- **Examples**: VMware Workstation, Oracle VirtualBox.

#### Architecture
1. The hypervisor relies on the host OS for hardware interactions.
2. Resource requests from VMs are processed through multiple layers, adding latency.

---

## Key Roles of Hypervisors
Popek and Goldberg defined three critical characteristics for hypervisors:

1. **Environment Simulation**: Provide an environment identical to the physical system.
2. **Efficiency**: Achieve minimal performance cost for operations.
3. **Control**: Retain full control over system resources.

---

## The Importance of Hypervisors
Without a hypervisor, multiple operating systems competing for direct access to hardware would cause conflicts. The hypervisor manages these interactions, ensuring:

- Stability and isolation among VMs.
- Controlled and efficient resource sharing.

Hypervisors revolutionized computing by enabling:

- Virtualization on affordable hardware.
- Efficient use of fast processors and large memory capacities.

---

## The Origin of Virtual Machine Monitors (VMMs)
The original VMM was developed to solve specific problems related to memory management. Over time, VMMs evolved significantly, leading to the term "hypervisor" replacing "virtual machine manager." Modern hypervisors allow:

- Better utilization of faster processors.
- Efficient use of dense memory offerings.

A hypervisor resides **below the virtual machines** and **above the hardware**, managing resource sharing effectively.

---

### Without a Hypervisor
In traditional systems, the operating system directly communicates with hardware (e.g., disks, memory), and multiple operating systems competing for direct access to hardware could cause conflicts. The hypervisor manages these interactions, enabling seamless sharing of physical resources among virtual machines.

---

## Holodecks and Traffic Cops Analogy
To share host physical resources among multiple guests, the hypervisor ensures:

1. Each guest perceives and accesses the necessary hardware resources.
2. The guest OS can interact with disks, memory, and networks seamlessly, facilitated by the hypervisor.
