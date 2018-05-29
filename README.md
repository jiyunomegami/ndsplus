This version of ndsplus detects the original version of the adapter.\
It has only been tested with a few games.\
If you use this, please check that the save file size is correct.

Example Usage
=============

$ ./ndsplus --backup test1.out\
Original NDS Adapter detected.\
Detected save: 64 KiB EEPROM\
Backing up savegame...\
100%   \
Backup to test1.out completed!\
\
$ ./ndsplus --restore test1.out \
Original NDS Adapter detected.\
Detected save: 64 KiB EEPROM\
Restoring savegame...\
100%   \
Restore from file test1.out completed!

How to override the save file size
==================================

Use -s to specify the size.\
If the parameter is less than 32, it is treated as a power of 2.\
For this example, the size is correctly detected as 256 KiB, and 4 copies are written sequentially to the output file.\
\
$ ./ndsplus -s 20 --backup ash.out\
Original NDS Adapter detected.\
Detected save: 256 KiB EEPROM\
Overriding to: 1024 KiB\
Backing up savegame...\
100%   \
Backup to ash.out completed!\
$ for i in $(seq 0 3); do dd bs=256k count=1 if=ash.out of=ash.$i skip=$i; done; for i in $(seq 1 3); do cmp ash.0 ash.$i; done\
1+0 records in\
1+0 records out\
262144 bytes (262 kB, 256 KiB) copied, 0.000437325 s, 599 MB/s\
1+0 records in\
1+0 records out\
262144 bytes (262 kB, 256 KiB) copied, 0.00039962 s, 656 MB/s\
1+0 records in\
1+0 records out\
262144 bytes (262 kB, 256 KiB) copied, 0.000409048 s, 641 MB/s\
1+0 records in\
1+0 records out\
262144 bytes (262 kB, 256 KiB) copied, 0.000419386 s, 625 MB/s

Original ndsplus software
=========================

See https://github.com/Thulinma/ndsplus for the original ndsplus software.
