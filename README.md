[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: SONG, Jinzhao
### Student Id: 21076208
### Email: joshuasong42@gmail.com

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > Phoronix-test-suite
    >
    > phoronix-test-suite run pts/compress-7zip
    >
    > This command tests the compression rate of a virtual machine using 7zip.
    >
    > The result is MIPS, meaning millions of instructions per second. The bigger, the better performance the CPU has.
    >
    > phoronix-test-suite run pts/ramspeed
    >
    > This command tests the ram speed of a virtural machine
    >
    > By configuring the method copy integer, this test the RAM's copy performance.
    >
    > The result is MB/s, meaning how many integers(MB) per second can be copied.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` | 3703 MIPS | 10784.09 MB/s |
    | `t2.medium`  | 110040 MIPS | 19681.81 MB/s |
    | `c5d.large` | 7707 MIPS | 14661.12 MB/s |

    > No, it does not increase commensurately(proportionally).
    >
    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` | 4.11 Gbits/sec | 0.155 ms |
    | `m5.large` - `m5.large`   | 4.95 Gbits/sec | 0.179 ms |
    | `c5n.large` - `c5n.large` | 4.95 Gbits/sec | 0.166 ms |
    | `t3.medium` - `c5n.large` | 2.65 Gbits/sec | 0.610 ms |
    | `m5.large` - `c5n.large`  | 4.96 Gbits/sec | 0.169 ms |
    | `m5.large` - `t3.medium`  | 2.15 Gbits/sec | 0.761 ms |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      | 35.0 Mbits/sec | 63.0 ms  |
    | N. Virginia - N. Virginia | 4.97 Gbits/sec | 0.202 ms |
    | Oregon - Oregon           | 8.78 Gbits/sec | 0.108 ms |

    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
