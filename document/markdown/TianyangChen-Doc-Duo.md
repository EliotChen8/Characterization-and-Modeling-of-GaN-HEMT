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

## Modeling

### Angelov GaN Parameters

#### All Parameters

使用 Angelov GaN 进行建模，我们需要提取一系列参数。
对于simulator来说，所有的参数已经定义好并完成了初始化。

对于本次项目中使用的模型，所有参数的名称，定义和默认值，请见[Appendix 4.1](### Keysight: Angelov-GaN Parameters Definitions and Default Values)

#### List of Significant Parameters

并非所有参数都将对最终的仿真结果产生实质性影响。同时，由于ICCAP和ADS使用的仿真器版本不一定一致，有相当一部分参数将在ADS的仿真器中出现，但是并不会被ICCAP所提取。不过幸运的是：经过测试，这一系列参数基本不会对最终的fitting结果产生实质性影响。

对于将会对仿真结果产生实质性影响，且支持从ICCAP中进行提取的参数，我整理如下：

> 根据参数的类型和对最终结果的影响，我将参数分为以下三组；
>
> 对于每个参数，基于本次项目中获得的经验，主要有三种获取信息的来源：来自ICCAP的计算，来自manual提取参数的程序，和根据fitting结果的tuning。在表格中，我分别用ICC, MAN, TUN代表信息的来源，其中1代表该参数信息可以在这一过程中获取。

DC Characters and Polynomial Coefficients:

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

Capacitance Parameters and Polynomial Coefficients:

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

Resistance and Inductance Parameters:

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



### IC-CAP Extraction Flow 

#### Extraction Flow Overview

这一部分将介绍IC-CAP软件原生设计的参数提取流程。

![image-20240830164602889](assets/image-20240830164602889.png)

具体而言，整个流程主要分为7个大的部分，每个部分包含着软件中显示的extraction setup，在这些setup当中，我么可以的得到我们需要的参数，具体情况如下所示（对于提取出核心参数的步骤进行了加粗）：

1. **Initialize:**
   1. Reset Parameter to Defaults:
   2. Initialize Parameter and Boundaries for Extraction:
   3. Update All Measures Data for Extraction:
2. **Port Res:**
   1. **PreDC Port1: Z1;**
   2. **PreDC Port2: Z2;**
3. **Cold FET:**
   1. **SP Cold FET: Rg, Rd, Rs, Lg, Ld, Ls;**
4. **Gate Diode:**
   1. DC gate diode forward:
   2. DC gate diode reverse:
5. **DC idvd & idvg:**
   1. **DC idvg: Ipk0, Vpks**
   2. DC idvd:
   3. DC idvg:
   4. DC idvd:
   5. DC idvg:
6. **SP vg & vd:**
   1. SP vg at vd0 A1: 
   2. SP vg at vg0:
   3. **SP vg at vd0 A1: Cgs0, Cgspi, Cds, Cgd0, Cgdpi, Ri, Rgd;**
   4. **SP vg at vg0: Cgs0, Cgspi, Cds, Cgd0, Cgdpi**
   5. **SP vg at vgm2: Cgdpe**
7. **Finalize:**
   1. Save Parameters:

当然，这个流程不是完美的，尤其是在拟合过程中将会出现大量error。根据我的测试，软件中自带的extract flow甚至不能完整运行自带的demo程序，且debug过程相当复杂。

根据与教授的沟通，教授告诉我软件并不是万能的，我们应该以软件作为自己的启发，但回归论文寻找更清晰的答案。因此在本次工作中，我们的目的是：

1. 能够完整的运行整个extract flow；
2. 使用IC-CAP计算了一部分参数；
3. 之后，我们会基于这些参数和论文中的定义来手动提取剩余的参数；
4. 最终，根据ADS的tuning结果来得到所有参数。

#### Debugging

这一部分将介绍实际运行Extraction Flow之前的debug过程。

如果使用软件自带的程序，由于其必须要提取一系列温度敏感性相关的参数，系统会强制要求测量两个温度下期间的character。具体而言，软件会禁止我们选择shrink list。

<img src="assets/image-20240830165650120.png" alt="image-20240830165650120" style="zoom: 80%;" />

但是本次暑期科研的测试平台只支持测量室温一个温度下的数据，这和软件产生了冲突。

在参数提取过程中，这个问题会被体现出来。具体而言，软件在初始化过程中会中断，并禁止我们继续进行参数提取，这将使我们完全不能从IC-CAP当中提取所有参数。

为了解决这一问题，我们可以进行以下操作

- 选中室温（Tnom）下的测试数据，并导出；
- 选中另外一个温度的对应setup，导入室温下的数据；
- 请不要忘记：在这一步选择Copy Tnom Settings，否则程序将会依旧无法运行。

此时运行测试流程，程序将可以运行，运行中主要会出现三种报错：

- 优化函数显示 Data Unchanged，这是相对正常的，说明拟合结果已经达到了最好；
- 优化函数中断并显示仿真器出错，这是相对难以处理的问题。我们可以选择从上一步重新运行，大多数情况下这一种错误将会消失；
- 在terminal的output显示较大误差，且数据不变，这种情况需要分类讨论：
  - 如果是参数触及了仿真前设置的极限，可以尝试调整极限；
  - 但是绝大多数情况下，函数就是不工作；
    事实上，我曾经花了一个星期来研究这个问题，但是没有得到一个明确的答案；
    也正是在此时教授提醒了我，让我不要盲目相信这个软件。



### Parameter Extractions

#### IC-CAP Data Output

这一部分将总结所有从IC-CAP当中读取的参数。

关于这些参数的定义，请查阅上文的所有参数列表，或significant parameter的列表。这一部分主要结合ICCAP的数据提取这些参数。

以下是所有参数的读取过程：

DC Characters and Polynomial Coefficients:

- Vpks: -0.1

  gm峰值位于-0.1~0之间

  <img src="assets/image-20240830181803658.png" alt="image-20240830181803658" style="zoom: 25%;" />

- Ipks: 0.033

  读取-0.1时候的电流值

  <img src="assets/image-20240830182147730.png" alt="image-20240830182147730" style="zoom:25%;" />

Capacitance Parameters and Polynomial Coefficients:

- 根据帮助文档：

  <img src="assets/image-20240830183502777.png" alt="image-20240830183502777" style="zoom: 67%;" />

  我们得到以下结果：

  <img src="assets/image-20240830185147132.png" alt="image-20240830185147132" style="zoom: 33%;" />

  - Cgs0: 83;
  - Cgspi: 88;
  - Cds: 29;
  - Cgd0: 53;
  - Cgdpi: 44;

- 再根据帮助文档：

  <img src="assets/image-20240830190459048.png" alt="image-20240830190459048" style="zoom:67%;" />

  我们针对相同的参数组合又得到了结果：

  <img src="assets/image-20240830185843868.png" alt="image-20240830185843868" style="zoom: 33%;" />

  - Cgs0: 20;
  - Cgspi: 150;
  - Cds: 20;
  - Cgd0: 93;
  - Cgdpi: 5;

  令人担忧的是，这三个曲线并不符合帮助文档中呈现的趋势。

- 最终根据帮助文档：

  <img src="assets/image-20240830190148155.png" alt="image-20240830190148155" style="zoom:67%;" />

  观察测量结果：

  <img src="assets/image-20240830190213591.png" alt="image-20240830190213591" style="zoom: 25%;" />

  Cgdpe:5.2;

Resistance and Inductance Parameters:

- 根据帮助文档，这一部分的数据主要来源于 Cold FET 的 setup

  <img src="assets/image-20240830192426827.png" alt="image-20240830192426827" style="zoom:67%;" />

  根据；论文叙述，提取电阻值应该使用低频的flat range，电感值应使用高频的flat range

  <img src="assets/image-20240830193841287.png" alt="image-20240830193841287" style="zoom:33%;" />

  读出以下电阻值：

  - Rg: 25.2;
  - Rd: 13.0;
  - Rs: 9.2;

  读出以下电容值：

  - Lg: 20.0;
  - Ld: 39.4;
  - Ls: -9.4;

  这里有两点非常令人担心：

  1. Demo Project和这里的低频都没有呈现出flat range；
  2. Ls得到的不是正数。

- 接下来读取Ri:

  <img src="assets/image-20240830195421595.png" alt="image-20240830195421595" style="zoom:33%;" />

  Ri = 8.0;

- 最终读取Rgd

  <img src="assets/image-20240830200543270.png" alt="image-20240830200543270" style="zoom:33%;" />

  Rgd = 27.2.

#### Manual Extractions

由于IC-CAP的软件问题，在extract和tuning的过程中有一系列参数并不能被有效提取，因此我们进行一系列的手动提取，来获得能够被用于建模的参数。

DC Characters and Polynomial Coefficients:

- P1：这一步通过计算峰值处的gm与对应的id之比得到：

  <img src="assets/image-20240830204111216.png" alt="image-20240830204111216" style="zoom: 33%;" />
  $$
  P1 = \frac{gm_{max}}{Id} = \frac{35.79}{33.13} = 1.08
  $$

Capacitance Parameters and Polynomial Coefficients:

在这一部分，我们需要：

1. 我们首先需要根据帮助文档中提供的信息，确定提取参数需将数据抄写至MATLAB；
2. 基于论文中参数的定义，进行相关的函数运算，并进行线性拟合。

具体而言，我们按照以下方式完成这一过程：

首先，我们阅读帮助文档中对电容多项式参数的表述：

<img src="assets/image-20240830223545909.png" alt="image-20240830223545909" style="zoom: 33%;" />

然后，我们将数据导入MATLAB：

```matlab
vg = [-3:0.2:0];
cgsvg = [85.67,86.18,86.87,88.15,88.43,89.28,90.35,91.66,95.31,108.2,126.0,139.6,151.1,160.5,167.7,172.5];
cgdvg = [41.4,42.0,42.6,43.6,44.1,44.9,45.6,46.9,49.0,56.7,69.6,80.8,88.6,93.6,96.6,98.9];

vd = [0:1:28];
cgsvd = [172.8,163.4,153.5,152.1,152.2,155.0,157.1,158.8,160.2,161.6,162.9,164.3,165.5,166.6,168.0,168.2,168.5,168.9,169.4,169.7,170.1,170.3,170.0,170.1,170.2,170.4,170.4,170.3,170.2];
cgdvd = [98.8,76.0,49.8,39.5,31.7,25.1,19.4,15.3,12.5,10.6,9.2,8.1,7.2,6.6,6.0,5.6,5.2,4.9,4.6,4.4,4.2,4.1,3.9,3.7,3.6,3.6,3.5,3.4,3.4];

cgspi =     88;
cgs0 =      83;
cgdpi =     44;
cgd0 =      53;
```

我们可以进行绘图，来确保数据的正确性：

<img src="assets/image-20240830214409838.png" alt="image-20240830214409838" style="zoom: 50%;" />

我们可以查阅这一过程在文章中的表达：

<img src="assets/image-20240830214703000.png" alt="image-20240830214703000" style="zoom:50%;" />

其中：

<img src="assets/image-20240830214715663.png" alt="image-20240830214715663" style="zoom:50%;" />

接下来，我们以此对上述参数进行计算

- **P11 P10:**

  我们计算以下函数：

  <img src="assets/image-20240830220206120.png" alt="image-20240830220206120" style="zoom:50%;" />

  我们通过MATLAB进行运算，并进行线性拟合：

  ```MATLAB
  % p11vgs+p10
  y1 = atanh(((cgsvg-cgspi)/(cgs0))-1);
  
  % Find indices for vg between -1.4 and -0.6
  idx = find(vg >= -1.7 & vg <= -0.9);
  
  % Linear fit for y1 over the selected range of vg
  p11p10 = polyfit(vg(idx), y1(idx), 1)  
  % Linear fit, p(1) is slope, p(2) is intercept
  
  % Generate values from linear fit
  y_fit = polyval(p11p10, vg(idx));
  
  % Plotting
  clf;
  plot(vg, y1, 'b-', 'DisplayName', 'Original y1'); hold on;
  plot(vg(idx), y_fit, 'r--', 'DisplayName', 'Linear Fit');
  ```

  运行结果如下，这一步忽略了虚部，但没有影响最终结果：

  <img src="assets/image17250704836580.png" alt="img" style="zoom:67%;" />

  最终我们得到：

  ```
  p11p10 = 1×2
      2.2086    1.6136
  ```

- **P41 P40:**

  我们计算以下函数：

  <img src="assets/image-20240830220238640.png" alt="image-20240830220238640" style="zoom:50%;" />

  我们通过MATLAB进行运算，并进行线性拟合：

  ```MATLAB
  % p41vds+p40
  y4 = atanh(((cgdvg-cgdpi)/cgd0)-1);
  
  % Find indices for vg between -1.4 and -0.6
  idx = find(vg >= -1.5 & vg <= -0.8);
  
  % Linear fit for y1 over the selected range of vg
  p41p40 = polyfit(vg(idx), y4(idx), 1)  
  % Linear fit, p(1) is slope, p(2) is intercept
  
  % Generate values from linear fit
  y_fit = polyval(p41p40, vg(idx));
  
  % Plotting
  clf;
  plot(vg, y4, 'b-', 'DisplayName', 'Original y1'); hold on;
  plot(vg(idx), y_fit, 'r--', 'DisplayName', 'Linear Fit');
  ```

  运行结果如下这一步忽略了虚部，但没有影响最终结果：

  <img src="assets/image17250704696440.png" alt="img" style="zoom:67%;" />

  最终我们得到：

  ```
  p41p40 = 1×2
      1.9931    1.3454
  ```

- **P21 P20:**

  我们计算以下函数：

  <img src="assets/image-20240830220307897.png" alt="image-20240830220307897" style="zoom:50%;" />

  我们通过MATLAB进行运算，并进行线性拟合：

  ```MATLAB
  % p21vds+p20
  p10 = p11p10(2)
  y2 = atanh(((cgsvd-cgspi)/(cgs0*(1+tanh(p10))))-1);
  
  % Find indices for vg between -1.4 and -0.6
  idx = find(vd >= 0 & vd <= 3);
  
  % Linear fit for y1 over the selected range of vg
  p21p20 = polyfit(vd(idx), y2(idx), 1)  
  % Linear fit, p(1) is slope, p(2) is intercept
  
  % Generate values from linear fit
  y_fit = polyval(p21p20, vd(idx));
  
  % Plotting
  clf;
  plot(vd, y2, 'b-', 'DisplayName', 'Original y1'); hold on;
  plot(vd(idx), y_fit, 'r--', 'DisplayName', 'Linear Fit');
  ```

  运行结果如下：

  <img src="assets/image17250704995060.png" alt="img" style="zoom:67%;" />

  最终我们得到：

  ```
  p21p20 = 1×2
     -0.0637   -0.5204
  ```

  ==这一步存在问题：Simulator支持的P21最小值为0.1。==

- **P31 P30:**

  我们计算以下函数：

  <img src="assets/image-20240830220325701.png" alt="image-20240830220325701" style="zoom:50%;" />

  我们通过MATLAB进行运算，并进行线性拟合：

  ```MATLAB
  % p31vds+p30
  p40 = p41p40(2)
  p41 = p41p40(1)
  
  y3 = zeros(size(vd));
  
  for i = 1:length(vd)
      tanh_value = tanh(p40 - p41 * vd(i));
      y3(i) = (atanh(((cgdvd(i) - cgdpi)/(cgd0 * (1 + tanh_value))) - 1));
  end
  
  % Find indices for vg between -1.4 and -0.6
  idx = find(vd >= 0.1 & vd <= 3);
  
  % Linear fit for y1 over the selected range of vg
  p31p30 = polyfit(vd(idx), y3(idx), 1)  
  % Linear fit, p(1) is slope, p(2) is intercept
  
  % Generate values from linear fit
  y_fit = polyval(p31p30, vd(idx));
  
  % Plotting
  clf;
  plot(vd, y3, 'b-', 'DisplayName', 'Original y1'); hold on;
  plot(vd(idx), y_fit, 'r--', 'DisplayName', 'Linear Fit');
  ```

  运行结果如下，这一步忽略了虚部，**且影响最终结果**：

  <img src="assets/image17250717725520.png" alt="img" style="zoom:67%;" />

  最终我们得到：

  ```
  p31p30 = 1×2 complex
    -0.2156 - 0.7854i   0.6075 + 1.5708i
  ```

  ==也就是在这一步中产生了虚数，这是不能被simulator利用的。==

#### Result of Extractions

截止到这步，我们已经得到的数据如下所示，其中存在问题的数据已高亮显示：

DC Characters and Polynomial Coefficients:

| Parameter | Definition and Description                                   | Original Value |
| --------- | ------------------------------------------------------------ | -------------- |
| Ipk0      | Value of drain current (id) at maximum transconductance (gm) | 0.033          |
| Vpks      | Gate voltage (Vg) at maximum transconductance (gm)           | -0.1           |
| Dvpks     | Change in gate voltage at peak transconductance              | ==NA==         |
| P1        | Polynomial coefficient for channel current at peak gm        | 1.08           |
| P2        | Polynomial coefficient for channel current                   | ==NA==         |
| P3        | Polynomial coefficient for channel current                   | ==NA==         |
| Alphar    | Saturation parameter alpha r                                 | ==NA==         |
| Alphas    | Saturation parameter alpha                                   | ==NA==         |
| Lambda    | Channel length modulation parameter                          | ==NA==         |
| Lambda1   | Channel length modulation parameter                          | ==NA==         |
| Ij        | Gate forward saturation current                              | ==NA==         |

Capacitance Parameters and Polynomial Coefficients:

| Parameter | Definition and Description             | Original Value  |
| --------- | -------------------------------------- | --------------- |
| Cds       | Zero-bias drain-source capacitance     | 29              |
| Cgspi     | Gate-source pinch-off capacitance      | 88              |
| Cgs0      | Gate-source capacitance parameter      | 83              |
| Cgdpi     | Gate-drain pinch-off capacitance       | 44              |
| Cgd0      | Gate-drain capacitance parameter       | 53              |
| Cgdpe     | External gate-drain capacitance        | 5.2             |
| P10       | Polynomial coefficient for capacitance | 1.61            |
| P11       | Polynomial coefficient for capacitance | 2.21            |
| P20       | Polynomial coefficient for capacitance | -0.52           |
| P21       | Polynomial coefficient for capacitance | ==-0.06==       |
| P30       | Polynomial coefficient for capacitance | ==0.61+1.57i==  |
| P31       | Polynomial coefficient for capacitance | ==-0.22-0.79i== |
| P40       | Polynomial coefficient for capacitance | 1.35            |
| P41       | Polynomial coefficient for capacitance | 1.99            |

Resistance and Inductance Parameters:

| Parameter | Definition and Description | Original Value |
| --------- | -------------------------- | -------------- |
| Rg        | Gate resistance            | 25.2           |
| Rd        | Drain resistance           | 13             |
| Rs        | Source resistance          | 9.2            |
| Ri        | Input resistance           | 8.0            |
| Rgd       | Non-ohmic gate resistance  | 27.2           |
| Lg        | Gate inductance            | 20.0           |
| Ld        | Drain inductance           | 39.4           |
| Ls        | Source inductance          | ==-9.4==       |



### Simulations and Optimizations

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

#### Original Results

我们直接将Extract出来的函数输入仿真器，观察结果。蓝色是测量，红色是仿真。

DC的仿真结果如下：

![image-20240830225750849](assets/image-20240830225750849.png)

对于S参数，我们仿真三个场景。第一个是cold FET：

<img src="assets/image-20240830230104666.png" alt="image-20240830230104666" style="zoom:45%;" />

第二个是在没有施加Vds的前提下，扫描Vgs：

<img src="assets/image-20240830230634926.png" alt="image-20240830230634926" style="zoom:33%;" />

第三个是在Vgs=1.75，这里是gm pinch off的地方，我们从0-28V扫描Vds：

<img src="assets/image-20240830230305278.png" alt="image-20240830230305278" style="zoom:33%;" />

> 看到结果的时候心都要碎了，
> 因为教授会说我的结果看起来很funny。

#### Optimization of Significant Parameters in ADS

这一部分将结合上述核心参数列表，主要从仿真结果的角度出发，说明各个参数对于仿真结果的影响

对于直接使用提取数据难以完成fitting的场景，可以基于这一部分对最终的结果进行调整，以抵消测量误差对于仿真结果的影响。

但是，由于这一部分的内容并不基于文献与测量结果，请辩证性看待这一系列结论，并在调整项目的过程中保持谨慎。

DC Characters and Polynomial Coefficients:

| Parameter | Effect on DC                                                 | Effect on S-Parameters                                       |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Ipk0      | Magnitude of drain current (Id)                              | Influential, but tuning is not recommended                   |
| Vpks      | Position of the turn-on voltage in the Id-Vg                 | Influential, but tuning is not recommended                   |
| Dvpks     | Slope in the turn-on region; gate diode conduction position  | Discreteness at low-frequency start in pinch-off simulation, smaller values lead to greater discreteness |
| P1        | Density of the Id-Vd curves as gate voltage is swept, negative values indicate inverse relationship between Vg and turn-on current | Influential, but tuning is not recommended                   |
| P2        | Voltage at the peak gm in Id-Vd curves                       | Discreteness at low-frequency start in pinch-off simulation, larger values lead to greater discreteness |
| P3        | Density of the Id-Vd curves                                  | Discreteness at low-frequency start in pinch-off simulation, smaller values lead to greater discreteness |
| Alphar    | Slope and curve disparity in the turn-on region              | Influential, but tuning is not recommended                   |
| Alphas    | Sharpness of the transition from turn-on to saturation regions | Influential, but tuning is not recommended                   |
| Lambda    | Slope in the saturation region                               | Influential, but tuning is not recommended                   |
| Lambda1   | Slope in the saturation region                               | Influential, but tuning is not recommended                   |
| Ij        | Current spread at high voltage in the off region, very minimal | None                                                         |

Capacitance Parameters and Polynomial Coefficients:

| Parameter | Effect on DC | Effect on S-Parameters                                       |
| --------- | ------------ | ------------------------------------------------------------ |
| Cds       | None         | Phase difference in S22 increases with value; S21 phase difference also increases |
| Cgspi     | None         | Outer magnitude of S21 decreases with value                  |
| Cgs0      | None         | Inner magnitudes of S21 and S12 decrease with value; outer magnitude of S12 increases |
| Cgdpi     | None         | Curvature of S21 increases with value                        |
| Cgd0      | None         | Sequence of curve                                            |
| Cgdpe     | None         | Dispersion of S21 and S12                                    |
| P10       | None         | Dependent variable, tuning not recommended                   |
| P11       | None         | Dependent variable, tuning not recommended                   |
| P20       | None         | Dependent variable, tuning not recommended                   |
| P21       | None         | Dependent variable, tuning not recommended                   |
| P30       | None         | Dependent variable, tuning not recommended                   |
| P31       | None         | Dependent variable, tuning not recommended                   |
| P40       | None         | Dependent variable, tuning not recommended                   |
| P41       | None         | Dependent variable, tuning not recommended                   |

Resistance and Inductance Parameters:

| Parameter | Effect on DC                                                 | Effect on S-parameters                                       |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Rg        | None                                                         | S11 amplitude decreases with increasing value; dispersion and phase difference in S21 and S12 also decrease |
| Rd        | Amplitude of id-vg curves                                    | Amplitude of S22 and S12 decreases with increasing value     |
| Rs        | Amplitude of idvd; forward conduction region amplitude in idvg | S11 and S22 amplitude decreases with value; dispersion and phase difference in S21 and S12 also decrease |
| Ri        | None                                                         | S11 amplitude decreases with increasing value; phase difference and dispersion in S21 and S12 also decrease |
| Rgd       | None                                                         | S22 amplitude decreases with value; phase difference in S21 and S12 increases |
| Lg        | None                                                         | Phase difference in S11 increases with value; similar increase in phase difference for S21 and S12 |
| Ld        | None                                                         | Phase difference in S22 decreases with value; amplitude and phase difference in S21 increase; phase difference in S12 also increases |
| Ls        | None                                                         | Phase difference in S11 and S22 increases with value; S21 and S12 show inner curling at higher frequencies |

#### Fitting Results (Updated at Aug 29 2024)

这一部分将介绍目前最新得到的仿真结果，并对目前存在的困难进行分析。

DC的仿真结果如下：

<img src="assets/image-20240831011019707.png" alt="image-20240831011019707" style="zoom:33%;" />

对于S参数，我们仿真三个场景。第一个是cold FET：

<img src="assets/image-20240830234212067.png" alt="image-20240830234212067" style="zoom:33%;" />

第二个是在没有施加Vds的前提下，扫描Vgs：

<img src="assets/image-20240830233504228.png" alt="image-20240830233504228" style="zoom:33%;" />

第三个是在Vgs=1.75，这里是gm pinch off的地方，我们从0-28V扫描Vds:

<img src="assets/image-20240831010035759.png" alt="image-20240831010035759" style="zoom:33%;" />



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
