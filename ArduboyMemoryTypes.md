# Arduboy Memory Types

Basically the Arduboy has three kinds of memory:
* 2.5KB of RAM
  * Can be read and written at runtime
  * The contents are erased when the Arduboy is turned off
* 1KB of EEEPROM
  * Can be read and written at runtime
  * The contents persist after the Arduboy is turned off
* 32KB of Flash (“Progmem”)
  * Can only be read at runtime
    * Except in bootloader mode. The bootloader can write to any other part of Flash, which is how uploading works.
  * The contents persist after the Arduboy is turned off

All the machine code of compiled programs are written to progmem, but data (e.g. arrays and variables) are only stored in progmem if you use 
the `PROGMEM` macro.
(`PROGMEM` actually translates to a special compiler-specific attribute that tells the compiler to put the data in progmem.)

However, data in progmem can’t be read like normal data because the machine code instructions for reading from progmem are different from 
the ones for reading from RAM. So to read from progmem, you have to use [special function macros](https://www.nongnu.org/avr-libc/user-manual/group__avr__pgmspace.html).

Specifically `pgm_read_byte`, `pgm_read_word`, `pgm_read_dword`, `pgm_read_float` and `pgm_read_ptr`.
(There’s also `memcpy_P` for copying blocks of data and several other functions that aren’t as useful.)
