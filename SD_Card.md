[Back to Overview](https://github.com/BRO-FHV/docs/blob/master/README.md)
## <a name="SD Card"></a>SD Card

This project uses FatFs as file system. It is a generic FAT file system module for small embedded systems.
[FatFs Homepage](http://elm-chan.org/fsw/ff/00index_e.html)


###Features supported
The whole SD part is directly built up on the StarterWare MMCSD Driver
Because of this, the following features are available:

- Support for SD v2.0 standard
- Support for Standard Capacity and High capacity cards
- Support for Standard Speed and High Speed cards
- DMA mode of operation

![StarterWare MMCSD Driver](http://processors.wiki.ti.com/images/2/2c/MMCSDFrameWork.JPG "Source: http://processors.wiki.ti.com/index.php/StarterWare_MMCSD_Driver")

### Changes 
In order to work with the BRO OS some minor changes were necessary.
The whole interrupt had to be reconfigured to use the already implemented interrupt driver of the BRO OS.
Additionally the same was done with the timers and clocks as well as UART.

### Current State
In the current state it is possible to read File from an SD Card. This is done with the elf loading.

### Outlook
For a real usage of SD card functionality some method it is necessary to implement methods that can handle file reading and writing on an higher level. 


### Code Example
The following code example shows how initializing is done 
```c
/**
 * Inits file system and checks for mounted sd
 */
int startFileSystem(void)
{    volatile unsigned int i = 0;
    volatile unsigned int initFlg = 1;
    /* Initialize console for communication with the Host Machine */
    /* Configure the EDMA clocks. */
    EDMAModuleClkConfig();
    /* Configure EDMA to service the HSMMCSD events. */
    HSMMCSDEdmaInit();
    /* Perform pin-mux for HSMMCSD pins. */
    HSMMCSDPinMuxSetup();
    /* Enable module clock for HSMMCSD. */
    HSMMCSDModuleClkConfig();
    /* Basic controller initializations */
    HSMMCSDControllerSetup();
    /* Initialize the MMCSD controller */
    MMCSDCtrlInit(&ctrlInfo);
    MMCSDIntEnable(&ctrlInfo);
    while(1)
    {
        if((HSMMCSDCardPresent(&ctrlInfo)) == 1)
        {
            if(initFlg)
            {
                HSMMCSDFsMount(0, &sdCard);
                initFlg = 0;
            }
            return 1;
        }
		else
		{
			//errorhandling code
		}
    }
}
```



