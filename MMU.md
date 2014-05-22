[Back to Overview](https://github.com/BRO-FHV/docs/blob/master/README.md)
## <a name="MMU"></a>The MMU
#### <a name="MMU_Mem"></a> Memory Model
The here given illustration shows the memory model of our BeagleBone boards.
You can find the full description in the AM335x Technical Reference Manual.

![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/memoryMap.png)

The below shown Graphic shows the memory concept of our MMU. It shows how we map the physical memory to your virtual memory.
![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/memoryModel.png)


Moreover you can read information about the memory sizes and page numbers listed in the table here.
![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/memoryTable.png)

We opted for the use of large pages with 64kb. We choose 
Our page table has a size of 1Gb. This allows us to save 16384 pages in the page table. 
We are able to manage up to xxx processes with our memory model. We do not think that we need more than xxx processes for our small operating system.  
As you can see from the above graphic of our store model, we have opted for the 4 to 1 division. Our operating system receives 1Gb memory. Our VM on the other hand gets 4GB of space.
