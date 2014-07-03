[Back to Overview](https://github.com/BRO-FHV/docs/blob/master/README.md)
## <a name="Timer"></a>Timer
The following sections is explaining the API and the problems we were faced during implementation. 
In the API section we also go into detail and explain some important stuff, that needs to be known when using the timer of our operating system.
Last you can find information about which timer were already used.

### API
The API offers the opportunity to easily configure and enable a specific timer by just using the following enum.
So the user of the timer driver does not need to have knowledge about the hardware address of the timer he/she wants to use.

Here you can see the enum: 
```c
typedef enum {
	Timer_TIMER1MS = 1,
	Timer_TIMER2,
	Timer_TIMER3,
	Timer_TIMER4,
	Timer_TIMER5,
	Timer_TIMER6,
	Timer_TIMER7
} Timer;
```

The first method that needs to be called when you want to use a timer is TimerConfiguration. As parameter you need to pass:
- the Timer (use the enum) you want to configure
- the milliseconds
	- which specify the amount of time after which the first interrupt should be raised
	- and how much time should pass between each interrupt
- the InterruptRoutine, which is called when the interrupt occurs.

In the InterruptRoutine you can do the stuff you want. The interrupt flags and so on is resetted automatically.

Here you can see the API for the configuration:
```c
typedef void (*InterruptRoutine)(void);

int32_t TimerConfiguration(Timer timer, uint32_t milliseconds, InterruptRoutine routine);
```

To start, pause, resume, stop and reset a specific timer you can use the following methods:
```c
int32_t TimerEnable(Timer timer);
int32_t TimerPause(Timer timer);
int32_t TimerContinue(Timer timer);
int32_t TimerStop(Timer timer);
int32_t TimerDisable(Timer timer);
int32_t TimerReset(Timer timer);
```
If a timer is started it runs until it is stopped or paused.

Our system also provides the opportunity to use a lightweight delay timer. The TimerDelaySetup method is called in the main of the OS - so you don't need to call it again.
```c
void TimerDelaySetup();
```

To use the delay timer you can whether use TimerDelayDelay or TimerDelayStart. TimerDelayDelay is a one-shot delay. When the passed milliseconds are over, the timer stops after the interrupt occurred.  This timer is processed as blocking operation - so when the delay timer is started no other code will be executed.
```c
void TimerDelayDelay(uint32_t milliSec);
```

###Used clock
For each timer we use the high frequency system input clock with 32Khz as clock source.

### Problems
The only problem we were faced to was to realize the trigger of the interrupt everytime the set amount of time has passed. The following image gives a clue how we have realized this. The "timer counter register" (=TCRR) is increased automatically and the starting value is equal to the value of the "timer load register" (=TLDR). The value of TLDR is used as reset value of the TCRR after an overflow (means TCRR reached value 0xFFFF FFFF) occurrd. In this case the TCRR value is set to the value of TLDR and the interrupt is triggered (=overflow-interrupt). 

![alt tag](https://raw.github.com/BRO-FHV/docs/master/images/timer.png)
### Which timers are used
- Timer2 is used for the scheduler
- DelayTimer is used for the network configuration
- DelayTimer is used for the sd card initialization
