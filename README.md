# uart_dma_unl
这是一个关于串口不定长数据收发的例子。问题卡在：__HAL_UART_GET_FLAG(&huart2,UART_FLAG_IDLE），而应该使用UART_FLAG_RXNE，否则
进入不了中断内的。先调试到这，节后再修改。
STM32的每个串口中断有好几个（发送接收等），但是只要是与串口相关的中断发生系统都会先调用同一个函数，也就是全局中断程序，中断向量表中的那个，比如usart2的话就是USART2_IRQHandler(void)，然后再调用HAL库函数：HAL_UART_IRQHandler；在HAL_UART_IRQHandler中去读取寄存器，判断究竟是哪些位被置为1，以便确定好是哪个中断之后（接收还是发送），最后调用不同的回调函数：HAL_UART_Receive_IT（）。


