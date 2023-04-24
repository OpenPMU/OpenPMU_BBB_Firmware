# OpenPMU BBB Firmware

The OpenPMU V2 system requires a stream of sampled values acquired by an ADC which is disciplined to UTC.  A method for achieving this using a BeagleBone Black, employing its PRUs, is described in this paper:

https://ieeexplore.ieee.org/document/7931698

`X. Zhao, D. M. Laverty, A. McKernan, D. J. Morrow, K. McLaughlin and S. Sezer, "GPS-Disciplined Analog-to-Digital Converter for Phasor Measurement Applications," in IEEE Transactions on Instrumentation and Measurement, vol. 66, no. 9, pp. 2349-2357, Sept. 2017, doi: 10.1109/TIM.2017.2700158.`

The Phase Locked Loop (PLL) in the above paper was improved with a new servo clock design, described in:

https://ieeexplore.ieee.org/document/8543082

`P. Tosato, D. Macii, D. Fontanelli, D. Brunelli and D. Laverty, "A Software-based Low-Jitter Servo Clock for Inexpensive Phasor Measurement Units," 2018 IEEE International Symposium on Precision Clock Synchronization for Measurement, Control, and Communication (ISPCS), 2018, pp. 1-6, doi: 10.1109/ISPCS.2018.8543082.`

Compiling / building the code for the BeagleBone Black and its PRU co-processors is complex, requiring modified device tree overlay (DTO) since several GPIO pins are shared between the PRUs and other peripherals.  The HDMI port must be disabled.

Firmware which achieves the functionality described in the above papers is available via the links below.  Select the firmware appropriate for the nominal power system frequency you wish to monitor.

## Downloads

* [OpenPMU BBB Firmware for 50 Hz Power Systems](https://drive.google.com/file/d/1r1bt4zcM0W5OHiENFCbF1iW5MukKSCy5/view?usp=sharing)
* [OpenPMU BBB Firmware for 60 Hz Power Systems](https://drive.google.com/file/d/1Vg028r7Pduzn5_saI2s_tAkN7W8vPipq/view?usp=sharing)

## Notes

With the above firmware images, it is necessary to use a u-blox GNSS (GPS) module (tested with 6th Gen or later).  These are widely available at low prices.  The firmware will send u-blox configuration messages to setup the GNSS module appropriately.  If another brand of GNSS module is used, the firmware will hang and sampled value data will not be streamed.

*The firmware will NOT work with another brand of GNSS receiver.*

## How to use

1. Unzip the .7z file.  This will create a microSD card image file.  
2. Use a tool such as "Win32 Disk Imager" to image a microSD card.
   * Note, copying the file to a microSD card is not the same as imaging card.
3. Insert the microSD card into the BeagleBone Black (powered off) you wish to image with OpenPMU firmware.
4. Power on the BeagleBone Black.
5. After a few moments, the four blue LEDs on the BeagleBone Black will start to illuminate in a sweeping back and forth pattern.  Wait until this stops.  This step may take several minutes.
6. When the blue LEDs stop sweeping, power down the BeagleBone Black and remove the microSD card.
7. Make sure the GNSS module is attached, and then power up the BeagleBone Black.  It will now start to stream sampled values to the default of 192.168.7.1:48001 (UDP).
   * Note, this assumes use of the USB virtual Ethernet interface on the BeagleBone Black.
   * This is the default setting.  The configuration may be edited to stream data to any IP/Port.

