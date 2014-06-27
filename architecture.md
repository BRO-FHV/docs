[Back to Overview](https://github.com/BRO-FHV/docs/blob/master/README.md)
## <a name="Architecture"></a>The Architecture
Below you can find an overview over the basic structure of our planned operating system. 
![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/architecture.png)

### Modifications
During development we faced various problems which resulted in some time issues. One of these problems was the porting of LWIP on our system. This specific problem was caused by an unaligned address access and we were not able to solve it. Ultimately we found a solution (partial reimplementation of LWIP code) and got it working so we could at least use UDP. 

Unfortunately to run PHP application we would have needed TCP/IP.

Below you find an updated illustration of our operating system structure.
![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/architecture_update.png)
