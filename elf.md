#Elf Loader

To load new processes we use ELF files. These are loaded from the SD card.

Below you can see the structure of an ELF file.

![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/elf.png)

An ELF file has two views: The program header shows the segments used at run-time, whereas the section header lists the set of sections of the binary.

To load the elf file we look at its header to get positions and size of the program headers and the entry point of the program.
Then we iterate through all program headers, copy their data into memory and map the virtual adresses to the newly allocated memory.

## Example for ELF initialization
Below you find an example for the initialization of an elf file.

```C
// load elf
startFileSystem();
FILINFO fi;

if (f_stat("BRO_UDP.out", &fi) == FR_OK) {
        uint8_t* dataBuff = malloc(fi.fsize);
	getElfFile(dataBuff, fi.fsize, "BRO_UDP.out");

	// start a process
	loadProcessFromElf(0, dataBuff);
	free(dataBuff);
}
```
