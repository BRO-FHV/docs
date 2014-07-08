# BRO - BeagleboaRd OS

![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/logo_transparent.png)

#### Overview

- [Goals](#Goals)
- [Current State](#CurrentState)
- [Todo](#Todo)
- [Team](#Team)
- [References](#References)
- [Project-Structure](https://github.com/BRO-FHV/docs/blob/master/project-structure.md)
- [Architecture](https://github.com/BRO-FHV/docs/blob/master/architecture.md)
- [Process-Management](https://github.com/BRO-FHV/docs/blob/master/process-management.md)
- [Memory Management Unit](https://github.com/BRO-FHV/docs/blob/master/mmu.md)
- [Client](https://github.com/BRO-FHV/docs/blob/master/client.md)
- [Timer](https://github.com/BRO-FHV/docs/blob/master/timer.md)
- [Networking](https://github.com/BRO-FHV/docs/blob/master/networking.md)
- [Elf](https://github.com/BRO-FHV/docs/blob/master/elf.md)
- [Solution configuration](https://github.com/BRO-FHV/docs/blob/master/configuration.md)

## <a name="Goals"></a>Goals
This is the documentation of our operating system for a resource limited system. The basic goal was to implement a bare metal OS on a BeagleBone.

The basic points are:  

- a monolitic kernel
- applications in PHP and C
- an event driven application layer 
- use network for communication via TCP and HTTP
- HTML/CSS/JS (client-side) will be delivered to the client and communicate via AJAX with the application

Ultimately we should be able to control DMX headlights with our applications via a browser.

## <a name="CurrentState"></a>Current State
The current state of the project contains:

- a hardware abstraction layer 
- drivers for LEDs, GPIO, Serial Port, Timer
- memory managment
- file system
- elf loader
- process scheduler
- library for client applications to communicate with the OS
- Ethernet component with UDP


## <a name="Todo"></a>Todo
- porting of LWIP to use TCP/IP which is needed for PHP
- porting of PHP
- implementation of the DMX driver
- refactoring of the HAL

## <a name="Team"></a>Team

- [Thomas Gaida](https://github.com/thomasgaida)
- [Stefan Lässer](https://github.com/sla89)
- [Johannes Schwendinger](https://github.com/jotschgl)
- [Johannes Wachter](https://github.com/wachterjohannes)
- [Michael Zangerle](https://github.com/michaelzangerle)

## <a name="References"></a>References

BeagleBoard:
* http://beagleboard.org/

University of Applied Sciences Vorarlberg

* http://www.fhv.at