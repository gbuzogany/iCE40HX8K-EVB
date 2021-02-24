SHELL = /bin/sh
FPGA_PKG = ct256
FPGA_TYPE = hx8k
PCF = ice40hx8k-evb.pcf
ADD_SRC = example.v

example: example.rpt example.bin

%.json: %.v
	yosys -ql $(subst .json,,$@)-yosys.log -p 'synth_ice40 -top top -json $@' $<

%.asc: %.json
	nextpnr-ice40 --${FPGA_TYPE} --package ${FPGA_PKG} --json $< --pcf ${PCF} --asc $@

%.rpt: %.asc
	icetime -d ${FPGA_TYPE} -mtr $@ $<

%.bin: %.asc
	icepack $< $@

clean:
	rm -f top*.json top*.asc top*.rpt top*.bin top*yosys.log

all: example

.PHONY: all clean