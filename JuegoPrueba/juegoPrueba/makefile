#################################################
#
# This file is part of RA_Amstrad.
# Copyright (C) 2014 Alejandro Almira (@al3x2450)
# RA_Amstrad is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# RA_Amstrad is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with RA_Amstrad. If not, see <http://www.gnu.org/licenses/>.
#
#################################################

# Variables
CC=sdcc
OBJECT_DIR=.obj/
CFLAGS=-o $(OBJECT_DIR) -mz80 --code-loc 0x0138 --data-loc 0 --no-std-crt0 crt0_cpc.rel putchar_cpc.rel
INCLUDE=include/
LIBRARY=-l $(INCLUDE)cpcrslib.lib	
SOURCE_NAME=main
GAME_NAME=$(SOURCE_NAME)

##################################################

# Targets

all: crt0_cpc.rel putchar_cpc.rel cpcrslib_library_correct $(GAME_NAME).dsk clean
$(GAME_NAME).dsk: $(SOURCE_NAME).bin
		iDSK $(GAME_NAME).dsk -n
		iDSK $(GAME_NAME).dsk -i $(OBJECT_DIR)$(SOURCE_NAME).bin -e 0100 -c 0100 -t 1
${SOURCE_NAME}.bin: $(SOURCE_NAME).ihx
		hex2bin $(OBJECT_DIR)$(SOURCE_NAME).ihx
${SOURCE_NAME}.ihx: $(SOURCE_NAME).c
		mkdir -p $(OBJECT_DIR)
		$(CC) $(CFLAGS) $(LIBRARY) $(SOURCE_NAME).c
crt0_cpc.rel: crt0_cpc.s
		sdasz80 -o crt0_cpc.s
putchar_cpc.rel: putchar_cpc.s
		sdasz80 -o putchar_cpc.s
cpctelera_library:
		cd cpctelera && make
cpcrslib_library:
		cd cpcrslib && make
cpcrslib_library_correct:
		cp cpcrslib_br2014/lib/* include/
clean:
		rm -rf crt0_cpc.rel putchar_cpc.rel $(OBJECT_DIR)
