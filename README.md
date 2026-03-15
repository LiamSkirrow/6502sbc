# 6502 🎉

A minimal implementation of a functional 6502-based system. It has everything that's needed to get going, including a 6522 VIA (for parallel ports/GPIO control) and a 6551 ACIA (for uart connection to a serial terminal).

## Pics or didn't happen
TODO, include screenshots of schematic and PCB. Can I render these automatically based on the current state of the schem/pcb in the repo?

## Memory Map
TODO

## Bootloader
ASM TODO

## Components
TODO

## Tutorial, how to get up and running
TODO, sourcing components, board bring-up, writing your own ASM snippets and loading them into ram via the bootloader+serial chip. How to write your own ISRs etc.

### Development Notes
- consider replacing zero-Ohm resistors with jumper headers, so I can place/replace them without a soldering iron
- add a jumper header to be able to switch between powering the board directly via a 5V USB cable, and an LM7805 linear reg. Three way jumper header to make it impossible to simultaneously select both options.
- rework memory map so that the ROM is only large enough to contain the minimal bootloader (+ a little extra just in case). We only need the ROM to be as large as the bootloader, since the RAM is where the user-code will be loaded into ready for execution, so minimise ROM and maximise RAM util.
- 
