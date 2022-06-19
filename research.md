# Research of LE Audio for nrf5340

This file collects information from research done
for LE Audio and more specifically, running it on
one of the Nordic semiconductors nrf5340 developer boards.

# Links

* Main page for nrf5340 Audio application to demonstrate LE Audio.
    * https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/nrf/applications/nrf5340_audio/README.html

* Bluetooth SIG page on LE Audio architecture and the list of different specifications involved in LE Audio.
    * https://www.bluetooth.com/learn-about-bluetooth/recent-enhancements/le-audio/le-audio-specifications/

* Documentation page for "west" Zephyr project's
"meta-tool" (Swiss-army knife CLI)
    * https://docs.zephyrproject.org/latest/develop/west/index.html

* Nordic semiconductors's own documentation page about
Zephy project's "west" CLI.
    * https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/zephyr/develop/west/index.html#west

* Page on "west config" and all the various configuration options
    * https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/zephyr/develop/west/config.html#west-config-cmd

* nrf Connect SKD code base (repositories setup)
    * https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/nrf/dm_code_base.html#dm-code-base

* nrf Command line tools
    * https://www.nordicsemi.com/Products/Development-tools/nRF-Command-Line-Tools

* Running a first test with nrf53 series board (A good starting place, to get starteed with nrf5340 DK)
    * https://infocenter.nordicsemi.com/index.jsp?topic=%2Fug_gsg_ncs%2FUG%2Fgsg%2Ffirst_test.html

* Information about the "Application core", "Network core" setup on the nrf5340 chip
    * https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/nrf/ug_nrf5340.html#id8

* RPC (Remote procedure call) sample for nrf5340, allowing RPC between the "Application and Network -Core"
    * https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/nrf/samples/bluetooth/rpc_host/README.html#ble-rpc-host

# Termonology

ISO - Isochronous channels
CIS - Connected Isochronous Stream
BIS - Broadcast Isochronous Stream

west - Zephyr Project's "meta-tool" (Swiss-army knife CLI)
nrfjprog - tool for programming through SEGGER J-LINK programmers and debuggers

# Developing nrf5340 application

## nrf5340 MCU or CPU?

Since nrf5340 consists of two ARM Cortex-M33 processors/MCU's (Part of the ARM Cortex-M family: https://en.wikipedia.org/wiki/ARM_Cortex-M)
the build output is going to be a .hex file that
is then going to be flashed onto the chip.

## nrf Connect SDK

nrf Connect SDK is the starting point from which to install all of the
tools you'll need to start developing for the nrf5340.

Here is a good link to start with instructions for how to install
nrf Connect SDK and then continuing in how to build and flash the
build-result onto the chip:
https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/nrf/getting_started.html

## Zephyr project

Alot of the example/sample code/applications for nrf5340
is built on Zephyr project's tools, which provides
Driver code, RTOS, lower-parts of bluetooth stack etc.
a lot of different libraries to simplify devellopment for MCU boards.

One way in which you'll notice this is how the CLI
"west" is used quite a lot, which is a product of 
Zephyr project to do all kind of things from building
to flashing it onto your MCU/board.

## nrf5340 Application core and Network core

As I mentioned earlier, the nrf5340 consists of
two ARM Cortex-M33 MCU's.
One of these is the so called "Network core", designed
for ultra-low-power operations.
They recommend that this is used for radio communication
(Like running a bluetooth stack, or just controller
part of bluetooth stack).

The other MCU is called the "Application core" and is
designed for tasks that require high performance and generally speaking, application-level logic.

### What to run on each core?

There are various example/sample firmware's that allows
you to run your code for the nrf5340 in different kind of setups.
For example you can either run the whole bluetooth LE stack on the "Network core" of you can split it up to run just the controller part of the stack on the "Network core" and the host part of the stack on the "Application core".

Read more here: https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/nrf/ug_nrf5340.html#id8

