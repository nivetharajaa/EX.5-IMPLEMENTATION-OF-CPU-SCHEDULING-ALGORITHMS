# EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS

# AIM:
To implement First-Come-First-Serve (FCFS) Scheduling

# ALGORITHM:

    Start the process
    Get the number of processes to be inserted
    Get the value for burst time of each process from the user
    Having allocated the burst time(bt) for individual processes , Start with the first process from its initial position let other process to be in queue
    Calculate the waiting time(wt) and turnaround time(tat) as
    Wt(pi) = wt(pi-1) + tat(pi-1) (i.e. wt of current process = wt of previous process + tat of previous process)
    tat(pi) = wt(pi) + bt(pi) (i.e. tat of current process = wt of current process + bt of current process)
    Calculate the total and average waiting time and turnaround time
    Display the values
    Stop the process

# PROGRAM:
```
EX. 5a) DISK SCHEDULING
FIRST COME FIRST SERVEDate:
AIM:
To write a program for the first come first serve method of disc scheduling.
DESCRIPTION:
Disk scheduling is schedule I/O requests arriving for the disk.
It is important because: -
Multiple I/O requests may arrive by different processes and only one I/O request can be served at a time
by the disk controller. Thus other I/O requests need to wait in the waiting queue and need to be
scheduled.
Two or more request may be far from each other so can result in greater disk head movement.
Hard drives are one of the slowest parts of the computer system and thus need to be accessed in an
efficient manner
FCFS is the simplest of all the Disk Scheduling Algorithms. In FCFS, the requests are addressed in the
order they arrive in the disk queue.
Example: Given the following queue -- 95, 180, 34, 119, 11, 123, 62, 64 with the Read-write head
initially at the track 50 and the tail track being at 199.
PROGRAM:
```
#include <stdio.h>
#include <stdlib.h>
int main()
{
int RQ[100],i,n,TotalHeadMoment=0,initial;
printf ("Enter the number of Requests\n");
scanf("%d",&n);
printf("Enter the Requests sequence\n");
for(i=0;i<n;i++)
scanf("%d",&RQ[i]);
printf("Enter initial head position\n");
scanf("%d",&initial);
for(i=0;i<n;i++)
{
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
initial=RQ[i];
}
printf("Total head moment is %d",TotalHeadMoment);
return 0;
}
```

# OUTPUT:

![image](https://github.com/nivetharajaa/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/120543388/c5def0ef-7fd0-4c5a-adee-fef4900b0d74)


RESULT: First-Come-First-Serve Scheduling is implemented successfully.


AIM: To implement Shortest Job First (SJF) Preemptive Scheduling

ALGORITHM:


PROGRAM:


OUTPUT:


RESULT: Shortest Job First (SJF) preemptive scheduling is implemented successfully.


AIM: To implement Shortest Job First (SJF) Non-Preemptive Scheduling

ALGORITHM:


PROGRAM:


OUTPUT:


RESULT: Shortest Job First (SJF) Non-preemptive scheduling is implemented successfully.

AIM: To implement Round Robin (RR) Scheduling

ALGORITHM:


PROGRAM:


OUTPUT:


RESULT: Round Robin (RR) Scheduling is implemented successfully.


AIM: To implement Priority Preemptive Scheduling

ALGORITHM:


PROGRAM:


OUTPUT:


RESULT: Priority Preemptive scheduling is implemented successfully.


AIM: To implement Priority Non-Preemptive Scheduling

ALGORITHM:


PROGRAM:


OUTPUT:


RESULT: Priority Non-preemptive scheduling is implemented successfully.

