#Output files
EXECUTABLE=emwindow.elf
BIN_IMAGE=emwindow.bin
#======================================================================#

#Cross Compiler
CC=arm-none-eabi-gcc
OBJCOPY=arm-none-eabi-objcopy

#GCC Toolchain
TOOLCHAIN_PATH ?= /usr/local/csl/arm-2012.03/arm-none-eabi

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

#ST emWindow
ST_EMWIN=../lib/STemWinLibrary522_4x9i

#STM32F429I-Discovery Util
STM32F429I_DISCOVERY=../util/STM32F429I-Discovery

#Major programs
PROGRAM_LIB=./Core/Lib
PROGRAM_CONFIG = ./Config
PROGRAM_DEVICE = ./Core/Devices
PROGRAM_USER = ./Core/User
PROGRAM_DEMO = ./Core/Demo
PROGRAM_TEST = ./Core/Test_Program

#STD C Lib
C_LIB=$(TOOLCHAIN_PATH)/lib/thumb2

CFLAGS=-g -mlittle-endian -std=c99
CFLAGS+=-mcpu=cortex-m4 -mthumb
CFLAGS+=-mfpu=fpv4-sp-d16 -mfloat-abi=softfp
CFLAGS+=-Wall

#Flash
CFLAGS+=-Wl,-T,stm32_flash.ld

#STM32 CMSIS
CFLAGS+= \
        -D USE_STDPERIPH_DRIVER \
	-D STM32F429_439xx \
	-D USE_STM32F429I_DISCO \
	-D USE_USB_OTG_HS \
	-D USE_EMBEDDED_PHY
        -D __FPU_PRESENT=1 \
        -D ARM_MATH_CM4

LDFLAGS+=-lm -lc -lgcc

CFLAGS+=-l$(ST_EMWIN)/Lib/STemWin522_4x9i_CM4_OS_GCC.a

#Lib including
#CMSIS
CFLAGS+=-I$(CMSIS)/Include
CFLAGS+=-I$(CMSIS)/Device/ST/STM32F4xx/Include
CFLAGS+=-I$(CMSIS)/RTOS

CFLAGS+=-I$(PERIPH_LIB)/inc

#CFLAGS+=-I../util/Common

CFLAGS+=-I$(ST_EMWIN)/inc
CFLAGS+=-I$(ST_EMWIN)/Config

CFLAGS+=-I$(STM32F429I_DISCOVERY)

CFLAGS+=-I$(USB_DEVICE)/Core/inc
CFLAGS+=-I$(USB_DEVICE)/Class/hid/inc
CFLAGS+=-I$(USB_HOST)/Core/inc
CFLAGS+=-I$(USB_HOST)/Class/MSC/inc
CFLAGS+=-I$(USB_OTG)/inc

CFLAGS+=-I$(FREERTOS_INC)
CFLAGS+=-I$(FREERTOS_PORT_INC)

CFLAGS+=-I$(FATFS_INC)

CFLAGS+=-I$(PROGRAM_LIB)

#Major programs including
CFLAGS+=-I$(PROGRAM_CONFIG)
CFLAGS+=-I$(PROGRAM_DEVICE)/STM32F4xx
CFLAGS+=-I$(PROGRAM_USER)
CFLAGS+=-I$(PROGRAM_DEMO)
CFLAGS+=-I$(PROGRAM_DEMO)/Res
#CFLAGS+=-I$(PROGRAM_TEST)

INC_HEADERS=$(PROGRAM_CONFIG)/*.h \
		$(PROGRAM_DEVICE)/STM32F4xx/*.h \
		$(PROGRAM_USER)/*.h \
		$(PROGRAM_DEMO)/Res/*.h \
#		$(PROGRAM_TEST)/*.h \

#Major programs source code
SRC+=$(wildcard $(PROGRAM_DEVICE)/*.c)
SRC+=$(wildcard $(PROGRAM_USER)/*.c)
SRC+=$(wildcard $(PROGRAM_DEMO)/*.c)
SRC+=$(wildcard $(PROGRAM_DEMO)/RES/*.c)
#SRC+=$(wildcard $(PROGRAM_TEST)/*.c)
#SRC+=$(wildcard ../util/Common/*.c)

SRC+=$(ST_EMWIN)/Config/GUIConf.c \
	$(ST_EMWIN)/OS/GUI_X_FreeRTOS.c

SRC+=$(STM32F429I_DISCOVERY)/stm32f429i_discovery.c \
	$(STM32F429I_DISCOVERY)/stm32f429i_discovery_ioe.c \
	$(STM32F429I_DISCOVERY)/stm32f429i_discovery_l3gd20.c \
	$(STM32F429I_DISCOVERY)/stm32f429i_discovery_lcd.c \
	$(STM32F429I_DISCOVERY)/stm32f429i_discovery_sdram.c

#STM32F4xx Peripherys source code
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

#stm32f4xx_fsmc

SRC+=$(USB_DEVICE)/Class/hid/src/usbd_hid_core.c \
	$(USB_DEVICE)/Core/src/usbd_core.c \
	$(USB_DEVICE)/Core/src/usbd_req.c \
	$(USB_OTG)/src/usb_core.c \
	$(USB_OTG)/src/usb_dcd.c \
	$(USB_OTG)/src/usb_dcd_int.c \
	$(USB_OTG)/src/usb_hcd.c \
	$(USB_OTG)/src/usb_hcd_int.c \
	$(USB_HOST)/Class/MSC/src/usbh_msc_bot.c \
	$(USB_HOST)/Class/MSC/src/usbh_msc_core.c \
	$(USB_HOST)/Class/MSC/src/usbh_msc_scsi.c \
	$(USB_HOST)/Core/src/usbh_core.c \
	$(USB_HOST)/Core/src/usbh_hcs.c \
	$(USB_HOST)/Core/src/usbh_ioreq.c \
	$(USB_HOST)/Core/src/usbh_stdreq.c

SRC+=$(ST_EMWIN)/Config/GUIDRV_stm32f429i_discovery.c

SRC+=$(FATFS_SRC)/ff.c \
	$(FATFS_SRC)/option/syscall.c

SRC+=$(FREERTOS_SRC)/croutine.c \
	$(FREERTOS_SRC)/list.c \
	$(FREERTOS_SRC)/queue.c \
	$(FREERTOS_SRC)/tasks.c \
	$(FREERTOS_SRC)/timers.c \
	$(FREERTOS_SRC)/portable/MemMang/heap_2.c \
	$(FREERTOS_SRC)/portable/GCC/ARM_CM4F/port_cm4.c

#STM32 startup file
STARTUP=./startup_stm32f4xx.s
#======================================================================#

#Make all
all:$(BIN_IMAGE)

$(BIN_IMAGE):$(EXECUTABLE)
	$(OBJCOPY) -O binary $^ $@

STARTUP_OBJ = startup_stm32f4xx.o

$(STARTUP_OBJ): $(STARTUP)
	$(CC) -Wl,--start-group $(CFLAGS) $^ -c $(STARTUP) -Wl,--end-group

$(EXECUTABLE):$(SRC) $(STARTUP_OBJ) ${INC_HEADERS}
	$(CC) -Wl,--start-group $(CFLAGS) $^ -o $@ $(LDFLAGS) -Wl,--end-group

#Make clean
clean:
	rm -rf $(EXECUTABLE)
	rm -rf $(BIN_IMAGE)

#Make flash
flash:
	st-flash write $(BIN_IMAGE) 0x8000000

.PHONY:all clean flash
