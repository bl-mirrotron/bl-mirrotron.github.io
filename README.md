# Mirrotron Control System Overview
![llr](doc/mirrotronSplash.png)
* <a href="https://github.com/bl-mirrotron" target="_blank">Source code</a>
* <a href="https://www.bl-mirrotron.com/" target="_blank">Mirrotron Web Page</a>
* <a href="https://www.bl-mirrotron.com/apps" target="_blank">Application Launcher</a>

## Repositories
* <a href="https://docs.bl-mirrotron.com/mirrotron-user-guide/">Mirrotron Users guide</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-box/">Mirrotron Application Server</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rf-src-tray/">RF Frequency Source</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-phase-detector-tray/">Four Quadrant IQ Phase Detector</a>
* <a href="https://docs.bl-mirrotron.com/gateGen125-tray/">Timing Gate Generator</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rfq-llrf-timer-cube/">RFQ LLRF Timer Cube</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-llrf-scope-tray/">IQ Monitor System</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rfpower-scope-tray/">RF Power Monitor System</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rk-pa-tray/">RF Power Amplifier System</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rfq-vacuum-tray/">RFQ Vacuum System</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rfq-vacuum-cube/">RFQ Vacuum System Cube Controller</a>
* <a href="https://docs.bl-mirrotron.com/nXDS-backing-pump-tray/">Backing Pump System</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rfq-temp-cube/">RFQ Temperature Cube</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rfq-temp-tray-inlet/">RFQ Inlet Temperature Tray</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rfq-temp-tray-outlet/">RFQ Outlet Temperature Tray</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rfq-flow-cube/">RFQ Flow Cube</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rfq-flow-tray-inlet/">RFQ Inlet Flow Tray</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rfq-flow-tray-outlet/">RFQ Outlet Flow Tray</a>

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
* [200 MHz RF power amplifier](#200-mhz-rf-power-amplifier)
* [Vacuum system](#vacuum-system)
* [Cooling system](#cooling-system)
* [Machine protection system](#machine-protection-system)

## RF source
The RF source is a modular system based on the Red-Pitaya Stemlab 125-14 reconfigurable instrument platform. A modular approach was chosen for design simplicity and future upgrades. Likewise, the Red-Pitaya Stemlab 125-14 was chosen for its ease of use. A block diagram is shown in Figure 1. The LLRF system comprises of four modules:
- <a href="https://docs.bl-mirrotron.com/mirrotron-rf-src-tray/">RF Frequency Source</a>
- <a href="https://docs.bl-mirrotron.com/mirrotron-phase-detector-tray/">Four Quadrant IQ Phase Detector</a>
- <a href="https://docs.bl-mirrotron.com/mirrotron-llrf-scope-tray/">IQ Monitor System</a>
- <a href="https://docs.bl-mirrotron.com/mirrotron-rfpower-scope-tray/">RF Power Monitor System</a>

<p></p><p style="text-align:center;font-size: large;"><span style="font-weight: bold;color: green;">Figure 1. </span> <span style="font-style: italic;">Block diagram of LLRF</span></p>
<div style="width:100%;text-align:center;"><img width="100%" style="border-style:solid;border-color:#1c6e97;" src="doc/LlrfFPDiagram.png"/></div><br>

<p></p><p style="text-align:center;font-size: large;"><span style="font-weight: bold;color: green;">Figure 2. </span> <span style="font-style: italic;">LLRF modules Implementation</span></p>
<div style="width:100%;text-align:center;"><img width="100%" style="border-style:solid;border-color:#1c6e97;" src="doc/llrf.jpg"/></div><br>

## Timing system
The Mirrotron RFQ is a pulsed system so a timing system is required. The <a href="https://docs.bl-mirrotron.com/gateGen125-tray/">Mirrotron Timing system</a> is an 8 channel system based on a 32 bit counter clocked at 125 MHz. The resolution of the timing system is 8nS and can have intervals as long as 17 seconds. The implementation is shown in Figure 3.

#### Channel allocation
The Mirrotron RFQ uses five of the eight channels:
* <ins>Channel 0</ins>  for the RF source and phase Detector
* <ins>Channel 1</ins>  for LLRF scope
* <ins>Channel 2</ins>  for the RF Power Amp pulse gate
* <ins>Channel 3</ins>  for the RF Power Amp sample and hold
* <ins>Channel 4</ins>  for the RF Power Amp Scope

#### Easy Setup Timer
These channels can be configured with the Timing App as shown in Figure 30. To change the pulse length of the RFQ, all five channels would need to be adjusted which would be time consuming and error prone. To make it easier to change the pulse length a virtual tray called the Easy Setup Timer was created. This virtual tray will adjust all five channels synchronously. This virtual device is implemented in the <a href="https://docs.bl-mirrotron.com/mirrotron-box">Mirrotron application server</a>.

<p></p><p style="text-align:center;font-size: large;"><span style="font-weight: bold;color: green;">Figure 3. </span> <span style="font-style: italic;">Gate Generator Implementation</span></p>
<div style="width:100%;text-align:center;"><img width="100%" style="border-style:solid;border-color:#1c6e97;" src="doc/GateGenImpl.jpg"/></div><br>

## 200 MHz RF power amplifier
The RF Power amplifier is <a href="https://rk-microwave.com/wp-content/uploads/2021/12/CA200BW2-7585RP.pdf" target="_blank">custom made solid state RF power amplifier</a> operating at 200 MHz. The amplifier has a gain of about 75 dB and can transform 10mW (10dBm) of RF signal into 320 kW of RF power. The amplifier can operate a pulse length of 1.25mS at a pulse repetition rate of 40 Hz.  The RF Power amplifier connected to the RFQ is shown in Figure 4.

The RF power amplifier requires two timing channels from the [Timing system](#timing-system).
* <ins>Channel 2</ins>  for the RF Power Amp pulse gate
* <ins>Channel 3</ins>  for the RF Power Amp sample and hold

The RF power amplifier takes the low level signal generated from the [RF source](#rf-source) as shown in Figure 1. The amplifier has a 75dB directional coupler mounted  on its output and the forward and reflected RF signals are available on the front panel. These signals are fed into the [RF power monitor](https://docs.bl-mirrotron.com/mirrotron-rfpower-scope-tray/).

The <a href="https://rk-microwave.com/" target="_blank">manufacturer</a> of the RF power amplifier provides a remote interface so the RF Power amplifier can be [controlled and monitored](https://docs.bl-mirrotron.com/mirrotron-rk-pa-tray/).  

<p></p><p style="text-align:center;font-size: large;"><span style="font-weight: bold;color: green;">Figure 4. </span> <span style="font-style: italic;">RF power amplifier connected to RFQ</span></p>
<div style="width:100%;text-align:center;"><img width="100%" style="border-style:solid;border-color:#1c6e97;" src="doc/PaAndRFQ.jpg"/></div><br>

## Vacuum system

The RFQ requires ultra-high vacuum for operations. RF power should not be applied to the cavity unless the vacuum pressure inside the cavity is less than 5x10<sup>-5</sup> Pa. The RFQ has two identical vacuum systems mounted on either side of the RFQ as shown in Figure 5. The <a href="https://docs.bl-mirrotron.com/mirrotron-rfq-vacuum-tray/">RFQ vacuum system tray</a> is responsible for:
* Control opening and closing of valves
* Read status of gate valve limit switches
* Read vacuum gauge pressures
* Read status of the turbo pumps
  - Turbo pump error status
  - Turbo pump 70% speed status
* RFQ Vacuum protection

The  <a href="https://docs.bl-mirrotron.com/nXDS-backing-pump-tray/">backing pump trays</a> are responsible for:
* Controlling backing-pump power on and off.
* Reading backing-pump status
  - Pump speed
  - Pump Temperature
  - Pump hours
  - Pump cycles

<p></p><p style="text-align:center;font-size: large;"><span style="font-weight: bold;color: green;">Figure 5. </span> <span style="font-style: italic;">Vacuum system layout</span></p>
<div style="width:100%;text-align:center;"><img width="100%" style="border-style:solid;border-color:#1c6e97;" src="doc/VacuumLayout.png"/></div><br>

## Cooling system
The RFQ will dissipate energy at an average rate of 15kW when running at peak RF power and  5% duty factor. To keep the remove this energy, two water chillers supply cooling water to the upstream (inlet) and downstream (outlet) ends of the RFQ.  The cooling water flows into headers that split the cooling to various cooling channels built into the RFQ. Control of the water chillers is manual and not part of the control system.

However to ensure that water is flowing at the correct flow rate and temperature, a separate temperature monitor and flow monitor is mounted on each cooling channel on each header as shown in Figure 6. On top of each header, as shown in Figure 7,  are mounted custom built Blinky-Lite<sup>TM</sup> trays that measure and report the temperature and flow through each cooling channel to the control system.

Details about the cooling monitor system software and electronics can be found at:
* <a href="https://docs.bl-mirrotron.com/mirrotron-rfq-temp-tray-inlet/">Inlet temperature tray</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rfq-flow-tray-inlet/">Inlet flow tray</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rfq-temp-tray-outlet/">Outlet temperature tray</a>
* <a href="https://docs.bl-mirrotron.com/mirrotron-rfq-flow-tray-outlet/">Outlet flow tray</a>

<p></p><p style="text-align:center;font-size: large;"><span style="font-weight: bold;color: green;">Figure 6. </span> <span style="font-style: italic;">Cooling System Header</span></p>
<div style="width:100%;text-align:center;"><img width="100%" style="border-style:solid;border-color:#1c6e97;" src="doc/coolingHeaderBottomView.jpg"/></div><br>

<p></p><p style="text-align:center;font-size: large;"><span style="font-weight: bold;color: green;">Figure 7. </span> <span style="font-style: italic;">Outlet Cooling System Header<br>From left to right: Temperature cube and tray, 5V power, 24V power, Flow cube and tray</span></p>
<div style="width:100%;text-align:center;"><img width="100%" style="border-style:solid;border-color:#1c6e97;" src="doc/coolingHeaderTopView.jpg"/></div><br>

## Machine protection system
More to come
