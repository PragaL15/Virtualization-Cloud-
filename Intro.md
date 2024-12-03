# Virtualization: Transforming Computing Services

We are in the midst of a substantial change in the way computing services are provided. As a consumer, you surf the Web on your cell phone, get directions from a GPS device, and stream movies and music from the cloud. At the heart of these services is **virtualization**—the ability to abstract a physical server into a virtual machine.

In this chapter, you will explore some of the basic concepts of virtualization, review how the need for virtualization came about, and learn why virtualization is a key building block to the future of computing.

## Topics Covered
- Describing virtualization
- Understanding the importance of virtualization
- Understanding virtualization software operation

---

## Describing Virtualization

Over the last 60 years, certain key trends created fundamental changes in how computing services are provided. Mainframe processing drove the 1960s and 1970s. Personal computers, the digitization of the physical desktop, and client/server technology headlined the 1980s and 1990s. The Internet boom and bubble spanned the last and current centuries and continues today.

Today, application and infrastructure services are available via cloud computing. However, we are amidst another model-changing trend: **virtualization**.

Virtualization is a disruptive technology, shattering the status quo of how physical computers are handled, services are delivered, and budgets are allocated. To understand why virtualization has had such a profound effect on today’s computing environment, we need to understand its history.

---

### The Evolution of the Word "Virtual"

The word **virtual** has expanded its usage with the growth of computing, the Internet, and smartphones. Online applications allow us to:
- Shop in **virtual stores**
- Examine vacation spots via **virtual tours**
- Keep **virtual books** in virtual libraries

Similarly, **virtualization in computing** refers to the abstraction of some physical component into a logical object. By virtualizing an object, it is possible to achieve greater utility of its resources. For example:
- **Virtual Local Area Networks (VLANs)** improve network performance by abstracting physical hardware.
- **Storage Area Networks (SANs)** improve storage flexibility by abstracting physical devices.

Our focus is on the **virtualization of entire computers**.

---

### A Brief History of Computer Virtualization

The first mainstream virtualization occurred on IBM mainframes in the 1960s. Gerald J. Popek and Robert P. Goldberg codified the framework for virtualization in their 1974 article, *“Formal Requirements for Virtualizable Third Generation Architectures”*. They defined:
- A **Virtual Machine (VM)** as capable of virtualizing all hardware resources: processors, memory, storage, and network connectivity.
- A **Virtual Machine Monitor (VMM)**, now commonly known as a hypervisor, as the software providing the environment for VMs.

#### Properties of a VMM
1. **Fidelity**: The VM's environment should be identical to the original hardware.
2. **Isolation or Safety**: The VMM must control all system resources.
3. **Performance**: The VM should perform similarly to a physical machine.

Hypervisors and VMs will be explored in depth in later chapters.

---

### Why Virtualization?

The need for virtualization arose from challenges in server-based computing. Initially, **Microsoft Windows**, developed in the 1980s, became the dominant PC operating system. However, businesses relied on incompatible vendor-specific systems, making IT management costly and inefficient.

As hardware became more powerful:
- Businesses shifted applications from mainframes to Windows servers.
- The **“one server, one application”** model emerged to reduce conflicts.
- Departments resisted shared infrastructure, further driving server growth.

This resulted in:
- **Proliferation of servers**: Each application or department required its own servers.
- **High costs**: Both operational and capital expenses soared.
- **Data center limitations**: Space, power, and cooling became critical challenges.

---

## Moore’s Law and Its Impact

**Moore’s Law**, articulated by Gordon Moore of Intel in 1965, states that processing power doubles every 18 months. This exponential growth applies to:
- Processing power
- Memory capacity
- Storage capabilities

Servers replaced every 3–5 years became exponentially more powerful, but workloads did not scale proportionally. This led to **underutilized servers**, with capacities exceeding 90% in some cases.

### Example of Processor Speed Increases
| Year      | Processor Speed | 3-Year Plan | 5-Year Plan |
|-----------|-----------------|-------------|-------------|
| 2023      | 1x              | Purchase    |             |
| 2025      | 4x              | Purchase    |             |
| 2027      | 8x              |             | Purchase    |
| 2028      | 16x             | Purchase    |             |

---

## Data Centers and Their Challenges

As companies expanded, data centers faced challenges:
- **Space limitations**: Many reached their physical limits.
- **Power and cooling constraints**: Existing infrastructure could not scale.
- **Management issues**: “Lost servers” and tangled cabling became common.

The exponential growth of servers strained data centers, making **virtualization** a necessary innovation to improve efficiency and reduce costs.

---
# Virtualization: A Historical Perspective and Evolution

## The Birth of Virtualization

There was a wild explosion of data centers overfilled with servers. Over time, with the combination of Moore’s Law and the “one server, one application” model, these servers performed less work. Fortunately, virtualization emerged as a solution.

Virtualization was not new; it was used on IBM mainframes in the 1960s and later adapted for modern systems. Following Popek and Goldberg’s definition, virtualization enables multiple operating system workloads to run on the same server hardware, keeping each virtual machine isolated.

### Commercial Virtualization Solutions
- VMware introduced the first commercial solution for x86 computers in 2001.
- Open-source virtualization solution Xen followed in 2003.

Virtualization solutions, or **hypervisors**, either sit between an operating system and virtual machines (VMs) or install directly on hardware like traditional operating systems (e.g., Windows, Linux). We’ll explore hypervisors further in the next chapter.

## Benefits of Virtualization

### Server Consolidation
Virtualization allowed multiple physical servers to consolidate into fewer servers running many virtual machines. This significantly increased hardware utilization. 
- **Consolidation ratio**: The number of VMs running on a single server (e.g., 8 VMs = 8:1 ratio).
- Even a modest ratio of 4:1 could remove 75% of servers in a data center, reducing costs associated with hardware, power, and cooling.

### Cost Savings
The total cost of ownership for a server often surpasses its purchase cost by 3–10 times over three years. For example:
- A $5,000 server incurs $20,000 in total costs over three years.
- Consolidating 100 servers could save $2 million annually.

### Containment
As virtualization became widespread, companies stopped purchasing new hardware at lease expiration. Instead, they virtualized workloads on existing infrastructure, further reducing costs and simplifying management.

### Increased Efficiency
Virtualization improved hardware utilization and simplified IT operations. Organizations reclaimed data center space, reduced maintenance costs, and streamlined server management.

## Industry Trends

### Virtual Servers vs. Physical Servers
In 2009, virtual server deployments exceeded physical ones. IDC predicted virtual machine deployments would double physical deployments in five years—a conservative estimate given the rise of cloud computing.

### Key Use Cases
- **Infrastructure services**: File servers, print servers, and domain services often run on older or less reliable hardware.
- **Legacy applications**: Older applications running on obsolete hardware are migrated to virtual environments.

### Adoption Progress
Organizations typically virtualize infrastructure services first. This approach allows for:
- Rapid deployment of test and development environments.
- Consolidation and cost reduction.

By adopting **virtualization-first policies**, companies prioritize virtual resources for new projects unless physical resources are absolutely necessary.

## Advanced Virtualization

### Beyond Infrastructure
As confidence in virtualization grows, companies virtualize:
- **Tier-one applications**: Email, databases, and critical business software.
- **Larger workloads**: High-performance Unix applications migrate to x86 virtual environments.

### Availability and Disaster Recovery
Virtualization enhances system availability:
- **Live migration**: Move VMs between physical hosts without downtime.
- **Resource allocation**: Dynamically add CPUs or memory to VMs without rebooting.
- **Disaster recovery**: Rapidly restore data centers using replicated virtual machine files.

## The Cloud Era

Virtualization laid the foundation for cloud computing by abstracting hardware into scalable, on-demand resources. 
- Cloud computing simplifies application delivery and accelerates deployments.
- Administrators spend less time on routine tasks and more on innovation.

## Hyperconverged Infrastructure

Virtualization reshaped server architecture:
- **Converged infrastructure**: Combines compute, networking, and storage in preconfigured units.
- Introduced in 2009 by Cisco with its Universal Computing System (UCS) blade.
- Solutions by HP, Dell, EMC, and newer entrants like Nutanix optimize virtual desktop hosting and other specialized tasks.

## Conclusion

Virtualization is more than just technology—it transforms how organizations approach infrastructure, cost management, and scalability. It serves as the engine for cloud computing and the future of IT environments.

Virtualization emerged as a solution to address the inefficiencies and challenges posed by traditional server-based computing. By abstracting physical hardware into logical entities, virtualization:
- Improves resource utilization
- Reduces costs
- Paves the way for modern cloud computing and data center operations
