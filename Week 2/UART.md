## UART (Universal Asynchronous Receiver / Transmitter)

We will see how serial communication happens between arduino and esp32.
Let's assume the 1st board is arduino and second board is esp.

![uart](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/UART.png)

- Wires used:2
- Maximum speed:any speed upto 115200,usually 9600.
- Asynchronous
- Serial Communication
- Max:1 Master and 1 Slave

![uart1](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/uart1.png)

![packet](https://github.com/sharvaree1921/Tinkering-Bootcamp)

### Start bit
The UART data transmission line is normally held at a high voltage level when it’s not transmitting
data. To start the transfer of data, the transmitting UART pulls the transmission line from high to
low for one clock cycle. When the receiving UART detects the high to low voltage transition, it
begins reading the bits in the data frame at the frequency of the baud rate.
### Dataframe
The data frame contains the actual data being transferred. It can be 5 bits up to 8 bits long if a
parity bit is used. If no parity bit is used, the data frame can be 9 bits long. In most cases, the data
is sent with the least significant bit first.
### Parity bit
Parity describes the evenness or oddness of a number. The parity bit is a way for the receiving
UART to tell if any data has changed during transmission. Bits can be changed by electromagnetic
radiation, mismatched baud rates, or long distance data transfers. After the receiving UART reads
the data frame, it counts the number of bits with a value of 1 and checks if the total is an even or
odd number. If the parity bit is a 0 (even parity), the 1 bits in the data frame should total to an even
number. If the parity bit is a 1 (odd parity), the 1 bits in the data frame should total to an odd
number. When the parity bit matches the data, the UART knows that the transmission was free of
errors. But if the parity bit is a 0, and the total is odd; or the parity bit is a 1, and the total is even,
the UART knows that bits in the data frame have changed.
### Stop bit
To signal the end of the data packet, the sending UART drives the data transmission line from a
low voltage to a high voltage for at least two bit durations.

### Advantages
● Only uses two wires
● No clock signal is necessary
● Has a parity bit to allow for error checking
● The structure of the data packet can be changed as long as both sides are set up for it
● Well documented and widely used method

### Disadvantages
● The size of the data frame is limited to a maximum of 9 bits
● Doesn’t support multiple slave or multiple master systems
● The baud rates of each UART must be within 10% of each other
