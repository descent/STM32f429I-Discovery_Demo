#Output files
EXECUTABLE=demonstration.elf
BIN_IMAGE=demonstration.bin
#======================================================================#

#Cross Compiler
CC=arm-none-eabi-gcc
OBJCOPY=arm-none-eabi-objcopy

LIB=./Core/Lib

PROGRAM_CONFIG = ./Config
PROGRAM_DEVICE = ./Core/Devices
PROGRAM_USER = ./Core/User
PROGRAM_DEMO = ./Core/Demo
PROGRAM_TEST = ./Core/Test_Program

TOOLCHAIN_PATH ?= /usr/local/csl/arm-2012.03/arm-none-eabi
C_LIB=$(TOOLCHAIN_PATH)/lib/thumb2

CFLAGS=-g -mlittle-endian -mthumb
CFLAGS+=-mcpu=cortex-m4
#CFLAGS+=-mfpu=fpv4-sp-d16 -mfloat-abi=softfp
CFLAGS+=-Wall

#Flash
CFLAGS+=-Wl,-T,stm32_flash.ld

#STM32 CMSIS
CFLAGS+= \
        -D STM32F40XX \
        -D USE_STDPERIPH_DRIVER \
        -D __FPU_PRESENT=1 \
        -D ARM_MATH_CM4

LDFLAGS+=-lm -lc -lgcc

#Lib including
CFLAGS+=-I$(LIB)

#Major programs including
CFLAGS+=-I$(PROGRAM_CONFIG)
CFLAGS+=-I$(PROGRAM_DEVICE)/STM32F4xx
CFLAGS+=-I$(PROGRAM_USER)
CFLAGS+=-I$(PROGRAM_DEMO)
CFLAGS+=-I$(PROGRAM_DEMO)/Res
CFLAGS+=-I$(PROGRAM_TEST)

INC_HEADERS=$(PROGRAM_CONFIG)/*.h \
		$(PROGRAM_DEVICE)/STM32F4xx/*.h \
		$(PROGRAM_USER)/*.h \
		$(PROGRAM_DEMO)/*.h \
		$(PROGRAM_DEMO)/Res/*.h \
		$(PROGRAM_TEST)/*.h

#Major programs source code
SRC+=$(wildcard PROGRAM_DEVICE/*.c)
SRC+=$(wildcard PROGRAM_USER/*.c)
SRC+=$(wildcard PROGRAM_DEMO/*.c)
SRC+=$(wildcard PROGRAM_DEMO/RES/*.c)
SRC+=$(wildcard PROGRAM_TEST/*.c)

#STM32 startup file
STARTUP=./lib/CMSIS/startup_stm32f4xx.s
#======================================================================#

#Make all
all:$(BIN_IMAGE)

$(BIN_IMAGE):$(EXECUTABLE)
	$(OBJCOPY) -O binary $^ $@

STARTUP_OBJ = startup_stm32f4xx.o

$(STARTUP_OBJ): $(STARTUP)
	$(CC) $(CFLAGS) $^ -c $(STARTUP)

$(EXECUTABLE):$(SRC) $(STARTUP_OBJ) ${INC_HEADERS}
	$(CC) $(CFLAGS) $^ -o $@ $(LDFLAGS)

#Make clean
clean:
	rm -rf $(EXECUTABLE)
	rm -rf $(BIN_IMAGE)

#Make flash
flash:
	st-flash write $(BIN_IMAGE) 0x8000000

.PHONY:all clean flash
