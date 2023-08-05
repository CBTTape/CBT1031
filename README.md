# CBT1031
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)
This is still a work in progress. GitHub repos will be deleted and created during this period...
~~~~~~~~~~~~~~~~

//***FILE1031 is a set of programs to address an issue of           *   FILE1031
//*           "irregular" ISPF statistics.                          *   FILE1031
//*                                                                 *   FILE1031
//*      email:   sbgolob@cbttape.org   (for support contact)       *   FILE1031
//*                                                                 *   FILE1031
//*      Description of the Problem:                                *   FILE1031
//*                                                                 *   FILE1031
//*           The particular "irregularity" that is addressed, is   *   FILE1031
//*           the packed numeric "create date" and "last changed    *   FILE1031
//*           date", when the packed number ends in X'nC' rather    *   FILE1031
//*           than X'nF'.  The problem occurs when a user program   *   FILE1031
//*           tries to display the date and uses an UNPK (unpack)   *   FILE1031
//*           instruction instead of using an EDIT assembler        *   FILE1031
//*           instruction.  If the packed number ends in X'nC',     *   FILE1031
//*           where n is a number from 0 to 9, then the UNPK        *   FILE1031
//*           instruction turns the nibbles around to create the    *   FILE1031
//*           byte X'Cn' (non-numeric) instead of X'Fn', which is   *   FILE1031
//*           numeric.  The non-numeric result ruins subsequent     *   FILE1031
//*           processing.  We wish to detect and correct all such   *   FILE1031
//*           errors:                                               *   FILE1031
//*                                                                 *   FILE1031
//*           There are the following programs in this file:        *   FILE1031
//*           The first two are assembler programs, which have      *   FILE1031
//*           to be assembled and linkedited (jobs included).       *   FILE1031
//*           The third member is a CLIST.                          *   FILE1031
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
//*                 in "C".                                         *   FILE1031
//*                                                                 *   FILE1031
//*      RESETCF  - Change the packed number ending in "C" to a     *   FILE1031
//*                 packed number ending in "F".  Actually to       *   FILE1031
//*                 fix the error indicated by the PDSCF program,   *   FILE1031
//*                 for one pds member.                             *   FILE1031
//*                                                                 *   FILE1031
//*      RESETCFC - A CLIST to run RESETCF against every member     *   FILE1031
//*                 of a pds, to change the packed numbers ending   *   FILE1031
//*                 in "C" to a packed number ending in "F".        *   FILE1031
//*                                                                 *   FILE1031
~~~~~~~~~~~~~~~~

