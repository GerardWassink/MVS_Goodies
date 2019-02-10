# HOWTO

## The files
These files must be uploaded using IND$FILE to a member in a PDS under your control. I worked on MVS3.8j TK4- under Hercules, so YMMV... I work on my MVS in the HERC01 user, so do ***NOT*** forget to change the 'HERC01' in the jobs where needed.

### gaw8051	
This is the assembler program, embedded in JCL statements. As a job, it will assemble the program and store the callable subroutine in HERC01.TEST.LOADLIB(GAW8051). This is done at the very end of the job.

### tst8051
This job contains the PL/I program I made to be able to test the assembler program. It contains the hexadecimal print routine and some control info.

## Testing
First adapt (when needed) the gaw8051 job and submit it. Check it for max RC 0000. You now have your callable module. 
Now use the other job and play with it to your heart's content. Change the record and see wether it gets compressed and decompressed back to it's original form.
(spoiler: it will).
