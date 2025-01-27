- **What is Amazon EC2?**  
  - EC2 stands for **Elastic Compute Cloud**.  
  - A highly popular AWS offering, widely used.  
  - Provides **Infrastructure as a Service** (IaaS) on AWS.  
  - Composed of multiple services at a high level:  
    - **Elastic Compute Cloud (EC2) instances**: Virtual machines.  
    - **Amazon Elastic Block Store (EBS) volumes**: Virtual drives for storing data.  
    - **Elastic Load Balancer (ELB)**: Distributes load across machines.  
    - **Auto-scaling group (ASG)**: Scales services dynamically.  

- **Why learn EC2?**  
  - Fundamental for understanding how the cloud works.  
  - Enables on-demand compute rental.  

- **Choosing EC2 Instances:**  
  - **Operating Systems:**  
    - Linux (most popular), Windows, or MacOS.  
  - **Compute resources:**  
    - CPU cores and RAM.  
  - **Storage:**  
    - **EBS (Elastic Block Store):** Network-attached storage for persistent block-level storage.
    - **EFS (Elastic File System):** Network-attached storage for scalable file storage.
    - **EC2 Instance Store:** Hardware-attached storage for temporary block-level storage.
  - **Network options:**  
    - Network card speed, public IP, and **security groups** (firewall rules).  
  - **Bootstrap script (EC2 User Data):**  
    - Automates tasks at instance launch.  
    - Runs commands (updates, software installation, downloading files) as the root user.

- **EC2 User Data:**  
  - Purpose: Bootstrapping or Automate boot tasks (e.g., updates, software installation).  
  - Bootstrapping means launching commands whenthe machine starts.
  - Runs once during the first boot, with root (sudo) privileges, for example :
    - Install nginx, update packages, etc.
    - Donwload files from internet, etc.
  - Heavier scripts can slow down boot time.  

- **EC2 Instance Types:**  
  - **t2.micro:**  
    - 1 vCPU, 1 GB RAM, EBS storage, low to moderate network performance.  
    - Part of AWS Free Tier (up to 750 hours/month).  
  - **t2.xlarge:**  
    - 4 vCPU, 16 GB RAM, moderate network performance.  
  - **c5d.4xlarge:**  
    - 16 vCPU, 32 GB RAM, 400 NVMe SSD, up to 10 Gbps network performance.  
  - **r5.16xlarge or m5.8xlarge:**  
    - Higher specifications for more demanding applications.  

- **EC2 Keypair:**  
  - A pair of keys used to securely connect to an EC2 instance.  
  - **Public Key:**  
    - Shared with the EC2 instance.  
  - **Private Key:**  
    - Kept secret and used to authenticate the connection.
    - **pem file:**  
      - Used to connect to the EC2 instance (Linux, MacOS, Windows 10+)
    - **ppk file:**
      - Used for windows 7 or 8 (not recommended for new systems)

- ** EC2 Public IP:**  
  - A static IP address that is assigned to an EC2 instance.  
  - Can be used to connect to the EC2 instance from **outside the AWS network**.  
  - Can be changed after the instance is created each time the instance is stopped and started.  
- ** EC2 Privite IP:**  
  - An internal IP address that is assigned to an EC2 instance.  
  - Can be used to connect to the EC2 instance from **within the AWS network**.  
  - Can not be changed after the instance is created or stopped.
- **Notes:**  
  - Choose instances that match your application needs.  
  - EC2 enables scalable, on-demand compute power in the cloud


---

## EC2 Instance Types

There are different types of EC2 instances you can use for various use cases, optimized in different ways. As of now, there are **seven types** of EC2 instances listed on the AWS website. Let’s explore a high-level overview of how they work.

### EC2 Naming Convention
AWS instances follow a standard naming convention. For example, **M5.2xlarge**:
- **M**: Instance Class, representing the type (e.g., General Purpose).
- **5**: Generation of the instance. As AWS updates the hardware, new generations are released (e.g., M6 after M5).
- **2xlarge**: Instance size, starting from small and scaling up (e.g., small → large → 2xlarge → 4xlarge). Larger sizes offer more CPU and memory.

---

### Instance Types and Use Cases

#### 1. **General Purpose**
- **Overview**: These are versatile instances with a good balance of compute, memory, and networking.  
- **Use Cases**:  
  - Web servers.
  - Code repositories.
  - Applications requiring a mix of resources.  
- **Details**:  
  - Ideal for diversity of workloads.  
  - Example: **T2.micro** (Free Tier – up to 750 hours/month).  
  - Families: T2, T3, T4, and M series (e.g., M5, M6).

#### 2. **Compute Optimized**
- **Overview**: These instances are specifically designed for tasks requiring high levels of compute power.  
- **Use Cases**:  
  - Batch processing data.  
  - Media transcoding.  
  - High-performance web servers.  
  - High-Performance Computing (HPC).  
  - Machine learning and dedicated gaming servers.  
- **Details**:  
  - Optimized for compute-intensive tasks.  
  - Families: C series (e.g., C5, C6).

#### 3. **Memory Optimized**
- **Overview**: These instances offer high performance for workloads that process large datasets in memory.  
- **Use Cases**:  
  - Relational and non-relational databases.  
  - In-memory databases like ElasticCache.  
  - Business intelligence (BI) workloads.  
  - Real-time processing of big, unstructured data.  
- **Details**:  
  - Optimized for RAM-intensive applications.  
  - Families: R series (e.g., R5), X1, and Z1.

#### 4. **Storage Optimized**
- **Overview**: These instances are designed for applications requiring high sequential read and write access to large datasets stored locally.  
- **Use Cases**:  
  - High-frequency online transactional processing (OLTP).  
  - Relational and NoSQL databases.  
  - Distributed file systems.  
  - Data warehousing.  
- **Details**:  
  - High storage throughput for data-intensive tasks.  
  - Families: I, G, and H1 series.

---

### Instance Comparison

#### Examples of Instance Types
1. **T2.micro** (General Purpose):  
   - 1 vCPU, 1 GB RAM.  
   - Part of AWS Free Tier (750 hours/month).  
2. **R5.16xlarge** (Memory Optimized):  
   - 16 vCPUs, 512 GB RAM.  
   - High memory for in-memory databases.  
3. **C5d.4xlarge** (Compute Optimized):  
   - 16 vCPUs, 32 GB RAM.  
   - Excellent for compute-intensive tasks.  
4. **I3.2xlarge** (Storage Optimized):  
   - 8 vCPUs, 50 GB RAM.  
   - High storage throughput for data-intensive tasks.  
