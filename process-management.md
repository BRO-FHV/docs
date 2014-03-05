[Back to Overview](https://github.com/BRO-FHV/docs/blob/master/README.md)
## <a name="Process-Management"></a>Process-Management

#### Overview
- [Process-Event-Management](#Process-Event-Management) 
- [Process-Lifecycle](#Process-Lifecycle) 
- ...

### <a name="Process-Lifecycle"></a>Process Lifecycle
Below you can find a overview over the basic lifecycle of a process.
![Process Lifecycle](https://raw.github.com/BRO-FHV/docs/master/images/ProcessLifecycle.png)

### <a name="Process-Event-Management"></a>Process-Event-Management
Below you can find a overview over the basic creating, listening (on) and firing (emit) of events.
The function to __create events__ offers the possibility to limit the number of processes listenting and/or to limit the events to specific process ids.

```C
bool events_on(char event_name[], processID pid);
bool events_emit(char event_name[], processID pid);
bool events_create(char event_name[], int count, processID pid[]);
```

![Process-Event-Management](https://raw.github.com/BRO-FHV/docs/master/images/IPC-EventManagement.png)
