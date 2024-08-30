# Characterization and Modeling of GaN HEMTs

<center>Tianyang (Eliot) Chen | Advisor: Patrick Fay | 2024 Summer</center>

> *Click the hyperlink in the table of contents to navigate to the corresponding section.*

[TOC]

## ==Introduction==

### ==Overview==

#### ==About this Work==

这一部分将概述本次暑期科研的工作

#### ==About this Documents==

这一部分将介绍本文件的主要内容和outline思维导图

#### ==Updates and Releases==

这一部分将包含本次项目文件的下载方式和更新渠道



### ==Gallium Nitride (GaN) High-Electron-Mobility Transistors (HEMTs)==

#### ==Concepts==

这一部分将结合文献调研介绍氮化镓高电子迁移率三极管的基本概念和结构

#### ==Modeling Techniques==

这一部分将主要介绍目前市面上常见的三种针对GaN HEMT的建模方式，并且分析其优缺点。
这一部分说明了为什么我们需要在本次项目中采用Angelov GaN模型。

- **Physics Based Models:**

- **ANN Based Models:**

- **Empirical Models:**



### ==Angelov Model==

#### ==A Review==

这一部分将介绍本次文献调研的基本情况，着重介绍提出Angelov模型的论文，并介绍这一模型的逐渐发展—最终成为商业simulator的常用模型的过程。

#### ==Angelov GaN Model==

这一部分将介绍本次模型中所采用的Angelov GaN模型。本次项目基于keysight发行的GaN HEMT model进行仿真。



### ==Integrated Circuit Characterization and Analysis Program (IC-CAP)==

IC-CAP一个由Keysight Technologies开发的软件，用于半导体器件的建模和特性分析。

#### ==Designed Workflow==

这一部分介绍本次的Modeling Package，以及软件自身包含的整个提取项目的workflow。



[Back to Table of Contents](# Characterization and Modeling of GaN HEMTs)

<div STYLE="page-break-after: always;"></div>

## ==Characterization==

这一部分将讲述如何进行基于测量的Characterization，我将会详细介绍如何针对我们的器件来进行设置，介绍如何根据器件的基本信息设置具体的测试流程，并在尽可能确保器件安全的前提下完成测量。

### ==Settings==

#### ==Device Settings==

这一部分将介绍如何基于器件的基本结构对于项目进行设置。

#### ==Instrument Setting==

这一部分将介绍本次实验选用的测量仪器，并介绍如何通过IC-CAP与仪器进行通信。



### ==Measurement Flow Design==

#### ==Measurement Setting==

这一部分将介绍如何对测试的基本信息进行设置，包含了对校准的设置、对测量限制的设置、和对于提取频率的设置。

#### ==Pad Open/Short==

这一部分介绍了对于Open和Short Pad的测量，这一步将被应用于De-embed计算。

#### ==DC Setups==

这一部分介绍DC测量的一系列setups，并基于本次的测量说明测量设计的思路。

#### ==RF Setups==

这一部分介绍DC测量的一系列setups，并基于本次的测量说明测量设计的思路。



### ==Measurements with Risk Managements==

这一部分将介绍如何利用上述构建出的程序，对于器件开展测量。

> 测量的过程就像是人生，最安全的方式是待在家里永远不出去，但是这样我们不会有任何收获。

在测试器件的过程中，我们难免会施加一些相对严格的条件，这是一个高风险高回报的过程。当然，我们可以进行风险和收益的trade off，从而在更安全的范围内得到更有效的数据。

#### ==Instrument Setups==

这一部分将介绍仪器和测试端口的连接。

#### ==Measurement Settings==

这一步将介绍对测试的设置，主要是RF测试的校准。

#### ==Pad Open/Short and De-Embed Calculations==

这一步将介绍对于Pad测量的基本情况。

#### ==Measure DC==

这一步将介绍如何运行DC测量的setup，并根据结果调整测量参数。

#### ==Measure RF==

这一步将介绍如何运行RF测量的setup，并根据结果调整测量参数。



[Back to Table of Contents](# Characterization and Modeling of GaN HEMTs)

<div STYLE="page-break-after: always;"></div>

## ==Modeling==

### ==Angelov GaN Parameters==

#### All Parameters

使用 Angelov GaN 进行建模，我们需要提取一系列参数。
对于simulator来说，所有的参数已经定义好并完成了初始化。

对于本次项目中使用的模型，所有参数的名称，定义和默认值，请见[Appendix 4.1](### Keysight: Angelov-GaN Parameters Definitions and Default Values)

#### ==List of Significant Parameters==

并非所有参数都将对最终的仿真结果产生实质性影响。同时，由于ICCAP和ADS使用的仿真器版本不一定一致，有相当一部分参数将在ADS的仿真器中出现，但是并不会被ICCAP所提取。不过幸运的是：经过测试，这一系列参数基本不会对最终的fitting结果产生实质性影响。

对于将会对仿真结果产生实质性影响，且支持从ICCAP中进行提取的参数，我整理如下：

> 根据参数的类型和对最终结果的影响，我将参数分为以下三组；
>
> 对于每个参数，基于本次项目中获得的经验，主要有三种获取信息的来源：来自ICCAP的计算，来自manual提取参数的程序，和根据fitting结果的tuning。在表格中，我分别用ICC, MAN, TUN代表信息的来源，其中1代表该参数信息可以在这一过程中获取。

| Parameter | Definition and Description                                   | ICC  | MAN  | TUN  |
| --------- | ------------------------------------------------------------ | ---- | ---- | ---- |
| Ipk0      | Value of drain current (id) at maximum transconductance (gm) | 1    | 0    | 1    |
| Vpks      | Gate voltage (Vg) at maximum transconductance (gm)           | 1    | 0    | 1    |
| Dvpks     | Change in gate voltage at peak transconductance              | 0    | 0    | 1    |
| P1        | Polynomial coefficient for channel current at peak gm        | 0    | 1    | 1    |
| P2        | Polynomial coefficient for channel current                   | 0    | 0    | 1    |
| P3        | Polynomial coefficient for channel current                   | 0    | 0    | 1    |
| Alphar    | Saturation parameter alpha r                                 | 0    | 0    | 1    |
| Alphas    | Saturation parameter alpha                                   | 0    | 0    | 1    |
| Lambda    | Channel length modulation parameter                          | 0    | 0    | 1    |
| Lambda1   | Channel length modulation parameter                          | 0    | 0    | 1    |
| Ij        | Gate forward saturation current                              | 0    | 0    | 1    |

| Parameter | Definition and Description             | ICC  | MAN  | TUN  |
| --------- | -------------------------------------- | ---- | ---- | ---- |
| Cds       | Zero-bias drain-source capacitance     | 1    | 0    | 1    |
| Cgspi     | Gate-source pinch-off capacitance      | 1    | 0    | 1    |
| Cgs0      | Gate-source capacitance parameter      | 1    | 0    | 1    |
| Cgdpi     | Gate-drain pinch-off capacitance       | 1    | 0    | 1    |
| Cgd0      | Gate-drain capacitance parameter       | 1    | 0    | 1    |
| Cgdpe     | External gate-drain capacitance        | 1    | 0    | 1    |
| P10       | Polynomial coefficient for capacitance | 0    | 1    | 1    |
| P11       | Polynomial coefficient for capacitance | 0    | 1    | 1    |
| P20       | Polynomial coefficient for capacitance | 0    | 1    | 1    |
| P21       | Polynomial coefficient for capacitance | 0    | 1    | 1    |
| P30       | Polynomial coefficient for capacitance | 0    | 1    | 1    |
| P31       | Polynomial coefficient for capacitance | 0    | 1    | 1    |
| P40       | Polynomial coefficient for capacitance | 0    | 1    | 1    |
| P41       | Polynomial coefficient for capacitance | 0    | 1    | 1    |

| Parameter | Definition and Description | ICC  | MAN  | TUN  |
| --------- | -------------------------- | ---- | ---- | ---- |
| Rg        | Gate resistance            | 1    | 0    | 1    |
| Rd        | Drain resistance           | 1    | 0    | 1    |
| Rs        | Source resistance          | 1    | 0    | 1    |
| Ri        | Input resistance           | 1    | 0    | 1    |
| Rgd       | Non-ohmic gate resistance  | 1    | 0    | 1    |
| Lg        | Gate inductance            | 1    | 0    | 1    |
| Ld        | Drain inductance           | 1    | 0    | 1    |
| Ls        | Source inductance          | 1    | 0    | 1    |



### ==IC-CAP Extraction Flow== 

这一部分将介绍基于IC-CAP的参数提取过程。

#### ==Extraction Flow Overview==

这一部分将介绍IC-CAP软件原生设计的参数提取流程。

#### ==Debugging==

这一部分将介绍实际运行Extraction Flow之前的debug过程。当然，并不是所有问题都能被解决。因此在本次工作中，我们只使用IC-CAP计算了一部分参数。之后我们会基于这些参数来手动提取剩余的参数。



### ==Parameter Extractions==

#### ==IC-CAP Data Output==

这一部分将总结所有从IC-CAP当中读取的参数。

关于这些参数的定义，请查阅上文的所有参数列表，或significant parameter的列表。这一部分主要结合ICCAP的数据提取这些参数。

#### ==Manual Extractions==

由于IC-CAP的软件问题，在extract和tuning的过程中有一系列参数并不能被有效提取，因此我们进行一系列的手动提取，来获得能够被用于建模的参数。



### ==Simulations and Optimizations==

#### Export IC-CAP Models to ADS

IC-CAP官方帮助文档中的方法并不完全可用。

从IC-CAP完成数据导出后，IC-CAP将导出两个文件：

1. 含有simulator名字的`.lib`文件
2. 以IC-CAP项目名称为文件名的`.mps`文件

将导出的文件导入到ADS，首先需要进行以下操作：

1. 由于angelov GaN是veriloga的模型，所以要先把veriloga的designKit加进来。根据ADS的manual，下面是这一步的具体操作：

   > 0. Navigate from the ADS Main window: Choose DesignKit > Manage Favorite Design Kits to display the Manage Favorite Design Kits dialog box.
   > 1.  Since the Design Kit is delivered as an unzipped file, simply click the Add Library Definition File and browse to $HPEESOF_DIR/tiburonda/ads/designkits/tiburon-da_veriloga.（ADS安装路径下）
   > 2. Select the lib.defs file and click Open.
   > 3. The Add Design Kit dialog box appears to add the design kit to current workspace. Click OK.
   > 4. If a design is open, a warning “All designs must be closed to Add a Design Kit” appears.
   > 5. Close all the designs and click OK to add the design kit to your current workspace.
   > 6. Close the Manage Favorite Design Kits dialog box and open a schematic window. The Devices-Verilog-A palette should now be available in the Component Palette List. The following figure shows the icons for each of the devices and models available in the Devices-Verilog-A palette.

2. load Model card，有两种解决办法：

   1. 使用tools->IC-CAP import->Any Device选择之后，输入angelov_gan_va_Model (注意大小写)然后弹出对话框，选择之前生成的mps文档。load好之后的结果；
   2. 使用DynamicLink->Add Netlist File Include。双击图标选择 之前生成的lib即可。(注意lib里load verilogA文件的路径一定要正确) 

   a和b相比，a会更灵活一些，可以进行参数的tunning，而b作为ICCAP推荐的方法，只能基于导出的文件进行仿真。

#### Simulations Setups

我们可以在ADS当中搭建测试电路：

DC的仿真电路如下：

![4b123e625db0490b7b22748d44c1a5fc](./assets/4b123e625db0490b7b22748d44c1a5fc.png)

S参数的仿真电路如下：

![0786d7e6f752e8047ba5176d4e5354d3](./assets/0786d7e6f752e8047ba5176d4e5354d3.png)

在仿真电路搭建完成后，我们依然可能会面临问题。以下是两个常见问题的解决方案：

1. 如果simulator给出warning，我们可以通过给端口进行命名的方式进行解决
2. 如果simulator在仿真中报错，显示所给的instance存在问题，可能是存在以下两个问题：
   1. 参数模型和FET没有采用相同的模型，我们必须确保两个模型要么都是ADS的原生格式，要么都是VerilogA模式
   2. 参数模型的名称可能与FET模型的不同

#### Preparations for Simulations Result Analysis

只观察仿真结果难以观察fitting的结果。我们需要将IC-CAP的测量结果导入到ADS当中，和仿真测试进行对比。

但是很遗憾，我尝试了相当多版本的ADS（从2017到2024），所有的ADS版本使用report页面的Data Tools工具，直接基于ICCAP的默认输出`.mdl`格式进行导入都会产生问题。我们尝试在各种技术论坛中进行了检索，目前没有找到这一问题的准确答复。

在这一过程中，很有可能会覆盖掉之前已经仿真出的数据，使数据从 data set 界面当中消失。但是我们可以通过重新运行指定cell的仿真来恢复被复写为空文件的仿真数据。

但是，我们找到了间接性解决这一问题的方法，DC与RF的方法略有不同：

- 对于DC测量数据，我们可以这样将其导入ADS：
  1. 在IC-CAP中选择File-Export
  2. 选择将测量数据导出为`.ds`文件，这是ADS的原生数据显示格式
  3. 将导出得到的`.ds`文件直接导入ADS项目的data文件夹
  4. 检索需要使用的数据，其中以.m为结尾的是测量文件，以.s为结尾的是仿真文件
  5. 选择适当的数据和verses关系，绘制iv curve
- 对于RF测量数据，我们可以这样将其导入ADS：
  1. 在IC-CAP中选择Save As
  2. 将需要导出的`.mdl`另存为`.dut`格式
  3. 在ADS中使用Data Tool，选定需要导入的文件
  4. 在下方数据名称输入不重复的名称
  5. 选择IC-CAP进行数据导入
  6. 数据格式被ADS自动写为`.ds`
  7. 检索数据，其中.sd()为已经过de-embed计算的数据，.s()是未经过de-embed的测量数据
  8. 直接选择合适的数据进行对比绘图

将数据导入后，我们可以进行对比，从而得知数据拟合结果的理想程度。但我曾花费时间来纠正以下几点误区：

1. 对于DC：
   1. 我们可以选择开启数据标签显示，从而得知是否针对正确的Vgs进行了拟合
   2. 对于不同工作区拟合情况不同的情况，我们可以分别绘图，从而实现更好的数据可视化
2. 对于RF
   1. 合理规划频率扫描的step，可以极大程度上提高仿真效率，和数据的显示效果
      1. 在参数调整过程中，适当增加step可以提高仿真速率
      2. 在结果分析过程中，适当减少step可以更清晰地看到数据的拟合情况

但是，目前我依然存在一个问题，没有解决：RF的测量默认显示为线，但是仿真结果只能选择散点一种形式。这极大程度上不利于呈现仿真结果的观察。我注意到在Angelov的论文当中也使用了相似的数据呈现形式，我怀疑这是一个ADS仿真过程中普遍存在的问题。

#### ==Optimization of Significant Parameters in ADS==

这一部分将结合上述核心参数列表，主要从仿真结果的角度出发，说明各个参数对于仿真结果的影响

对于直接使用提取数据难以完成fitting的场景，可以基于这一部分对最终的结果进行调整，以抵消测量误差对于仿真结果的影响。

但是，由于这一部分的内容并不基于文献与测量结果，请辩证性看待这一系列结论，并在调整项目的过程中保持谨慎。

#### ==Fitting Results (Updated at Aug 29 2024)==

这一部分将介绍目前最新得到的仿真结果，并对目前存在的困难进行分析。

DC 仿真与测量的拟合情况

RF 仿真与测量的拟合情况



[Back to Table of Contents](# Characterization and Modeling of GaN HEMTs)

<div STYLE="page-break-after: always;"></div>

## ==Appendix==

### Keysight: Angelov-GaN Parameters Definitions and Default Values

![image-20240829195944556](./assets/image-20240829195944556.png)

![image-20240829195954382](./assets/image-20240829195954382.png)

### ==Hand-Scripts of Angelov Model Parameter Extractions==

### Notes on the IC-CAP Help Doc

#### Parameter Extraction Flow Example

0. Example Parameter Extraction Flow

   ![image-20240829192455824](assets/image-20240829192455824.png)

1. Initialize![image-20240829192618897](assets/image-20240829192618897.png)

2. DC Port Resistance![image-20240829192754002](assets/image-20240829192754002.png)

3. SP Cold FET![image-20240829193229308](assets/image-20240829193229308.png)

![image-20240829193250725](assets/image-20240829193250725.png)

4. Gate Diode

   ![image-20240829193426731](assets/image-20240829193426731.png)

   ![image-20240829193453155](assets/image-20240829193453155.png)

   ![image-20240829193535115](assets/image-20240829193535115.png)

   ![image-20240829193552364](assets/image-20240829193552364.png)

5. idvg & idvd

   ![image-20240829193653055](assets/image-20240829193653055.png)

   ![image-20240829193715716](assets/image-20240829193715716.png)

   ![image-20240829193749966](assets/image-20240829193749966.png)

   ![image-20240829193811622](assets/image-20240829193811622.png)

   ![image-20240829193841299](assets/image-20240829193841299.png)

6. SP

   ![image-20240829194108905](assets/image-20240829194108905.png)

   ![image-20240829194126101](assets/image-20240829194126101.png)

   ![image-20240829194205151](assets/image-20240829194205151.png)

   ![image-20240829194216313](assets/image-20240829194216313.png)

   ![image-20240829194241064](assets/image-20240829194241064.png)

   ![image-20240829194256350](assets/image-20240829194256350.png)

7. Finalize: Saving all parameters in the model files



[Back to Table of Contents](# Characterization and Modeling of GaN HEMTs)

<div STYLE="page-break-after: always;"></div>

## ==Reference==



[Back to Table of Contents](#Characterization and Modeling of GaN HEMT)
