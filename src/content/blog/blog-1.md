---
title: STM32串口
author: zyr
pubDatetime: 2024-08-01T11:00:00+08:00
slug: blog-1
featured: true
draft: false
tags:
  - stm32
ogImage: ""
description: This is the example description of the example post.
canonicalURL: https://example.org/my-article-was-already-posted-here
---

只能说

## DMA不定长收发

```c
/* USER CODE BEGIN PV */
uint8_t rx_buffer[50] = {0};
extern DMA_HandleTypeDef hdma_usart1_rx;    //如勾选了.c/.h
/* USER CODE END PV */
```

```c
/* 初始化后添加 */
/* USER CODE BEGIN 2 */
HAL_UARTEx_ReceiveToIdle_DMA(&huart1, rx_buffer, sizeof(rx_buffer));
/* 关闭DMA半完成中断 */
__HAL_DMA_DISABLE_IT(&hdma_usart1_rx, DMA_IT_HT);    
/* USER CODE END 2 */
```

```c
/* 回调函数 */
void HAL_UARTEx_RxEventCallback(UART_HandleTypeDef *huart, uint16_t Size)
{
    if (huart == &huart1) {
        HAL_UART_Transmit_DMA(&huart1, rx_buffer, Size);    //发送接收的数据
	    HAL_UARTEx_ReceiveToIdle_DMA(&huart1, rx_buffer, sizeof(rx_buffer));	
	    __HAL_DMA_DISABLE_IT(&hdma_usart1_rx, DMA_IT_HT);		
    }
}
```