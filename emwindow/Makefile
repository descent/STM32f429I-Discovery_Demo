#Output files
EXECUTABLE=emwindow.elf
BIN_IMAGE=emwindow.bin
#=====================================================================================#

#Cross Compiler
CC=arm-none-eabi-gcc
OBJCOPY=arm-none-eabi-objcopy
#=====================================================================================#

#Path

#CMSIS
CMSIS=../lib/CMSIS

#FreeRTOS
ARCH=CM4F  
FREERTOS_SRC=../util/Third_Party/FreeRTOS/Source
FREERTOS_INC=../util/Third_Party/FreeRTOS/Source/include
FREERTOS_PORT_INC=../util/Third_Party/FreeRTOS/Source/portable/GCC/ARM_$(ARCH)

#FatFS
FATFS_SRC=../util/Third_Party/fat_fs/src
FATFS_INC=../util/Third_Party/fat_fs/inc

#USB
USB_DEVICE=../lib/STM32_USB_Device_Library
USB_HOST=../lib/STM32_USB_HOST_Library
USB_OTG=../lib/STM32_USB_OTG_Driver

#STM32F4xx STD Periph
PERIPH_LIB=../lib/STM32F4xx_StdPeriph_Driver

#Major programs
PROGRAM_LIB=./Core/Lib
PROGRAM_CONFIG=./Config
PROGRAM_DEVICE=./Core/Devices
PROGRAM_USER =./Core/User
PROGRAM_DEMO=./Core/Demo
PROGRAM_TEST=./Core/Test_Program

#ST emWindow
ST_EMWIN=../lib/STemWinLibrary522_4x9i

#STM32F429I-Discovery Util
STM32F429I_DISCOVERY=../util/STM32F429I-Discovery

STARTUP=./startup_stm32f429_439xx.s
#=====================================================================================#

#Compiling information

LIBS=-lm
CFLAGS=-g -std=c99 -mlittle-endian -mthumb
CFLAGS+=-mcpu=cortex-m4 -DSTM32F429_439xx

#FPU
CFLAGS+=-DARM_MATH_CM4 -D__FPU_PRESENT
CFLAGS+=-mfpu=fpv4-sp-d16 -mfloat-abi=hard

#Flash
CFLAGS+=-DVECT_TAB_FLASH
CFLAGS+=-Wl,-T,stm32f429zi_flash.ld

SRC+=$(STARTUP)

#CMSIS
CFLAGS+=-I$(CMSIS)/Device/ST/STM32F4xx/Include
CFLAGS+=-I$(CMSIS)/Include
SRC+=$(CMSIS)/Lib/GCC/libarm_cortexM4lf_math.a

#ST emWindow
CFLAGS+=-I$(ST_EMWIN)/Config
SRC+=$(ST_EMWIN)/Config/*.c
CFLAGS+=-I$(ST_EMWIN)/inc
SRC+=$(ST_EMWIN)/Lib/STemWin522_4x9i_CM4_OS_GCC.a
SRC+=$(ST_EMWIN)/OS/*.c

#STM32F4xx STD Periph
CFLAGS+=-DUSE_STDPERIPH_DRIVER
CFLAGS+=-I$(PERIPH_LIB)/inc
SRC+=$(PERIPH_LIB)/src/misc.c \
	$(PERIPH_LIB)/src/stm32f4xx_adc.c \
	$(PERIPH_LIB)/src/stm32f4xx_dcmi.c \
	$(PERIPH_LIB)/src/stm32f4xx_dma.c \
	$(PERIPH_LIB)/src/stm32f4xx_dma2d.c \
	$(PERIPH_LIB)/src/stm32f4xx_exti.c \
	$(PERIPH_LIB)/src/stm32f4xx_flash.c \
	$(PERIPH_LIB)/src/stm32f4xx_fmc.c \
	$(PERIPH_LIB)/src/stm32f4xx_gpio.c \
	$(PERIPH_LIB)/src/stm32f4xx_i2c.c \
	$(PERIPH_LIB)/src/stm32f4xx_ltdc.c \
	$(PERIPH_LIB)/src/stm32f4xx_pwr.c \
	$(PERIPH_LIB)/src/stm32f4xx_rcc.c \
	$(PERIPH_LIB)/src/stm32f4xx_rng.c \
	$(PERIPH_LIB)/src/stm32f4xx_rtc.c \
	$(PERIPH_LIB)/src/stm32f4xx_sdio.c \
	$(PERIPH_LIB)/src/stm32f4xx_spi.c \
	$(PERIPH_LIB)/src/stm32f4xx_tim.c \
	$(PERIPH_LIB)/src/stm32f4xx_usart.c

#USB_DEVICE
CFLAGS+=-I$(USB_DEVICE)/Core/inc
SRC+=$(USB_DEVICE)/Core/src/*.c
#CFLAGS+=-I$(USB_DEVICE)/Class/audio/inc
#SRC+=$(USB_DEVICE)/Class/audio/src/*.c
#CFLAGS+=-I$(USB_DEVICE)/Class/cdc/inc
#SRC+=$(USB_DEVICE)/Class/cdc/src/*.c
#CFLAGS+=-I$(USB_DEVICE)/Class/dfu/inc
#SRC+=$(USB_DEVICE)/Class/dfu/src/*.c
CFLAGS+=-I$(USB_DEVICE)/Class/hid/inc
SRC+=$(USB_DEVICE)/Class/hid/src/*.c
CFLAGS+=-I$(USB_DEVICE)/Class/msc/inc
SRC+=$(USB_DEVICE)/Class/msc/src/*.c

#USB_HOST
CFLAGS+=-I$(USB_HOST)/Core/inc
SRC+=$(USB_HOST)/Core/src/*.c
CFLAGS+=-I$(USB_HOST)/Class/HID/inc
SRC+=$(USB_HOST)/Class/HID/src/*.c
CFLAGS+=-I$(USB_HOST)/Class/MSC/inc
SRC+=$(USB_HOST)/Class/MSC/src/*.c

#USB_OTG
CFLAGS+=-I$(USB_OTG)/inc
#SRC+=$(USB_OTG)/src/*.c

#Common

#STM32F429I-Discovery
CFLAGS+=-I$(STM32F429I_DISCOVERY)
SRC+=$(STM32F429I_DISCOVERY)/stm32f429i_discovery.c \
	$(STM32F429I_DISCOVERY)/stm32f429i_discovery_ioe.c \
	$(STM32F429I_DISCOVERY)/stm32f429i_discovery_l3gd20.c \
	$(STM32F429I_DISCOVERY)/stm32f429i_discovery_lcd.c \
	$(STM32F429I_DISCOVERY)/stm32f429i_discovery_sdram.c


CFLAGS+=-I$(FATFS_INC)
SRC+=$(FATFS_SRC)/ff.c

CFLAGS+=-I$(FREERTOS_INC)
CFLAGS+=-I$(FREERTOS_PORT_INC)
SRC+=$(FREERTOS_SRC)/croutine.c \
	$(FREERTOS_SRC)/list.c \
	$(FREERTOS_SRC)/queue.c \
	$(FREERTOS_SRC)/tasks.c \
	$(FREERTOS_SRC)/timers.c \
	$(FREERTOS_SRC)/portable/MemMang/heap_2.c \
	$(FREERTOS_SRC)/portable/GCC/ARM_CM4F/port_cm4.c

#Major programs
CFLAGS+=-I$(PROGRAM_CONFIG)
CFLAGS+=-I$(PROGRAM_LIB)
SRC+=$(PROGRAM_LIB)/*.c
CFLAGS+=-I$(PROGRAM_DEVICE)/STM32F4xx
SRC+=$(PROGRAM_DEVICE)/STM32F4xx/*.c
CFLAGS+=-I$(PROGRAM_USER)
SRC+=$(PROGRAM_USER)/*.c
CFLAGS+=-I$(PROGRAM_DEMO)
SRC+=$(PROGRAM_DEMO)/*.c
CFLAGS+=-I$(PROGRAM_DEMO)/Res
SRC+=$(PROGRAM_DEMO)/Res/*.c
CFLAGS+=-I$(PROGRAM_TEST)
SRC+=$(PROGRAM_TEST)/*.c
#=====================================================================================#

#Make all
all:$(BIN_IMAGE)

$(BIN_IMAGE):$(EXECUTABLE)
	$(OBJCOPY) -O binary $^ $@

$(EXECUTABLE):$(SRC)
	$(CC) -o $@ -Wl,--start-group $(CFLAGS) $^ $(LIBS) -Wl,--end-group

#Make clean
clean:
	rm -rf $(EXECUTABLE)
	rm -rf $(BIN_IMAGE)

#Make flash
flash:
	st-flash write $(BIN_IMAGE) 0x8000000

.PHONY:all clean flash
