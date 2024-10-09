---
layout: default
title: Electricity
parent: Physics
---

# Electricity

### 什么是电？

电是一种能量形式，它的表现形式是电荷的流动。电荷有两种：正电荷和负电荷。大多数电现象都是由于电子（带负电荷的粒子）在物体中移动而产生的。电子的移动会形成电流，而电流则是电的基本表现形式之一。

#### 电流与电压

- **电流（Current）**：电流是电荷在电路中流动的速率。电流的单位是安培（A），用符号“I”表示。电流的方向通常定义为正电荷流动的方向（尽管实际是电子在反方向移动）。
  
- **电压（Voltage）**：电压是推动电流在电路中流动的“压力”或“势能差”。电压的单位是伏特（V），用符号“V”表示。电压越大，电流流动的动力越强。

- **电阻（Resistance）**：电阻是对电流流动的阻碍，单位是欧姆（Ω）。电阻越大，电流通过的难度越高。电阻通常由电路中的各种元件提供，帮助调节电流。

### 基础电路知识

一个简单的电路通常包括一个电源（比如电池）、导线和一个负载（比如灯泡）。电源提供电压，导线连接电路元件，负载消耗电能。电流在闭合电路中流动，形成电能的传输。

#### 电路类型

- **串联电路**：电流依次流过每个元件，如果一个元件失效，整个电路就会中断。
  
- **并联电路**：每个元件都有独立的路径，如果一个元件失效，其他元件仍然可以工作。

### 常见的电路元件及其工作原理

#### 电阻器（Resistor）
电阻器是一种消耗电能并提供电阻的元件，用于限制电流流动。电阻的大小决定了它对电流的阻碍作用。可以用欧姆定律（V = IR）来计算电阻、电流和电压的关系。

#### 电容器（Capacitor）
电容器是一种储存电荷的元件。电容器可以暂时储存电能，并在需要时释放。电容的单位是法拉（F），它决定了电容器储存电荷的能力。

#### 电感器（Inductor）
电感器是由线圈绕成的元件，用于储存磁能。电感器会对电流的变化产生阻碍作用，特别是在交流电路中。电感的单位是亨利（H）。

#### 二极管（Diode）
二极管是一种只能让电流单向流动的元件。它常用于整流电路中，将交流电转换为直流电。

#### 晶体管（Transistor）
晶体管是一种用来放大或开关电流的元件。它有三极：发射极、基极和集电极。晶体管是现代电子电路的核心元件。

## PCB

### Common Designator Meanings

| Designator | Component type |
|---|---|
| A | Separable assembly, Sub-assembly (e.g. printed circuit assembly) |
| AN, AS | Antenna |
| AR | Amplifier |
| AT | Attenuator, Isolator |
| BR | Bridge rectifier |
| B, BT | Battery |
| BZ | Buzzer |
| C | Capacitor |
| CB | Circuit breaker, Supercapacitor |
| CN | Capacitor network |
| D, | CR Diode (all types, including LED), Thyristor |
| DL | Delay line |
| DS | Display, General light source, Lamp, Signal light |
| F | Fuse |
| FB | Ferrite bead |
| FD | Fiducial |
| FL | Filter |
| G | Generator, Oscillator |
| GN | General network |
| H | Hardware, Screws, Nuts, Washers |
| HY | Circulator, Directional coupler |
| IR | Infrared diode |
| J | Jack (least-movable connector of a connector pair), Jack connector (connector may have male pin contacts and/or female socket contacts) |
| JP | Jumper (Link) |
| K | Relay, Contactor |
| L | Inductor, Coil, Ferrite bead |
| LS | Loudspeaker, Buzzer |
| M | Mosfet, Motor, Meter, Measuring device |
| MH | Mounting hole |
| MK | Microphone |
| MP | Mechanical part (including screws and fasteners) |
| OP | Opto-isolator, Operational amplifier |
| P | Plug (most-movable connector of a connector pair), Plug connector (connector may have male pin contacts and/or female socket contacts) |
| PS | Power supply |
| Q | Transistor (all types) |
| R | Resistor |
| RLA, RY | Relay |
| RN | Resistor network |
| RT | Thermistor |
| RV | Varistor, Variable resistor |
| S, SW | Switch (all types, including buttons) |
| T | Transformer, Incorrectly used as transistor (see “Q”) |
| TC | Thermocouple |
| TP | Test point |
| TR | Transistor, Transducer |
| TUN | Tuner |
| U | Integrated circuit (IC), Inseparable assembly |
| V | Vacuum tube |
| VR | Voltage regulator (voltage reference), Variable resistor (potentiometer or rheostat), PTC |
| W | Cable, Wire, Busbar |
| X | Socket connector for another item not P or J, paired with the letter symbol for that item (XV for vacuum tube socket, XF for fuse holder, XA for printed circuit assembly connector, XU for integrated circuit connector, XDS for light socket, etc.) |
| XMER | Transformer |
| XTAL | Crystal |
| Y | Crystal, Oscillator |
| Z | Zener Diode |

![SMD Cheat Sheet](https://mechaelephant.com/dev/img/smd_cheat_sheet.png)