TITLE_ID = TinyGLL04
TARGET   = TinyGLL04
OBJS     = lesson4.o

LIBS = -lTinyGL -lvita2d -lpsp2shell -lpthread -lSceDisplay_stub -lSceGxm_stub \
	-lSceSysmodule_stub -lSceCtrl_stub -lScePgf_stub -lSceNetCtl_stub -lSceNet_stub -lScePower_stub \
	-lSceCommonDialog_stub -lSceAudio_stub -lSceAppMgr_stub -lfreetype -lpng -ljpeg -lz -lm -lc

PREFIX  = arm-vita-eabi
CC      = $(PREFIX)-gcc
CFLAGS  = -Wl,-q -Wall -O3 -ftree-vectorize -mword-relocations -fomit-frame-pointer -ffast-math \
					-march=armv7-a -mtune=cortex-a9 -mfpu=neon -mfloat-abi=hard
ASFLAGS = $(CFLAGS)

all: $(TARGET).vpk

%.vpk: eboot.bin
	vita-mksfoex -s TITLE_ID=$(TITLE_ID) "$(TARGET)" param.sfo
	vita-pack-vpk -s param.sfo -b eboot.bin $@

eboot.bin: $(TARGET).velf
	vita-make-fself -s $< $@

%.velf: %.elf
	vita-elf-create $< $@

$(TARGET).elf: $(OBJS)
	$(CC) $(CFLAGS) $^ $(LIBS) -o $@

clean:
	@rm -rf $(TARGET).vpk $(TARGET).velf $(TARGET).elf $(OBJS) \
		eboot.bin param.sfo

vpksend: $(TARGET).vpk
	curl -T $(TARGET).vpk ftp://$(PSVITAIP):1337/ux0:/
	@echo "Sent."

send: eboot.bin
	curl -T eboot.bin ftp://$(IP):1337/ux0:/app/$(TITLE_ID)/
	@echo "Sent."
