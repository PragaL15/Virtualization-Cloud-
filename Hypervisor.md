# Hypervisors: An Overview

## What is a Hypervisor?
At its core, a **hypervisor** is an arbiter of resources. It is a layer of software that resides between the physical server's hardware and the virtual machines (VMs) running on it. Its primary functions include:
- Resource allocation to virtual machines.
- Providing a virtual environment for workloads.
- Enabling virtual networks for communication between VMs and the external world.
- Offering clustering capabilities for high availability.

Initially, the term **virtual machine monitor (VMM)** was used, but as hypervisors evolved, this term was largely replaced.

---

## Types of Hypervisors
Hypervisors are classified into two categories based on their deployment method:

### Type 1 Hypervisors
- **Definition**: Also known as "bare-metal" hypervisors, they run directly on the server hardware without an underlying operating system.
- **Advantages**:
  - Direct access to hardware resources ensures high efficiency.
  - Improved security as guest failures are contained within the VM.
  - Minimal processing overhead allows more VMs per host.
- **Use Case**: Ideal for dedicated server environments where maximum performance and reliability are essential.
- **Example**: VMware ESXi, Microsoft Hyper-V.

#### Architecture
1. The hypervisor communicates directly with hardware.
2. Guest VMs operate independently, and failures within one VM do not affect others.

---

### Type 2 Hypervisors
- **Definition**: These hypervisors run as applications on top of an existing operating system.
- **Advantages**:
  - Easier to install and deploy due to OS-level support.
  - Wide hardware compatibility inherited from the host OS.
- **Disadvantages**:
  - Additional layers (host OS and hypervisor) increase processing overhead.
  - Less reliable as OS issues (e.g., patches, reboots) affect all hosted VMs.
- **Use Case**: Best for desktop development environments or small-scale testing.
- **Example**: VMware Workstation, Oracle VirtualBox.

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
