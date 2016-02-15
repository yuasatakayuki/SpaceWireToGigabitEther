Overview
--------

SpaceWire-to-GigabitEther is an interface to SpaceWire networks for PC
software via GigabitEthernet. Users can send/receive SpaceWire packets
from/to a user program running on an ordinary PC to/from a SpaceWire
node or router connected to the device. The class library written in C++
is also available for user programs which run on the PC. Using the
library, users can perform Remote Memory Access Protocol (RMAP) to RMAP
Target nodes connected to the converter through the SpaceWire network.
This device is not flight qualified, but originally intended for
SpaceWire/RMAP-based data acquisition system of scientific experiments
and ground tests of flight modules which use SpaceWire interfaces.

Note that there are two types of SpaceWire-to-GigabitEther, one is an
open-source version (FPGA IP and software are open), and the other is a
product version which can be purchased from [Shimafuji
Electric](http://shimafuji.co.jp/spacewire/index.html).

-   Open-source SpaceWire-to-GigabitEther utilizes the ZestET1 board by
    [OrangeTree](http://www.orangetreetech.com/). SpaceWire Open IP (by
    Shimafuji Electric and Osaka University) and Host I/F are
    implemented on the UserFPGA of the board. This board bridges one
    TCP/IP connection to one external SpaceWire port.
-   Shimafuji’s SpaceWire-to-GigabitEther provides very similar
    functionality as what the open-source version implements, but with
    an additional internal SpaceWire router and 4 micro-Dsub (MDM)
    external SpaceWire ports. The Shimafuji SpaceWire-to-GigabitEther
    accepts higher Tx frequencies (up to 200MHz) than the open-source
    version does (\~130MHz).

The both SpaceWire-to-GigabitEther operates as a TCP server which
listens/accepts a connection from a client PC on which user program
runs. When disconnected, the converter goes back to the listening state
and waits for a new connection. The Shimafuji SpaceWire-to-GigabitEther
accepts two TCP/IP connections (identified by TCP/IP port numbers) and
bridges them to separate SpaceWire ports (both connected to the internal
SpaceWire router; see User Guide for details), while one
TCP/IP-SpaceWire bridge is available in the open-source
SpaceWire-to-GigabitEther.

## Open-source SpaceWire-to-GigabitEther
[![](https://github.com/yuasatakayuki/SpaceWireToGigabitEther/wiki/images/SpaceWire-to-GigabitEther_opensource_version-300x201.jpg)](https://github.com/yuasatakayuki/SpaceWireToGigabitEther/wiki/images/SpaceWire-to-GigabitEther_opensource_version)

## Product version from Shimafuji Electric
[![](https://github.com/yuasatakayuki/SpaceWireToGigabitEther/wiki/images/ShimafujiSpaceWire-to-GigabitEther-300x200.jpg)](https://github.com/yuasatakayuki/SpaceWireToGigabitEther/wiki/images/ShimafujiSpaceWire-to-GigabitEther.jpg)

Documents
---------

PDF documents are available in doc/.

Uesr Guide of the open-source
SpaceWire-to-GigabitEther: [SpaceWire-to-GigabitEther\_UesrGuide\_20100930](https://github.com/yuasatakayuki/SpaceWireToGigabitEther/raw/master/doc/SpaceWire-to-GigabitEther_UesrGuide_20100930.pdf)

Hardware specification ofthe Shimafuji
SpaceWire-to-GigabitEther: [SpW-GbE Hardware Spec EN
Rev16\_3-1.pdf](https://github.com/yuasatakayuki/SpaceWireToGigabitEther/raw/master/doc/SpW-GbE-Hardware-Spec-EN-Rev16_3-1.pdf)

Typical usage and performance
-----------------------------

The SpaceWire-to-GigabitEther bridge can be used in applications which
run PC software to control SpaceWire nodes and transfer data from them
to the software.

[![](https://github.com/yuasatakayuki/SpaceWireToGigabitEther/wiki/images/TypicalConfigurationOfSpaceWire-to-GigabitEther.png)](https://github.com/yuasatakayuki/SpaceWireToGigabitEther/wiki/images/TypicalConfigurationOfSpaceWire-to-GigabitEther.png)

The open-source SpaceWire-to-GigabitEther transfers data at 95 Mbps
(max) when the link is operated at 125 MHz. See the user guide for
measurement details.

The Shimafuji SpaceWire-to-GigabitEther transfers data at \~160 Mbps
over a 200-MHz link. The speed reaches the theoretical maximum of
SpaceWire which gives \~80% efficiency due to 8bit-10bit expansion due
to the data/control flag and the parity (see the SpaceWire standard).

Open-source SpaceWire-to-GigabitEther issues
--------------------------------------------

### Block diagram

The figure below presents internal structure of the open-source
SpaceWire-to-GigabitEther FPGA.

[![](https://github.com/yuasatakayuki/SpaceWireToGigabitEther/wiki/images/BlockDiagramOfOpenSourceSpaceWire-to-GigabitEther.png)](https://github.com/yuasatakayuki/SpaceWireToGigabitEther/wiki/images/BlockDiagramOfOpenSourceSpaceWire-to-GigabitEther.png)

### FPGA IP core

Download the latest vernon:

-   VHDL project
    file: [download from vhdl_project/ directory](https://github.com/yuasatakayuki/SpaceWireToGigabitEther/tree/master/vhdl_project)
-   Compiled bit
    file: [download from bit/ directory](https://github.com/yuasatakayuki/SpaceWireToGigabitEther/tree/master/bit_files)
-   Note: The VHDL project file includes the SpaceWire Open IP by
    Shimafuji Electric and Osaka University.
-   Note: The bit file can be directly programmed to the FPGA of ZestET1
    using CPanel.exe provided by OrangeTree (contained in the
    attached CD-ROM). See the section below for details of programming
    the FPGA.

### Circuit of the interface board

The open-source SpaceWire-to-GigabitEther requires an interface board
which converts the FPGA connector to a micro-Dsub 9 or a Dsub 9
connector. The above FPGA project  assumes an interface board whose
circuit is available from

[Circuit\_of\_SpaceWire-to-GigabitEthernet\_Interface\_Board](https://github.com/yuasatakayuki/SpaceWireToGigabitEther/raw/master/doc/Circuit_of_SpaceWire-to-GigabitEthernet_Interface_Board.pdf).

### How to update FPGA IP Core

The FPGA core of SpaceWire-to-GigabitEther can be updated via Ethernet
by a user. Program the latest IP core file (bit file) to the FPGA using
the control panel software CPanel.exe (developed by OrangeTree Tech)
contained in the CD-ROM. No JTAG connection to the board is needed. For
detailed prescriptions, see the section “How to update IP core of the
FPGA on the device” in the user guide.
