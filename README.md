# CBT1031
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. GitHub repos will be deleted and created during this period...

```
//***FILE1031 is a set of programs to address and correct an        *   FILE1031
//*           issue of "irregular" ISPF statistics.                 *   FILE1031
//*                                                                 *   FILE1031
//*      email:   sbgolob@cbttape.org   (for support contact)       *   FILE1031
//*                                                                 *   FILE1031
//*      Description of the Problem:                                *   FILE1031
//*                                                                 *   FILE1031
//*           The particular "irregularity" that is addressed, is   *   FILE1031
//*           the packed numeric "create date" and "last changed    *   FILE1031
//*           date", when the packed number ends in X'nC' rather    *   FILE1031
//*           than X'nF'.  The problem rears its ugly head, when    *   FILE1031
//*           a user program tries to display the date and uses     *   FILE1031
//*           an UNPK (unpack) instruction instead of using an      *   FILE1031
//*           EDIT assembler instruction.  If the packed number     *   FILE1031
//*           ends in X'nC', where n is a number from 0 to 9,       *   FILE1031
//*           then the UNPK instruction turns the nibbles around    *   FILE1031
//*           to create the byte X'Cn' (non-numeric) instead of     *   FILE1031
//*           X'Fn', which is numeric.  The non-numeric result      *   FILE1031
//*           ruins subsequent processing.  We wish to detect and   *   FILE1031
//*           correct all such errors:                              *   FILE1031
//*                                                                 *   FILE1031
//*           There are the following programs in this file:        *   FILE1031
//*           The first two are assembler programs, which have      *   FILE1031
//*           to be assembled and linkedited (jobs included).       *   FILE1031
//*           The other three members are CLISTs.                   *   FILE1031
//*                                                                 *   FILE1031
//*      Possible Cause of the Problem:                             *   FILE1031
//*                                                                 *   FILE1031
//*           Whenever "packed arithmetic" is done with packed      *   FILE1031
//*           numbers, such as adding 20 days to a packed date,     *   FILE1031
//*           for example, the result (if positive) is a X'nC'      *   FILE1031
//*           or (if negative) an X'nD'.  The ISPF statistics       *   FILE1031
//*           which are packed fields, are the two dates.  So       *   FILE1031
//*           trying to add or subtract "days", will possibly       *   FILE1031
//*           cause this problem.                                   *   FILE1031
//*                                                                 *   FILE1031
//*      PDSCF    - Read in a PDS and detect if it has irregular    *   FILE1031
//*                 ISPF statistics with packed numbers ending      *   FILE1031
//*                 in "C".  (Assembler Program)                    *   FILE1031
//*                                                                 *   FILE1031
//*      RESETCF  - Change the packed number ending in "C" to a     *   FILE1031
//*                 packed number ending in "F".  Actually to       *   FILE1031
//*                 fix the error indicated by the PDSCF program,   *   FILE1031
//*                 for one pds member.  (Assembler Program)        *   FILE1031
//*                                                                 *   FILE1031
//*      * * * * * * * * * *   USE THIS ONLY   * * * * * * * * *    *   FILE1031
//*      RESETCFF - A CLIST to run RESETCF against every member     *   FILE1031
//*                 of a pds, to change the packed numbers ending   *   FILE1031
//*                 in "C" to a packed number ending in "F".        *   FILE1031
//*      * * * * * * * * * *   USE THIS ONLY   * * * * * * * * *    *   FILE1031
//*                                                                 *   FILE1031
//*      RESETCFI - A CLIST to ren RESETCF just to inquire if any   *   FILE1031
//*                 members have the "bad ISPF stats".  The         *   FILE1031
//*                 program PDSCF is better, but this also works.   *   FILE1031
//*                                                                 *   FILE1031
//*      RESETCFC - A CLIST TO CREATE THE PROBLEM.  DO NOT USE IT   *   FILE1031
//*                 UNLESS YOU WANT TO CREATE THE PROBLEM.  IT      *   FILE1031
//*                 IS BETTER NOT TO EVEN COPY THIS ONE INTO YOUR   *   FILE1031
//*                 CLIST LIBRARY.  (Or change the '&MEMNAM,C'      *   FILE1031
//*                 that is in it, to '&MEMNAM,F' so it fixes       *   FILE1031
//*                 the problem instead of creating it.)            *   FILE1031
//*                                                                 *   FILE1031
```
