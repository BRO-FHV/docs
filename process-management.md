[Back to Overview](https://github.com/BRO-FHV/docs/blob/master/README.md)
## <a name="Process-Management"></a>Process-Management

#### Overview
- [Process-Lifecycle](#Process-Lifecycle) 
- [Process-Event-Management](#Process-Event-Management) 
- [Scheduler](#Scheduler) 

### <a name="Process-Lifecycle"></a>Process Lifecycle
Below you can find a overview over the basic lifecycle of a process.
![Process Lifecycle](https://raw.github.com/BRO-FHV/docs/master/images/ProcessLifecycle.png)

### <a name="Process-Event-Management"></a>Process-Event-Management
Below you can find a overview over the basic functions concerning the event management:

- creating
- register listener
- deregister listener
- emit 
- register emitter
- deregister emitter

![Process-Event-Management](https://raw.github.com/BRO-FHV/docs/master/images/IPC-EventManagement.png)


#### API
```C
bool events_create(char event_name[], int count, processID pid[]);

bool events_register_listener(char event_name[], processID pid);
bool events_deregister_listener(char event_name[], processID pid);

bool events_emit(char event_name[], processID pid, void* data);
bool events_register_emitter(char event_name[], processID pid);
bool events_deregister_emitter(char event_name[], processID pid);
```

The function to __create events__ offers the possibility to limit the number of processes listening  and/or to limit the events to specific process ids.


## <a name="Scheduler"></a> Scheduler
Below you can find a overview over the basic functions concerning the scheduler:
- Process management (start, stop, wait, kill)
- Processswitching

```C
void SchedulerRunNextProcess(Context* context);
void SchedulerStartProcess(processFunc func);
Process* SchedulerCurrentProcess(void);
void KillProcess(processID);
void loadProcessFromElf(uint32_t length, uint8_t* data);
```

The following code segment represents a process.

```C
/*
 * Process structure
 */
typedef struct {
	processID id;
	processState state;
	processFunc func;
	programCounter pc;
	registerCache reg[REG_COUNT];

	/* Control Process Status Register */
	cpsrValue cpsr;

	uint32_t* masterTable;

} Process;
```


###Problems
Because we assigned a wrong parameter to the following function (wrong REG_COUNT) we had some major problems when we switched processes. Because of this bug we lost the process context which resulted in some problems whens loading an elf file.

```C
memcpy(context->reg, gThreads[gRunningThread].reg, REG_COUNT);
```
