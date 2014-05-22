[Back to Overview](https://github.com/BRO-FHV/docs/blob/master/README.md)
## <a name="MMU"></a>The MMU
#### <a name="MMU_Mem"></a> Memory Model
The below shown Graphic shows the memory concept of our MMU. 
![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/architecture.png)


Moreover you can read information about the memory sizes and page numbers listed in the table here.
![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/architecture.png)

We opted for the use of Large Pages with 64kb. Our page table has a size of 1Gb. This allows us to save 16384 pages in the page table. 
