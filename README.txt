cristinel.ababei@ndsu.edu
November 2009, Fargo ND


Synopsis
========
This is the PROPART tool: Efficient event screening for
power systems. It uses the efficient hMetis partitioner to do
partitioning of the power system multiple times (by default
10 times but user can change this via command arguments) with
an increasing number of nodes (buses) "generators" fixed in 
partition 1 and "loads" fixed in partition 2.


How to use the tool
===================
Note: The tool is compiled on a Linux machine running Fedora 8.
It is understood you are working on a linux machine.
Type "part" at the command prompt to see the help menu, copied here:

Usage:   part line_file.dat bus_file.dat [Options...]
Example: part a30.dat b30.dat
Options: [-option val|...] Default. Explanation.
        [-fix_percentage Int] 0. If nonzero, fix specified fraction of nodes.
        [-data_points Int] 10. Count of partitionings explored.
        [-format IEEE|FERC] IEEE. See readme file for details.
        [-verbose 0|1] 0. Print details of execution if set to 1.


Current options:
----------------

-fix_percentage Int
If this argument is not used then the tool will run the partitioning
methodology 10 times; with an increasing percentage of nodes being
fixed in the two partitions: therefore, we collect 10 data points.
If it is used, it requires an integere value between [1..100] as the
percentage of nodes to fix in partitions. The tool will be run only
once, so only one data point will be colleected in this case.
This option is stronger than "-data_points", in the sense that 
the value requested via -data_points argument will not be used.

-data_points Int
Specifies how many data points to collect.
You may use it with a very large number to actually run the tool 
through all possible data points: with a number of fixed nodes 
between 1..max(#generators,#loads)

-format IEEE|FERC
By default the tool expects benchmarks in the IEEE format.
However you can use it with benchmars in the "modified FERC" format. However,
to use it with FERC formats you will have to first use the hidden option
"-converter_mode" to slightly convert your benchmark into a "modified FERC" 
format that we introduced in order to parse it easier inside the tool.

-verbose 0|1
If not used (or used with value 0), then the tool will print minimal info. 
If used with value 1, the tool will print details of each partitioning run.


Examples:
---------

(a) Default runs:

part tests/a57.dat tests/b57.dat
part tests/a118.dat tests/b118.dat
part tests/a2383.dat tests/b2383.dat

part tests2/a_if09s.dat.new tests2/b_if09s.dat.new -format FERC


(b) Custom runs:

part tests/a57.dat tests/b57.dat -data_points 15
part tests/a57.dat tests/b57.dat -fix_percentage 50
part tests/a118.dat tests/b118.dat -data_points 20 -verbose 1
part tests/a2383.dat tests/b2383.dat -data_points 30
part tests/a2383.dat tests/b2383.dat -verbose -fix_percentage 3


Benchmarks
==========
The tool supports two formats. The default format is IEEE.
Please look for examples under tests/ directory.


Copyright
=========
Copyright 2009 by Cristinel Ababei, cristinel.ababei@ndsu.edu
This Copyright notice applies to all files, called hereafter 
"The Software".
Permission to use, copy, and modify this software and its 
documentation is hereby granted only under the following 
terms and conditions.  Both the above copyright notice and 
this permission notice must appear in all copies of the 
software, derivative works or modified versions, and any 
portions thereof, and both notices must appear in supporting 
documentation.  Permission is granted only for non-commercial 
use.  For commercial use, please contact the authors.
This software may be distributed (but not offered for sale 
or transferred for compensation) to third parties, provided 
such third parties agree to abide by the terms and conditions
of this notice.
The Software is provided "as is", and the authors, the 
North Dakota State University (NDSU), as well as any and
all previous authors (of portions or modified portions of
the software) disclaim all warranties with regard to this 
software, including all implied warranties of merchantability
and fitness.  In no event shall the authors or NDSU or any and
all previous authors be liable for any special, direct, 
indirect, or consequential damages or any damages whatsoever
resulting from loss of use, data or profits, whether in an
action of contract, negligence or other tortious action,
arising out of or in connection with the use or performance
of this software.
