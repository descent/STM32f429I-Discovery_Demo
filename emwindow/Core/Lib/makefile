OBJS=cpu_utils.o  file_utils.o  str_utils.o  time_utils.o

MYCFLAGS=-fno-common -O0 -g -mcpu=cortex-m3 -mthumb
INC=-I../../Config/ -I../../../util/Third_Party/FreeRTOS/Source/include/ -I../../../util/Third_Party/FreeRTOS/Source/portable/GCC/ARM_CM4F/ -I../../../util/STM32F429I-Discovery/ -I../../../lib/CMSIS/Device/ST/STM32F4xx/Include/ -I../../../lib/CMSIS/Include/  \
-I../../../lib/STM32F4xx_StdPeriph_Driver/inc/ \
-I../../../lib/STM32_USB_HOST_Library/Class/MSC/inc \
-I../../../lib/STM32_USB_HOST_Library/Core/inc/ \
-I../../../lib/STM32_USB_OTG_Driver/inc/ \
-I../User/ \
-I../../../util/Third_Party/fat_fs/inc/ \
-I../../../lib/STemWinLibrary522_4x9i/inc/ \
-I../../../lib/STemWinLibrary522_4x9i/Config/ \

libemwin.a: $(OBJS)
	arm-none-eabi-ar -rcs $@ $^
%.o: %.c
	arm-none-eabi-gcc $(INC) $(MYCFLAGS) -DSTM32F429_439xx -c $<
	
clean:
	rm -rf *.o libemwin.a
