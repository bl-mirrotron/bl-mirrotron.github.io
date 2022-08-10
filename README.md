![llr](doc/mirrotronSplash.png)
# The Mirrotron RFQ Control System
* <a href="https://github.com/bl-mirrotron" target="_blank">Source code</a>

## Repositories
* <a href="https://bl-mirrotron.github.io/mirrotron-box/">Mirrotron Application Server</a>
* <a href="https://bl-mirrotron.github.io/mirrotron-rf-src-tray/" target="_blank">RF Frequency Source</a>
* <a href="https://bl-mirrotron.github.io/mirrotron-phase-detector-tray/" target="_blank">Four Quadrant IQ Phase Detector</a>
* <a href="https://bl-mirrotron.github.io/gateGen125-tray/" target="_blank">Timing Gate Generator</a>
* <a href="https://bl-mirrotron.github.io/mirrotron-rfq-llrf-timer-cube/" target="_blank">RFQ LLRF Timer Cube</a>
* <a href="https://bl-mirrotron.github.io/mirrotron-llrf-scope-tray/" target="_blank">IQ Monitor System</a>
* <a href="https://bl-mirrotron.github.io/mirrotron-rfpower-scope-tray/" target="_blank">RF Power Monitor System</a>
* <a href="https://bl-mirrotron.github.io/mirrotron-rfq-temp-cube/" target="_blank">RFQ Temperature Cube</a>
* <a href="https://bl-mirrotron.github.io/mirrotron-rfq-temp-tray-inlet/" target="_blank">RFQ Inlet Temperature Tray</a>
* <a href="https://bl-mirrotron.github.io/mirrotron-rfq-temp-tray-inlet/" target="_blank">RFQ Inlet Temperature Tray</a>
* <a href="https://bl-mirrotron.github.io/mirrotron-rfq-flow-cube/" target="_blank">RFQ Flow Cube</a>
* <a href="https://bl-mirrotron.github.io/mirrotron-rfq-flow-tray-outlet/" target="_blank">RFQ Outlet Flow Tray</a>
* <a href="https://bl-mirrotron.github.io/mirrotron-rfq-flow-tray-outlet/" target="_blank">RFQ Outlet Flow Tray</a>

## Overview
The Mirrotron Radio Frequency Quadrupole (RFQ) is part of a compact neutron source that is being built in Martonvásár Hungary. The compact neutron source consists of five major systems
* 35 keV Hydrogen Ion source
* 2.5 MeV RFQ
* Lithium Target station
* Neutron Instrument stations

The 2.5 MeV RFQ designed and built by Time Co, Ltd., Japan is a pulsed accelerator that can support 1.25 mS pulses at a rate of 40 Hz for a maximum duty factor of 5% . The RFQ can accelerate a peak beam current of 20 mA with an input RF power 260 kW at 200 MHz. providing an average beam power of 2.5 kW. The loaded cavity Q is 10,000 which results in a cavity bandwidth of 20 kHz.

The RFQ accelerator system can be divided into 6 major subsystems
* [RF source (LLRF)](#rf-source)
* [Timing system](#timing-system)
* 200 MHz RF power amplifier
* Vacuum system
* [Cooling system](#cooling-system)
* [Machine protection system](#machine-protection-system)

## RF source
The RF source is a modular system based on the Red-Pitaya Stemlab 125-14 reconfigurable instrument platform. A modular approach was chosen for design simplicity and future upgrades. Likewise, the Red-Pitaya Stemlab 125-14 was chosen for its ease of use. A block diagram is shown in Figure 1. The LLRF system comprises of four modules:
- <a href="https://bl-mirrotron.github.io/mirrotron-rf-src-tray/" target="_blank">RF Frequency Source</a>
- <a href="https://bl-mirrotron.github.io/mirrotron-phase-detector-tray/" target="_blank">Four Quadrant IQ Phase Detector</a>
- <a href="https://bl-mirrotron.github.io/mirrotron-llrf-scope-tray/" target="_blank">IQ Monitor System</a>
- <a href="https://bl-mirrotron.github.io/mirrotron-rfpower-scope-tray/" target="_blank">RF Power Monitor System</a>

<p></p><p style="text-align:center;font-size: large;"><span style="font-weight: bold;color: green;">Figure 1. </span> <span style="font-style: italic;">Block diagram of LLRF</span></p>
<div style="width:100%;text-align:center;"><img width="100%" style="border-style:solid;border-color:#1c6e97;" src="doc/LlrfFPDiagram.png"/></div><br>

<p></p><p style="text-align:center;font-size: large;"><span style="font-weight: bold;color: green;">Figure 2. </span> <span style="font-style: italic;">LLRF modules Implementation</span></p>
<div style="width:100%;text-align:center;"><img width="100%" style="border-style:solid;border-color:#1c6e97;" src="doc/llrf.jpg"/></div><br>

## Timing system
The Mirrotron RFQ is a pulsed system so a timing system is required. The <a href="https://bl-mirrotron.github.io/gateGen125-tray/" target="_blank">Mirrotron Timing system</a> is an 8 channel system based on a 32 bit counter clocked at 125 MHz. The resolution of the timing system is 8nS and can have intervals as long as 17 seconds. The implementation is shown in FigureXXX.

#### Channel allocation
The Mirrotron RFQ uses five of the eight channels:
* <ins>Channel 0</ins>  for the RF source and phase Detector
* <ins>Channel 1</ins>  for LLRF scope
* <ins>Channel 2</ins>  for the RF Power Amp pulse gate
* <ins>Channel 3</ins>  for the RF Power Amp sample and hold
* <ins>Channel 4</ins>  for the RF Power Amp Scope

#### Easy Setup Timer
These channels can be configured with the Timing App as shown in Figure 30. To change the pulse length of the RFQ, all five channels would need to be adjusted which would be time consuming and error prone. To make it easier to change the pulse length a virtual tray called the Easy Setup Timer was created. This virtual tray will adjust all five channels synchronously. This virtual device is implemented in the <a href="https://bl-mirrotron.github.io/mirrotron-box" target="_blank">Mirrotron application server</a>.

<p></p><p style="text-align:center;font-size: large;"><span style="font-weight: bold;color: green;">FigureXXX. </span> <span style="font-style: italic;">Gate Generator Implementation</span></p>
<div style="width:100%;text-align:center;"><img width="100%" style="border-style:solid;border-color:#1c6e97;" src="doc/GateGenImpl.jpg"/></div><br>

## 200 MHz RF power amplifier
more to come

## Cooling system
The RFQ will dissipate energy at an average rate of 15kW when running at peak RF power and  5% duty factor. To keep the remove this energy, two water chillers supply cooling water to the upstream (inlet) and downstream (outlet) ends of the RFQ.  The cooling water flows into headers that split the cooling to various cooling channels built into the RFQ. Control of the water chillers is manual and not part of the control system.

However to ensure that water is flowing at the correct flow rate and temperature, a separate temperature monitor and flow monitor is mounted on each cooling channel on each header as shown in FigureXXX. On top of each header, as shown in FigureXXX,  are mounted custom built Blinky-Lite<sup>TM</sup> trays that measure and report the temperature and flow through each cooling channel to the control system.

Details about the cooling monitor system software and electronics can be found at:
* <a href="https://bl-mirrotron.github.io/mirrotron-rfq-temp-tray-inlet/" target="_blank">Inlet temperature tray</a>
* <a href="https://bl-mirrotron.github.io/mirrotron-rfq-flow-tray-inlet/" target="_blank">Inlet flow tray</a>
* <a href="https://bl-mirrotron.github.io/mirrotron-rfq-temp-tray-outlet/" target="_blank">Outlet temperature tray</a>
* <a href="https://bl-mirrotron.github.io/mirrotron-rfq-flow-tray-outlet/" target="_blank">Outlet flow tray</a>

<p></p><p style="text-align:center;font-size: large;"><span style="font-weight: bold;color: green;">FigureXXX. </span> <span style="font-style: italic;">Cooling System Header</span></p>
<div style="width:100%;text-align:center;"><img width="100%" style="border-style:solid;border-color:#1c6e97;" src="doc/coolingHeaderBottomView.jpg"/></div><br>

<p></p><p style="text-align:center;font-size: large;"><span style="font-weight: bold;color: green;">FigureXXX. </span> <span style="font-style: italic;">Outlet Cooling System Header<br>From left to right: Temperature cube and tray, 5V power, 24V power, Flow cube and tray</span></p>
<div style="width:100%;text-align:center;"><img width="100%" style="border-style:solid;border-color:#1c6e97;" src="doc/coolingHeaderTopView.jpg"/></div><br>

## Machine protection system
More to come
