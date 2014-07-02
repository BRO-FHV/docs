# BRO - BeagleboaRd OS

![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/logo_transparent.png)

#### Overview

- [Goals](#Goals)
- [Current State](#CurrentState)
- [Todo](#Todo)
- [Team](#Team)
- [Project-Structure](https://github.com/BRO-FHV/docs/blob/master/project-structure.md)
- [Architecture](https://github.com/BRO-FHV/docs/blob/master/architecture.md)
- [Process-Management](https://github.com/BRO-FHV/docs/blob/master/process-management.md)
- [Configuration](https://github.com/BRO-FHV/docs/blob/master/configuration.md)
- [Memory Management Unit](https://github.com/BRO-FHV/docs/blob/master/mmu.md)
- [Client](https://github.com/BRO-FHV/docs/blob/master/client.md)
- [Timer](https://github.com/BRO-FHV/docs/blob/master/timer.md)
- [UDP](https://github.com/BRO-FHV/docs/blob/master/udp.md)
- [Elf](https://github.com/BRO-FHV/docs/blob/master/elf.md)

## <a name="Goals"></a>Goals
This is the documentation for our operating system for ressource limited systems. The basic goal was to implement an OS on a beaglebone bare metal. The basic points are:  

- a monolitic kernel
- applications in php and c
- an event driven application layer 
- use network for communication via TCP and HTTP
- HTML/CSS/JS (client-side) will be delivered to the client and communicate via ajax with the application

Ultimately we should have a light controll and manage the lights in the browser.

## <a name="CurrentState"></a>Current State
The current state of the project contains:

- a hardware abstraction layer 
- drivers for LEDs, GPIO, Serial Port, Timer
- memory managment
- file system
- elf loader
- process scheduler
- library for client applications to communicate with the os
- ethernet component with udp


## <a name="Todo></a>Todo
- porting of LWIP to use TCP/IP which is needed for PHP
- porting of PHP
- implementation of the DMX driver
- refactoring of the HAL :D

### <a name="Team"></a>Team
- [Thomas Gaida](https://github.com/thomasgaida)
- [Stefan Lässer](https://github.com/sla89)
- [Johannes Schwendinger](https://github.com/jotschgl)
- [Johannes Wachter](https://github.com/wachterjohannes)
- [Michael Zangerle](https://github.com/michaelzangerle)
