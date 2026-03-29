# Flash-Memory-Communications-Protocol-Project


## I. Abstract 
This is a communication protocols based project that emphasizes on the acquisition, storage, and transmission of data. The data collection is performed with a temperature and humidity sensor through I2C and an STM32F446RE MCU. The data is periodically written through SPI to a NOR Flash Memory chip. The flash memory is organized into a File Allocation Table (FAT) - based memory structure, with a file directory and a corresponding table of linked data clusters. The 


## II. SPI Flash Memory
### **#1 void Flash_WriteEnable(void)**
This command is required prior to any writes to memory.
**Write Enable Command:** 0x06
**Process:** Flash CS low (to start communication), Send SPI command, and Flash CS high (to end communication)

### **#2 void Flash_SectorErase(uint32_t address)**
Erases an entire sector of Flash Memory (4kB of memory). Function finishes execution after erasure is fully done.
Sector Erase Command: 0x20
Read Command: 0x05

Process: 
1. Split erasure address into 3 bytes: [address23:16] [address15:8] [address7:0]
2. Transmit the sector erase command and address
3. Transmit read command for "Write In Progress" status until no longer busy (then exit loop)

### **#3 void Flash_ReadData (uint32_t address, uint8_t *buffer, uint16_t length)**
**Sector Erase Command:** 0x03
1. Split erasure address into 3 bytes: [address23:16] [address15:8] [address7:0]
2. Transmit the sector erase command and address
3. Receive 'length' number of bytes from memory, stored into 'buffer'



