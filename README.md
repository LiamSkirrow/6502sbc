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
  - perhaps rather than sacrifice a small but fixed amount of memory to the bootloader, why not think of a way to utilise the full 64kB RAM chip once the bootloader has completed. There would need to be some kind of dynamic bank-switching involved, possibly involving one output bit of the 6522 GPIO port to adjust the address decoding to no longer enable the ROM, instead always enabling the RAM (except obviously for when accessing the 6522/6551). So, when the bootloader completes and jumps to the starting address of the user program (in RAM), the first instructions should write to a special GPIO bit that switches out the default decode logic for another logic function that keeps the ROM disabled and RAM enabled. This way, we'd be able to utilise the full ROM space and then when its job is complete we could switch to utilising the full RAM space. So we don't need to use small, fixed regions of memory at any one time, instead using potentially the full capacity of the chip.
