# 2025-Timing-Driven-Paritition-Competition-Benchmarks
---

> This repository contains the benchmark cases from the **2025 Timing-Driven Partition Contest** hosted by **Shanghai Fudan Microelectronics Group**.
> 
> 📌 **Contest Specifications:**
> As the original official contest website link is currently inactive, we have provided the original problem description along with an English translation (via DeepL) directly in this repository for the convenience of reviewers and researchers:
> * 🇺🇸 **English Translation:** [`Timing-Driven_Partitioning_Contest_for_Multi-Die_FPGAs_EN.pdf`](./Timing-Driven_Partitioning_Contest_for_Multi-Die_FPGAs_(en-US).pdf)
> * 🇨🇳 **Original Chinese Spec:** [`04_第七届复微杯竞赛题目_FPGA赛道赛题一.pdf`](./04_第七届复微杯竞赛题目_FPGA赛道赛题一.pdf)

#### Benchmark Statistics

There are a total of 5 test cases. The scale and resource statistics for each case are detailed below:

| Case  | #Nodes  | #Nets   | #Pins   | #LUTs   | #FFs   | #CARRYs | #IOs | #BUFs | #RAMs | #DSPs |
| ----- | ------- | ------- | ------- | ------- | ------ | ------- | ---- | ----- | ----- | ----- |
| Case1 | 1571789 | 1574495 | 8781145 | 1420234 | 150321 | 1115    | 61   | 58    | 0     | 0     |
| Case2 | 631054  | 632460  | 2750724 | 495338  | 135039 | 558     | 61   | 58    | 0     | 0     |
| Case3 | 1800863 | 1800606 | 8327024 | 1123280 | 677061 | 0       | 262  | 260   | 0     | 0     |
| Case4 | 1534189 | 1551735 | 7876942 | 701116  | 830850 | 0       | 470  | 462   | 1291  | 0     |
| Case5 | 802556  | 965092  | 5429847 | 620659  | 133159 | 46692   | 330  | 236   | 1480  | 0     |

#### File Structure

Each case is provided as a compressed package (`Casex.zip`) containing the following files: 

```
Casex.zip:
  |--caseName.edif
  |--caseName.xml
  |--caseName.xdc
```

#### File Descriptions

+ **`caseName.edif`**: The design netlist.

  - It can be loaded in **Vivado** using the following Tcl commands:

    ```tcl
    read_edif path_to_edif.edif
    link_design
    ```

+ **`caseName.xml`**: The resource constraint file.

  - This file specifies the number of target **SLRs** (Super Logic Regions) and the resource capacity constraints for each SLR.

+ **`hdl.lib`**: Library file.

  - Provides timing information for each cell type used in the designs.

#### Delay Model

The total net delay is composed of **fixed delay** and **inter-die (crossing) delay**.

##### 1. Fixed Net Delay

The intrinsic delay is calculated based on the net's fanout using the following formula:

$$ \text{Fixed Delay} = \text{Base Delay} + \text{Fanout Based Delay} $$

- **Base Delay:** 0.2 ns
- **Fanout Based Delay Lookup Table:**

| **Fanout Range** | **Delay Added** |
| ---------------- | --------------- |
| **= 1**          | 0.1 ns          |
| **≤ 10**         | 0.2 ns          |
| **≤ 20**         | 0.25 ns         |
| **≤ 30**         | 0.35 ns         |
| **≤ 50**         | 0.55 ns         |
| **≤ 100**        | 0.8 ns          |
| **≤ 200**        | 1.2 ns          |
| **≤ 400**        | 2.0 ns          |
| **> 400**        | 3.0 ns          |

##### 2. Inter-Die Delay

- **Rule:** A penalty of **2 ns** is added for each SLR boundary crossed.

---

> 本仓库包含上海复旦微电子集团举办的 **2025 Timing-Driven Partition Contest** 的 Benchmark 数据。
>
> 📌 **赛题说明文件：**
> 由于官方赛事链接已失效，为方便审稿人及研究者查阅，我们在此直接提供了官方原版赛题说明文件以及对应的英文翻译版（由 DeepL 翻译）：
> * 🇨🇳 **官方中文原版:** [`04_第七届复微杯竞赛题目_FPGA赛道赛题一.pdf`](./04_第七届复微杯竞赛题目_FPGA赛道赛题一.pdf)
> * 🇺🇸 **英文翻译版:** [`Timing-Driven_Partitioning_Contest_for_Multi-Die_FPGAs_EN.pdf`](./Timing-Driven_Partitioning_Contest_for_Multi-Die_FPGAs_EN.pdf)

#### Benchmark规模信息

合计5个case，每个case的规模信息如下表所示：

| Case  | #Nodes  | #Nets   | #Pins   | #LUTs   | #FFs   | #CARRYs | #IOs | #BUFs | #RAMs | #DSPs |
| ----- | ------- | ------- | ------- | ------- | ------ | ------- | ---- | ----- | ----- | ----- |
| Case1 | 1571789 | 1574495 | 8781145 | 1420234 | 150321 | 1115    | 61   | 58    | 0     | 0     |
| Case2 | 631054  | 632460  | 2750724 | 495338  | 135039 | 558     | 61   | 58    | 0     | 0     |
| Case3 | 1800863 | 1800606 | 8327024 | 1123280 | 677061 | 0       | 262  | 260   | 0     | 0     |
| Case4 | 1534189 | 1551735 | 7876942 | 701116  | 830850 | 0       | 470  | 462   | 1291  | 0     |
| Case5 | 802556  | 965092  | 5429847 | 620659  | 133159 | 46692   | 330  | 236   | 1480  | 0     |

#### Benchmark文件组成

每个Case压缩包组成如下：

```
Casex.zip:
  |--caseName.edif
  |--caseName.xml
  |--caseName.xdc
```

+ `caseName.edif` 为网表文件，可以在 Vivado 中使用 `read_edif path_to_edif.edif` 以及 `link_design` 命令打开网表。
+ `caseName.xml` 为资源约束文件，其中指定了需要划分的 SLR 个数以及每个 SLR 内资源容量约束。

提供了`hdl.lib`文件，指定了每种Cell的时序信息

#### 时延计算方法

> Net delay的有固有时延和跨Die时延两部分组成

##### 1. Fixed Net Delay

Net delay的固有时延计算方法如下：

$$ \text{Fixed Delay} = \text{Base Delay} + \text{Fanout Based Delay} $$

+ **其中Base Delay为0.2ns**

+ **Fanout Based Delay查找表**如下：

| **Fanout Range** | **Delay Added** |
| ---------------- | --------------- |
| **= 1**          | 0.1 ns          |
| **≤ 10**         | 0.2 ns          |
| **≤ 20**         | 0.25 ns         |
| **≤ 30**         | 0.35 ns         |
| **≤ 50**         | 0.55 ns         |
| **≤ 100**        | 0.8 ns          |
| **≤ 200**        | 1.2 ns          |
| **≤ 400**        | 2.0 ns          |
| **> 400**        | 3.0 ns          |

##### 2. 跨Die时延

跨Die时延的计算规则是：**每跨越1个SLR则引入2ns时延**

