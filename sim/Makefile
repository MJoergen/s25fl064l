# Author:  Michael Jørgensen
#
# Description: Makefile for simulating the axi_wbus.vhd file.

# List of library files
FMF += ../src/conversions.vhd
FMF += ../src/gen_utils.vhd

# List of source files
SRC += ../src/s25fl064l.vhd

# List of simulation files
SRC += spansion_tc_pkg.vhd
SRC += testbench_s25fl064l_vhdl.vhd

# Top level entity
TB = testbench_s25fl064l_vhdl

# Test duration
STOP_TIME = 10ms

# Don't stop on errors
#ASSERT_LEVEL = none

WAVE = $(TB).ghw
SAVE = $(TB).gtkw
LOG  = $(TB).log


################## Don't change anything below here ******************************

WORK_LIB = work-obj93.cf
FMF_LIB  = fmf-obj93.cf

.PHONY: sim
sim: $(TB)
	ghdl -r $(TB) --wave=$(WAVE) | tee $(LOG)

$(TB): $(WORK_LIB) $(FMF_LIB)
	ghdl -m $(TB)

$(FMF_LIB): $(FMF)
	ghdl -i --work=fmf $(FMF)

$(WORK_LIB): $(SRC)
	ghdl -i $(SRC)

.PHONY: show
# Show the waveform of the last simulation
show: $(WAVE)
	gtkwave $(WAVE) $(SAVE)

.PHONY: clean
clean:
	rm -rf *.cf
	rm -rf $(WAVE)

