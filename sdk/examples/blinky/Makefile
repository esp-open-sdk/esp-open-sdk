CC = xtensa-lx106-elf-gcc

esp8266_sdk_dir := $(abspath $(dir $(word 2,$(shell whereis $(CC))))../../sdk/)/

CFLAGS = -I. -mlongcalls
LDLIBS = -nostdlib -Wl,--start-group -lmain -lnet80211 -lwpa -llwip -lpp -lphy -lc -lcirom -Wl,--end-group -lgcc
LDFLAGS = -L$(esp8266_sdk_dir)/ld -Teagle.app.v6.new.2048.ld

blinky-0x00000.bin: blinky
	esptool.py elf2image $^

blinky: blinky.o

blinky.o: blinky.c

flash: blinky-0x00000.bin
	esptool.py write_flash 0 blinky-0x00000.bin 0x10000 blinky-0x10000.bin

clean:
	rm -f blinky blinky.o blinky-0x00000.bin blinky-0x10000.bin
