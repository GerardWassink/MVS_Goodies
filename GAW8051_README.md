# System/370 compress decompress
A System/370 assembler program to compress and decompress records, callable from PL/I.

## Origin
I wrote this program in 1993 while working for a large bank. There was one file that spanned szeveral disk volumes. It cost the a lot of money for storage. So a program was written in PL/I to compress the records before writing them in that file. This saved some room. I was asked to have a look at that program. Suffice to say it was using a horrible algorithm, only to exclude repeating spaces.

## New algorithm
I set down and created a better algorithm that would compress some more. Obviously it had to compress repeating spaces; but furthermore it would compress all repeating characters and last but not least it would 'ZAP' zoned numeric data to BCD.

## Workings
To be able to process compressed records every area of the record will have to have it's own control code, even the uncompreseed areas. This control code can take one of two forms as shown below. In both cases the dots are placeholders for bits that make up the length of the following area. As can be seen, bit 6 of (the first byte of) the control code indicates wether there is a second length byte.

### for uncompressed data:
- 00......
- 01...... ........


### for compressed data:
- 10tt....
- 11tt.... ........

## Types of compression
In case of compressed data, bis 5 and 4 of (the first byte of) the control code indicate the type of compression ('tt').

### '00' - zoned to BCD
Numeric zoned characters are stored as hexadecimal 'Fn', so '0' to '9' are stored as x'F0' to x'F9' in EBCDIC. Zoned characters can be brought back to their lower nibbles without loss of data like this: x'F0F1F2F3F4F5F6F7' would become x'01234567'.

### '01' - space suppression
For this type a control code suffices. The control code contains a length, and that is the number of spaces that must be re-substituted during decompression.

### '10' - replicating character suppression
This type is almost the same as space suppression, but it has to store one more byte to remember the replicating character.


## Compression process

1) Initialize pointers

2) Find pointers to first field of each compression type

3) Determine which pointer is lowest

4) When appropriate, take over the area up until the smallest pointer, indicating it is an umcompressed field

5) Perform compression of the designated type for the current field

6) find the next area of the same type

7) If not end of record, loop around to 3)

8) Give back control to calling program




