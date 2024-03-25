```c
/**
  * Enable DMA controller clock
  * Configure DMA for memory to memory transfers
  *   hdma_memtomem_dma2_stream0
  */
static void MX_DMA_Init(void)
{

  /* DMA controller clock enable */
  __HAL_RCC_DMA2_CLK_ENABLE();

  /* Configure DMA request hdma_memtomem_dma2_stream0 on DMA2_Stream0 */

  // 使用 DMA2 控制器的 数据流 0
  hdma_memtomem_dma2_stream0.Instance = DMA2_Stream0;
  // 配置使用通道 0
  hdma_memtomem_dma2_stream0.Init.Channel = DMA_CHANNEL_0;
  // 传输模式为存储器到存储器
  hdma_memtomem_dma2_stream0.Init.Direction = DMA_MEMORY_TO_MEMORY;
  // 开启外设地址自增
  hdma_memtomem_dma2_stream0.Init.PeriphInc = DMA_PINC_ENABLE;
  // 开启存储器地址自增
  hdma_memtomem_dma2_stream0.Init.MemInc = DMA_MINC_ENABLE;
  // 开始地址宽度
  hdma_memtomem_dma2_stream0.Init.PeriphDataAlignment = DMA_PDATAALIGN_WORD;
  // 存储区地址宽度
  hdma_memtomem_dma2_stream0.Init.MemDataAlignment = DMA_PDATAALIGN_WORD;
  // 传输模式为普通模式
  hdma_memtomem_dma2_stream0.Init.Mode = DMA_NORMAL;
  // 优先级为低
  hdma_memtomem_dma2_stream0.Init.Priority = DMA_PRIORITY_LOW;
  // 开启 FIFO 队列
  hdma_memtomem_dma2_stream0.Init.FIFOMode = DMA_FIFOMODE_ENABLE;
  // FIFO 阈值
  hdma_memtomem_dma2_stream0.Init.FIFOThreshold = DMA_FIFO_THRESHOLD_FULL;
  // 存储器突发？
  hdma_memtomem_dma2_stream0.Init.MemBurst = DMA_MBURST_SINGLE;
  // 外设突发？
  hdma_memtomem_dma2_stream0.Init.PeriphBurst = DMA_PBURST_SINGLE;
  // 初始化 DMA
  if (HAL_DMA_Init(&hdma_memtomem_dma2_stream0) != HAL_OK)
  {
    Error_Handler( );
  }

}
```

```c
void main() {
   // 数据源
   uint32_t srcBuffer[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
   // 目标数据
   uint32_t dstBuffer[10] = {0,0,0,0,0,0,0,0,0,0};
  
   // 开始 DMA 传输
   HAL_DMA_Start(&hdma_memtomem_dma2_stream0, (uint32_t)srcBuffer, (uint32_t)dstBuffer, sizeof(srcBuffer)/sizeof(uint32_t));
}
```
