[Back to Overview](https://github.com/BRO-FHV/docs/blob/master/README.md)
# Memory Management Unit
## Memory Model
The here given illustration shows the memory model of our BeagleBone boards.
You can find the full description in the AM335x Technical Reference Manual.

![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/memoryMap.png)

The below shown graphic shows the memory concept of our MMU. It shows how we map the physical memory to your virtual memory.
![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/memoryModel.png)


Moreover you can read information about the memory sizes and page numbers listed in the table here.
![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/memoryTable.png)

As you can see we use large pages with 64kb. Our process virtual memory has a size of 1 GB. This allows us to save 16384 pages. With this memory model we are able to manage up to 32 processes. We do not think that we need more than 32 processes for our small operating system.

The next graphic gives information about the components of the physical memory and virtual memory. It shows that the physical memory consists of different regions. Each of these regions has pages. The virtual memory consists of a master table and process tables. With the virtual memory we also handle the logic of page faults.
![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/Komponenten_PM_und_VM.png)

