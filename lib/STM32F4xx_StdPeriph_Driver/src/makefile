OBJS=misc.o                 stm32f4xx_dbgmcu.o  stm32f4xx_hash.o       stm32f4xx_rtc.o stm32f4xx_adc.o        stm32f4xx_dcmi.o    stm32f4xx_hash_md5.o   stm32f4xx_sai.o stm32f4xx_can.o        stm32f4xx_dma2d.o   stm32f4xx_hash_sha1.o  stm32f4xx_sdio.o stm32f4xx_crc.o        stm32f4xx_dma.o     stm32f4xx_i2c.o        stm32f4xx_spi.o stm32f4xx_cryp_aes.o   stm32f4xx_exti.o    stm32f4xx_iwdg.o       stm32f4xx_syscfg.o stm32f4xx_cryp.o       stm32f4xx_flash.o   stm32f4xx_ltdc.o       stm32f4xx_tim.o stm32f4xx_cryp_des.o   stm32f4xx_pwr.o        stm32f4xx_usart.o stm32f4xx_cryp_tdes.o  stm32f4xx_fmc.o   stm32f4xx_rcc.o        stm32f4xx_wwdg.o stm32f4xx_dac.o        stm32f4xx_gpio.o    stm32f4xx_rng.o

OTHERS=stm32f4xx_fsmc.o # for STM32F40_41xxx

MYCFLAGS=-fno-common -O0 -g -mcpu=cortex-m3 -mthumb -DSTM32F429_439xx
#MYCFLAGS=-fno-common -O0 -g -mcpu=cortex-m3 -mthumb -DSTM32F40_41xxx
INC=-I../../Config/ -I../../../util/Third_Party/FreeRTOS/Source/include/ -I../../../util/Third_Party/FreeRTOS/Source/portable/GCC/ARM_CM4F/ -I../../../util/STM32F429I-Discovery/ -I../../../lib/CMSIS/Device/ST/STM32F4xx/Include/ -I../../../lib/CMSIS/Include/  \
-I../../../lib/STM32F4xx_StdPeriph_Driver/inc/ \
-I../../../lib/STM32_USB_HOST_Library/Class/MSC/inc \
-I../../../lib/STM32_USB_HOST_Library/Core/inc/ \
-I../../../lib/STM32_USB_OTG_Driver/inc/ \
-I../User/ \
-I../../../util/Third_Party/fat_fs/inc/ \
-I../../../lib/STemWinLibrary522_4x9i/inc/ \
-I../../../lib/STemWinLibrary522_4x9i/Config/ \

TARGET=libstm32f4xx_stdperiph.a
libstm32f4xx_stdperiph.a: $(OBJS)
	arm-none-eabi-ar -rcs $@ $^
%.o: %.c
	arm-none-eabi-gcc $(INC) $(MYCFLAGS) -c $<
	
clean:
	rm -rf *.o $(TARGET) 
