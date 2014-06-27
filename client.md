[Back to Overview](https://github.com/BRO-FHV/docs/blob/master/README.md)
## <a name="Architecture"></a>The Client
Below you can find a overview over the basic workflow of a client programm. The client programm uses the api_* methods of the library which it self calls the syscall method and results in an software interrupt in the os.

![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/Cilent_Library_Kernel_Interaction.png)

### Software Interrupt
The processes loaded by elf use software interrupts to communicate with the operating system. Therefore we implemented a small library for the client. This library provides a console, led handling, gpio access and udp functions. Below you can find an example for printing text onto the console.


```C
/**
 * Print function alias for standard printf
 */
void lib_print(const char* format, ...) {
	char parsed[API_PRINTF_MAXLENGTH];
	va_list args;
	va_start(args, format);
	vsprintf(parsed, format, args);
	va_end(args);

	SyscallArgData data;
	data.swiNumber = SYSCALL_PRINTF;
	data.arg1 = (uint32_t) & parsed;

	Syscall(&data);
}
```

The abstraction layer provided by the library uses following struct to communicate with the os and supports five arguments and two return values.

```C
typedef struct SyscallArg
{
    uint32_t swiNumber;
    uint32_t arg1;
    uint32_t arg2;
    uint32_t arg3;
    uint32_t arg4;
    uint32_t arg5;
    uint32_t result;
    uint32_t result2;
} SyscallArgData;

#pragma SWI_ALIAS(Syscall, 1)
extern void Syscall(SyscallArgData* data);
```
