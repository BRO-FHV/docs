[Back to Overview](https://github.com/BRO-FHV/docs/blob/master/README.md)
## <a name="Architecture"></a>The Client
Below you can find a overview over the basic workflow of a client programm. The client programm uses the api_* methods of the library which it self calls the syscall method and results in an software interrupt in the os.

![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/Cilent_Library_Kernel_Interaction.png)
