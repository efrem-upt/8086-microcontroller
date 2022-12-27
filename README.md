# 8086-microcontroller

<p align="center">
  <img src="img/8086_microcontroller.png" width = "200" height = "200">
</p>

A simple microcontroller based on the 8086 microprocessor with small applications in Proteus

## Configuration

- 128 KB of SRAM using 4 x 62256 circuits;
- 256 KB of EPROM using 4 x 27C512 circuits;
- Serial communication support using 8251 circuit;
- Parallel communication support using 8255 circuit;
- 8 LEDs
- 6 7 segment displays;
- one minikeyboard.

## Memory map

- 00000H - 0FFFFH: first and second 62256 circuits, each having a capacity of 32K x 8 bits, therefore occupying a memory of 64 KB (bit A0 will be used as the lower / upper memory selection bit); 
- 10000H - 1FFFFH: Third and fourth 62256 circuits, each having the capacity of 32K x 8 bits, therefore occupying a memory of 64 KB (bit A0 will be used as the lower / upper memory selection bit); 
- E0000H - EFFFFH: first and second 27C512 circuits, each having a capacity of 64K x 8 bits, therefore occupying 128 KB of memory; 
- F0000H - FFFFFH: Third and fourth 27C512 circuits, each having a capacity of 64K x 8 bits, therefore occupying 128 KB of memory.

Thus, the SRAM circuits finally occupy 128 KB, and the EPROM 256KB. One memory area addresses two different circuits to facilitate 16-bit data transfer.

## Ports

### 8251 USART
- The data port is at address 0FD0H;
- The command/status port is at address 0FD2H.

### 8253 PIT
- Counter 0 will be at address 08D0H;
- Counter 1 will be at address 08D2H;
- Counter 2 will be at address 08D4H;
- The command and control register will be at the address 08D6H.

### 8255 PPI
- Port A: 0250H;
- Port B: 0252H;
- Port C: 0254H;
- Command word port: 0256H.

### 8 LEDs
- The 8 LEDs are at address 18D0H.

### 6 7 segment displays
- Rank 1: 19D0H;
- Rank 2: 1AD0H;
- Rank 3: 1BD0H;
- Rank 4: 1CD0H;
- Rank 5: 1DD0H;
- Rank 6: 1ED0H.

### Minikeyboard
It has a matrix structure, where the keys are found at the intersection of lines and columns. This will work in the following way: the columns are swept with 0, the first time the first column is set to 0, after the second and so on. If a column is on 0, then pressing any button in that column will cause the diode in the schematic to conduct, so at the input of the 74LS244 buffer there will be about 0.6V (voltage drop across the diode) or logic 0, so it can tell which button was pressed. For example, I set column 1 to 0 and press button 4, then the row corresponding to button 4 will be set to 0.

- Address for setting the mini-keyboard columns: 28D0H;
- Address for retrieving line status: 29D0H;
