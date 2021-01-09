 # ATMega8 single cell voltage reader slave
 Read the voltage of a single cell and transport the data via to the master device
 
 # PIN Assignments
 
 ## Port B
 - PB0 ?
 - PB1 ?
 - PB2 ? SS    | ?
 - PB3 ? MOSI  | ?
 - PB4 ? MISO  | ?
 - PB5 ? SCK   | ?
 - PB6 - XTAL  | 1.8432 MHz Crystal
 - PB7 - XTAL  | 1.8432 MHz Crystal
 
 ## Port C
 - PC0 ?
 - PC1 ?
 - PC2 ?
 - PC3 ?
 - PC4 - SDA   | TWI Data
 - PC5 - SCL   | TWI Clock
 - PC6 - RESET
 
 ## Port D
 - PD0 ? RXD   | ?
 - PD1 ? TXD   | ?
 - PD2 ? INT0  | Wake Up Interrupt
 - PD3 ? INT1  | ?
 - PD4 ?
 - PD5 ?
 - PD6 ?
 - PD7 ?
 
 # TWI - Bekannte Bugs
 Bei einigen ATMEGA Varianten (z.B. ATMEGA8) hat die TWI Implementierung einen Bug. Nach dem Aufwachen aus einem Sleep Modus funktioniert der TWI nicht mehr. Erst ein Reset mit
 
 - TWCR &= ~((1 << TWSTO) | (1 << TWEN));
 - TWCR |= (1 << TWEN);
 nach dem Aufwachen löst das Problem.
 
 Nach dem senden eines "Stop" muß vor erneutem "Start" das TWSTO Bit im TWCR Register auf "0" abgefragt werden. Wenn dies noch eins enthält ist der Stop nicht am Bus wirksam. Ein e    rneuter Start innerhalb dieser Situation bringt statt der "Start" Rückmeldung "$08" die "Restart" Rückmeldung "$10"
