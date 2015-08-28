Installed ns-2.24 on Scientific Linux 5 OS, so some commands are specific to this OS.

s1. Install ns-2.24
s2. Merge ns-2.24_Clustering directory with ../ns-allinone-2.34/ns-2.24 directory (inclusding all sub directories - copy new files manually)
s3. Go to termial ../ns-allinone-2.34/ns-2.24 folder 
s4. Compile our code changes - re-make ns2 file. (make clean and then make)
s5. To run leach, you need to run ./test in termial folder location ../ns-allinone-2.34/ns-2.24 folder.
s6. To run leach, you need to run ./testeecs in termial folder location ../ns-allinone-2.34/ns-2.24 folder.
s7. To run leach, you need to run ./testeeuc in termial folder location ../ns-allinone-2.34/ns-2.24 folder.


Consider eecs:
input parameters will be in file: ../ns-allinone-2.34/ns-2.34/eecs_test
input topology will be in file: ../ns-allinone-2.34/ns-2.34/mit/uAMPS/sims/100nodes.txt
main code of leach will be in file: ../ns-allinone-2.34/ns-2.34/mit/uAMPS/ns-eecs.tcl
out files after running "./testeecs" will be in files: ../ns-allinone-2.34/ns-2.34/mit/leach_sims/eecs.out, ../ns-allinone-2.34/ns-2.34/mit/leach_sims/eecs.energy and ../ns-allinone-2.34/ns-2.34/mit/leach_sims/eecs.data

You can generate multiple topologies using file: ../ns-allinone-2.34/ns-2.34/mit/uAMPS/sims/genscen. 
(get to folder /root/ns-allinone-2.34/ns-2.34/mit/uAMPS/sims in terminal and run command 'genscen')

To generate graphs: In terminal run below script -

awk '{a[$1]+=$3}END{for (i in a) print i,a[i]}' leach.energy >temp
sort -t" " -k1 -nu temp>leach.energyG
awk '{a[$1]+=$3}END{for (i in a) print i,a[i]}' leach.data >temp
sort -t" " -k1 -nu temp>leach.dataG
awk '{a[$1]+=$3}END{for (i in a) print i,a[i]}' leach.alive >temp
sort -t" " -k1 -nu temp>leach.aliveG
awk '{a[$1]+=$3}END{for (i in a) print i,a[i]}' eecs.energy >temp
sort -t" " -k1 -nu temp>eecs.energyG
awk '{a[$1]+=$3}END{for (i in a) print i,a[i]}' eecs.data >temp
sort -t" " -k1 -nu temp>eecs.dataG
awk '{a[$1]+=$3}END{for (i in a) print i,a[i]}' eecs.alive >temp
sort -t" " -k1 -nu temp>eecs.aliveG
awk '{a[$1]+=$3}END{for (i in a) print i,a[i]}' eeuc.energy >temp
sort -t" " -k1 -nu temp>eeuc.energyG
awk '{a[$1]+=$3}END{for (i in a) print i,a[i]}' eeuc.data >temp
sort -t" " -k1 -nu temp>eeuc.dataG
awk '{a[$1]+=$3}END{for (i in a) print i,a[i]}' eeuc.alive >temp
sort -t" " -k1 -nu temp>eeuc.aliveG

Manually 5 different topologoes leach.alive to TotalLeach and use below scripts to get average alive nodes graph:

awk '{a[$1]+=$2}END{for (i in a) print i,a[i]/5}' TotalEECS >temp
sort -t" " -k1 -nu temp>TotalEECSAliveG
awk '{a[$1]+=$2}END{for (i in a) print i,a[i]/5}' TotalLeach >temp
sort -t" " -k1 -nu temp>TotalLeachAliveG
awk '{a[$1]+=$2}END{for (i in a) print i,a[i]/5}' TotalEEUC >temp
sort -t" " -k1 -nu temp>TotalEEUCAliveG

xgraph -x TimeInSecs -y NodesAlive -lw 5 -bg white -fg black -t AvgAliveNodesVsSecond TotalLeachAliveG TotalEECSAliveG TotalEEUCAliveG

Manually 5 different topologoes leach.alive to TotalLeach and use below scripts to get total data reached at base station graph:

awk '{a[$1]+=$2}END{for (i in a) print i,a[i]/5}' TotalEECSData >temp
sort -t" " -k1 -nu temp>TotalEECSDataG
awk '{a[$1]+=$2}END{for (i in a) print i,a[i]/5}' TotalLeachData >temp
sort -t" " -k1 -nu temp>TotalLeachDataG
awk '{a[$1]+=$2}END{for (i in a) print i,a[i]/5}' TotalEEUCData >temp
sort -t" " -k1 -nu temp>TotalEEUCDataG

xgraph -x TimeInSecs -y DataBytes -lw 5 -bg white -fg black -t AvgDataVsSecond TotalLeachDataG TotalEECSDataG TotalEEUCDataG