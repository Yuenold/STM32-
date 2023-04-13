# README
延时函数的创建方法
1. 利用NOP指令
```c
//例如MCU系统时钟为72M，那么一条NOP指令约等于1/72us，所以72个NOP约等于1us
void delay_us(u32 nTimer)
{
	u32 i=0;
	for(i=0;i<nTimer;i++){
		__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();
		__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();
		__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();
		__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();
		__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();__NOP();
	}
}
```

2. 利用定时器延时
```c
//利用通用定时器，分频系数72-1，周期1-1，设置好以后开始中断，每1us进入一次中断,在中断中设置变量tick++

void delay_us(uint8_t delay){
    HAL_TIM_Base_Start_IT();
    while(tick<delay);
    tick=0;
    HAL_TIM_Base_Stop_IT();
}



