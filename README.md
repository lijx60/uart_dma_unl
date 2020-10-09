# uart_dma_unl
这是一个关于串口不定长数据收发的例子。问题卡在：__HAL_UART_GET_FLAG(&huart2,UART_FLAG_IDLE），而应该使用UART_FLAG_RXNE，否则
进入不了中断内的。先调试到这，节后再修改。
