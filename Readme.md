# QP/C++ Application with Zephyr

This repository provides an example and a good starting point for deveoping
[QP/C++](https://github.com/QuantumLeaps/qpcpp) applications with Zephyr.

The provided example is the [Dining Philosopher Problem (DPP)](https://www.state-machine.com/qpcpp/tut_dpp.html)
application consisting of muliple Active Objects.

Additionally, the application demonstrates the use of the Zephyr's console UART
to implement [QP/Spy software tracing](https://www.state-machine.com/qtools/qpspy.html).

## Credits
This example application has been originally created by [Victor Chavez](https://github.com/vChavezB).


# Obtaining All Components

### Obtaining QP/C++ Zephyr Module
This example uses QP/C++ packaged as an external [Zephyr module](https://github.com/QuantumLeaps/qpcpp-zephyr).

```bash
git clone https://github.com/QuantumLeaps/qpcpp-zephyr --recurse-submodules
```


### Cloning This QP/C++ Application Example
```bash
git clone https://github.com/QuantumLeaps/qpcpp-zephyr-app --recurse-submodules
```

These two steps should produce the following subfolders in your current directory:

```
<current-dir>
 |
 +- qpcpp-zephyr/      - QP/C++ as Zephyr module
 |
 +- qpcpp-zephyr-app/  - QP/C++ application for zephyr
```

# Building the Project
Change directory to `qpcpp-zephyr-app` and type:

```bash
west build -b <board>
```
specific example for the `nucleo_h743zi` board:
```bash
west build -b nucleo_h743zi
```

## QP/Spy Build Configuration
The [QP/Spy software tracing](https://www.state-machine.com/qtools/qpspy.html) is enabled
by default in `prj.conf` as `CONFIG_QSPY=y`. This is passed to the
[qpcpp-zephyr module](https://github.com/QuantumLeaps/qpcpp-zephyr) and automatically selects
the correct files to build QP/Spy for your Zephyr application. If you don't wish to build with QP/Spy, simply comment out `#CONFIG_QSPY=y` in `prj.conf`.

> NOTE: The QP/Spy software tracing uses the Zephyr's console UART. This means that the Zephyr `printk()` facility cannot be used while QP/Spy is configured.


# Flashing the Board
Connect the board to your host and type:
```bash
west flash
```

# Running the Example


### The QSPY Host Utility
Open a separate terminal and run [qspy host application](https://www.state-machine.com/qtools/qspy.html)
to receive the QP/Spy sotwre tracing output:

> NOTE: You might need to build the QSPY host utility on your machine.
The QSPY utility is available in the [QTools collection](https://github.com/QuantumLeaps/qtools/tree/master/qspy).


```
qspy -c <serial-port>
```
specific example:
```
qspy -c /dev/ttyACM0
```


### Output
After resetting the board, you should see output similar to the following:
```
########## Trg-RST  QP-Ver=701,Build=220810_150847
           Obj-Dict 0x20003154->QS_RX
           Obj-Dict 0x20000680->AO_Table
           Obj-Dict 0x20000180->AO_Philo[0]
           Obj-Dict 0x20000280->AO_Philo[1]
           Obj-Dict 0x20000380->AO_Philo[2]
           Obj-Dict 0x20000480->AO_Philo[3]
           Obj-Dict 0x20000580->AO_Philo[4]
           Obj-Dict 0x0000A52C->timerID
           Usr-Dict 00000100->PHILO_STAT
           Usr-Dict 00000101->PAUSED_STAT
           Usr-Dict 00000102->COMMAND_STAT
           Usr-Dict 00000103->CONTEXT_SW
           Obj-Dict 0x20003054->EvtPool1
           Obj-Dict 0x20000180->Philo::inst[0]
           Obj-Dict 0x2000026C->Philo::inst[0].m_timeEvt
           Obj-Dict 0x20000280->Philo::inst[1]
           Obj-Dict 0x2000036C->Philo::inst[1].m_timeEvt
           Obj-Dict 0x20000380->Philo::inst[2]
           Obj-Dict 0x2000046C->Philo::inst[2].m_timeEvt
           Obj-Dict 0x20000480->Philo::inst[3]
           Obj-Dict 0x2000056C->Philo::inst[3].m_timeEvt
           Obj-Dict 0x20000580->Philo::inst[4]
           Obj-Dict 0x2000066C->Philo::inst[4].m_timeEvt
           Fun-Dict 0x00008929->Philo::initial
           Fun-Dict 0x0000890F->Philo::thinking
           Fun-Dict 0x00008917->Philo::hungry
           Fun-Dict 0x0000891F->Philo::eating
           Sig-Dict 00000004,Obj=0x00000000->TIMEOUT_SIG
0000000327 AO-Subsc Obj=Philo::inst[0],Sig=00000005,Obj=0x20000180
0000000327 AO-Subsc Obj=Philo::inst[0],Sig=00000009,Obj=0x20000180
===RTC===> St-Init  Obj=Philo::inst[0],State=0x00009B1B->Philo::thinking
===RTC===> St-Entry Obj=Philo::inst[0],State=Philo::thinking
0000000328 Init===> Obj=Philo::inst[0],State=Philo::thinking
0000000334 AO-Subsc Obj=Philo::inst[1],Sig=00000005,Obj=0x20000280
0000000334 AO-Subsc Obj=Philo::inst[1],Sig=00000009,Obj=0x20000280
===RTC===> St-Init  Obj=Philo::inst[1],State=0x00009B1B->Philo::thinking
===RTC===> St-Entry Obj=Philo::inst[1],State=Philo::thinking
0000000334 Init===> Obj=Philo::inst[1],State=Philo::thinking
0000000340 AO-Subsc Obj=Philo::inst[2],Sig=00000005,Obj=0x20000380
0000000340 AO-Subsc Obj=Philo::inst[2],Sig=00000009,Obj=0x20000380
===RTC===> St-Init  Obj=Philo::inst[2],State=0x00009B1B->Philo::thinking
===RTC===> St-Entry Obj=Philo::inst[2],State=Philo::thinking
0000000340 Init===> Obj=Philo::inst[2],State=Philo::thinking
0000000346 AO-Subsc Obj=Philo::inst[3],Sig=00000005,Obj=0x20000480
0000000346 AO-Subsc Obj=Philo::inst[3],Sig=00000009,Obj=0x20000480
===RTC===> St-Init  Obj=Philo::inst[3],State=0x00009B1B->Philo::thinking
===RTC===> St-Entry Obj=Philo::inst[3],State=Philo::thinking
0000000346 Init===> Obj=Philo::inst[3],State=Philo::thinking
0000000352 AO-Subsc Obj=Philo::inst[4],Sig=00000005,Obj=0x20000580
0000000352 AO-Subsc Obj=Philo::inst[4],Sig=00000009,Obj=0x20000580
===RTC===> St-Init  Obj=Philo::inst[4],State=0x00009B1B->Philo::thinking
===RTC===> St-Entry Obj=Philo::inst[4],State=Philo::thinking
0000000352 Init===> Obj=Philo::inst[4],State=Philo::thinking
           Obj-Dict 0x20000680->Table::inst
           Sig-Dict 00000006,Obj=0x00000000->DONE_SIG
           Sig-Dict 00000005,Obj=0x00000000->EAT_SIG
           Sig-Dict 00000007,Obj=0x00000000->PAUSE_SIG
           Sig-Dict 00000008,Obj=0x00000000->SERVE_SIG
           Sig-Dict 00000009,Obj=0x00000000->TEST_SIG
           Sig-Dict 00000011,Obj=0x20000680->HUNGRY_SIG
0000000370 AO-Subsc Obj=Table::inst,Sig=DONE_SIG
0000000370 AO-Subsc Obj=Table::inst,Sig=PAUSE_SIG
0000000370 AO-Subsc Obj=Table::inst,Sig=SERVE_SIG
0000000371 AO-Subsc Obj=Table::inst,Sig=TEST_SIG
0000000371 PHILO_STAT 0 thinking
0000000371 PHILO_STAT 1 thinking
0000000371 PHILO_STAT 2 thinking
0000000371 PHILO_STAT 3 thinking
```

