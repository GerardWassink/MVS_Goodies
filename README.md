# README

## BLKSIZE
A conversion of the blksize program written by Moshix to Rexx, [see Moshix's MVS repository](https://github.com/moshix/mvs).
I used this to test various things in mgrossman's BREXX implemenation for MVS 3.8.
The program will calculate an optimal block size for files on a specified DASD type and with a given logical record length.

## GAW8051
A System/370 assembler program to compress and decompress records, callable from PL/I. I only had the old listing on paper so I had to type it in all over, but in less then 5 assemblies I had it up and running again. When you have access to an (emulated) mainframe, feel free to try it.

#### GAW8051 History
The old compression routine was written - very badly - in PL/1; yes you CAN write bad programs in PL/1. The files for which this (de-)compression routine was originally written spanned several volumes each. When I was asked to improve it I had a peek at the algorithm and boy, it hurt my eyes to even look at it. It was a sloppy job and it only compressed repeating spaces. That could be vastly improved, both in terms of compression and in terms of processing time.

Ultimately this routine compressed one of those files back to 37% of its original size! It brought the numvber of volumes back (if I remember correctly, from three to just over one). It was also three times faster than the previous one. This saved the department I worked for almost 100.000 Ducth guilders per year in cost, for storage and CPU they had to pay for. 
