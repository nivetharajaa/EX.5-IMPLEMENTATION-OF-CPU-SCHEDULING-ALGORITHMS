# EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS

## AIM:
To implement First-Come-First-Serve (FCFS) Scheduling

## ALGORITHM:
1.Start the process
2.Get the number of processes to be inserted
3.Get the value for burst time of each process from the user
4.Having allocated the burst time(bt) for individual processes , Start with the first process from its initial position let other process to be in queue
5.Calculate the waiting time(wt) and turnaround time(tat) as
6.Wt(pi) = wt(pi-1) + tat(pi-1) (i.e. wt of current process = wt of previous process + tat of previous process)
7.tat(pi) = wt(pi) + bt(pi) (i.e. tat of current process = wt of current process + bt of current process)
8.Calculate the total and average waiting time and turnaround time
9.Display the values
10.Stop the process


## PROGRAM:
```
#include<stdio.h>
int main()
{
	int bt[20],p[20],wt[20],tat[20],i,j,n,total=0,pos,temp; float
	avg_wt,avg_tat;
	printf("Enter number of process:");
	scanf("%d",&n);
	printf("\nEnter Burst Time:\n");
	for(i=0;i<n;i++)
	{
		printf("p % d:",i+1);
		scanf("%d",&bt[i]);
		p[i]=i+1; //contains process number
	}
	wt[0]=0; //waiting time for first process will be zero
	//calculate waiting time
	for(i=1;i<n;i++)
	{
		wt[i]=0;
		for(j=0;j<i;j++)
		wt[i]+=bt[j];
		total+=wt[i];
	}
	avg_wt=(float)total/n; //average waiting time
	total=0;
	printf("\nProcess\t Burst Time \tWaiting Time\tTurnaround Time");
	for(i=0;i<n;i++)
	{
		tat[i]=bt[i]+wt[i]; //calculate turnaround time
		total+=tat[i];
		printf("\np%d\t\t %d\t\t %d\t\t\t%d",p[i],bt[i],wt[i],tat[i]);
	}
	avg_tat=(float)total/n; //average turnaround time
	printf("\n\nAverage Waiting Time=%f",avg_wt);
	printf("\nAverage Turnaround Time=%f\n",avg_tat);
}
```


## OUTPUT:
<img width="434" alt="image" src="https://github.com/nivetharajaa/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/120543388/90760f5f-7752-4b5f-aafc-5fda55dd3b79">


## RESULT: First-Come-First-Serve Scheduling is implemented successfully.


## AIM: To implement Shortest Job First (SJF) Preemptive Scheduling

## ALGORITHM:
Initialize variables and arrays to store process information, such as process ID (p), arrival time (at), burst time (bt), start time (st), finish time (ft), waiting time (wt), turnaround time (tt), response ratio (rr), and a flag to mark completed processes (iscompleted).Read the number of processes (n) from the user.Read the process ID, arrival time, and burst time for each process and store them in respective arrays (p, at, bt).Initialize variables, such as nextst (next start time) and counters.

Loop until all processes are completed:

a. Find the process with the minimum burst time among the processes that have arrived and are not completed.

b. Update the start time, finish time, waiting time, and turnaround time for the selected process.

c. Calculate the response ratio (rr) for the selected process (rr = turnaround time / burst time).

d. Mark the selected process as completed.

e. Update the nextst to the finish time of the selected process.Calculate the average waiting time (AWT) and average turnaround time (ATT) by summing up the individual waiting times and turnaround times and dividing by the total number of processes,Display the process information, including process ID, arrival time, burst time, start time, finish time, waiting time, turnaround time, and response ratio.Display the average waiting time and average turnaround time.

## PROGRAM:
```
#include<stdio.h>
int main()
{
int i,n,p[10],st[10],at[10],bt[10],ft[10],wt[10],tt[10];
int nextst,count,minsrt,minpos;
static int  iscompleted[10];
float rr[10],awt=0,att=0;
printf("\n\t SHORTEST JOB FIRST\n\t ******************");
printf("\nEnter the no. of process to be executed : ");
scanf("%d",&n);
printf("\nEnter the process,arrival time and burst time:\n");
for(i=0;i<n;i++)
{
scanf("%d %d %d",&p[i],&at[i],&bt[i]);
}
nextst=0;
for(count=0;count<n;count++)
{
minsrt=100;
minpos=0;
for(i=0;i<n;i++)
{
if(at[i]<=nextst&&iscompleted[i]==0)
{
if(minsrt>bt[i])
{
minsrt=bt[i];
minpos=i;
}
}
}
i=minpos;
st[i]=nextst;
ft[i]=st[i]+bt[i];
wt[i]=st[i]-at[i];
tt[i]=wt[i]+bt[i];
rr[i]=tt[i]/bt[i];
iscompleted[i]=1;
nextst=ft[i];
}
printf("\n---------------------------------------");
printf("\nPRO AT bT ST FT WT TT RR \n");
printf("---------------------------------------\n");
for(i=0;i<n;i++)
{
printf("%3d %2d %2d",p[i],at[i],bt[i]);
printf(" %3d %2d %2d %2d %4.2f\n",st[i],ft[i],wt[i],tt[i],rr[i]);
}
printf("---------------------------------------");
for(i=0;i<n;i++)
{
awt=awt+wt[i];
att=att+tt[i];
}
awt=awt/n;
att=att/n;
printf("\nAverage waiting time is %5.2f",awt);
printf("\nAverage turn around time is %5.2f",att);
}
```
## OUTPUT:
<img width="415" alt="image" src="https://github.com/nivetharajaa/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/120543388/34b4e116-c694-4796-a8c0-406c6dd7ca2c">

## RESULT: 
Shortest Job First (SJF) preemptive scheduling is implemented successfully.


## AIM: To implement Shortest Job First (SJF) Non-Preemptive Scheduling

## ALGORITHM:

Initialize variables and arrays to store process information, such as process ID (process_id), arrival time (arrival_time), burst time (burst_time), completion time (completion_time), waiting time (waiting_time), and turnaround time (turnaround_time).Read the number of processes (n) from the user.Input process information for each process, including arrival time and burst time, and store this information in the respective arrays.Sort the processes based on their arrival times in ascending order using a simple bubble sort algorithm. This step ensures that processes are in the order of their arrival.Initialize the current time (time) to 0.

Perform the scheduling loop for all processes:

a. Find the process with the smallest burst time that has already arrived and is not yet completed. Initialize "shortest_job" to -1 and "shortest_time" to a large initial value.

b. Iterate through the processes, checking if they have arrived and if their burst time is smaller than the current "shortest_time." If so, update "shortest_job" to the current process.

c. If "shortest_job" remains -1, it means no process is available to run at this time. Increment the time by 1.

d. If a process is available (shortest_job != -1), execute the selected process. Update the completion time, waiting time, and turnaround time for this process. Mark the burst time of the completed process as -1 to indicate completion.Display the scheduling information in a tabular format, including Process ID (P), Arrival Time (AT), Burst Time (BT), Completion Time (CT), Waiting Time (WT), and Turnaround Time (TAT) for each process.

## PROGRAM:
```
#include <stdio.h>

int main() {
    int n;
    printf("Enter the number of processes: ");
    scanf("%d", &n);

    int process_id[10];
    int arrival_time[10];
    int burst_time[10];
    int completion_time[10];
    int waiting_time[10];
    int turnaround_time[10];

    // Input process information
    for (int i = 0; i < n; i++) {
        process_id[i] = i + 1;
        printf("Enter arrival time for process %d: ", process_id[i]);
        scanf("%d", &arrival_time[i]);
        printf("Enter burst time for process %d: ", process_id[i]);
        scanf("%d", &burst_time[i]);
    }

    // Perform SJF Non-Preemptive Scheduling
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arrival_time[j] > arrival_time[j + 1]) {
                // Swap arrival_time
                int temp = arrival_time[j];
                arrival_time[j] = arrival_time[j + 1];
                arrival_time[j + 1] = temp;

                // Swap burst_time
                temp = burst_time[j];
                burst_time[j] = burst_time[j + 1];
                burst_time[j + 1] = temp;

                // Swap process_id
                temp = process_id[j];
                process_id[j] = process_id[j + 1];
                process_id[j + 1] = temp;
            }
        }
    }

    int time = 0; // Current time

    for (int i = 0; i < n; i++) {
        // Find the process with the smallest burst time that has arrived
        int shortest_job = -1;
        int shortest_time = 10000; // A large initial value

        for (int j = 0; j < n; j++) {
            if (arrival_time[j] <= time && burst_time[j] < shortest_time && burst_time[j] != -1) {
                shortest_job = j;
                shortest_time = burst_time[j];
            }
        }

        if (shortest_job == -1) {
            // No process is available to run at this time
            time++;
        } else {
            // Execute the selected process
            completion_time[shortest_job] = time + burst_time[shortest_job];
            waiting_time[shortest_job] = completion_time[shortest_job] - arrival_time[shortest_job] - burst_time[shortest_job];
            turnaround_time[shortest_job] = waiting_time[shortest_job] + burst_time[shortest_job];
            time = completion_time[shortest_job];
            burst_time[shortest_job] = -1; // Mark the process as completed
        }
    }

    // Display the scheduling information
    printf("\n-----------------------------------\n");
    printf("Process\tAT\tBT\tCT\tWT\tTAT\n");
    printf("-----------------------------------\n");
    for (int i = 0; i < n; i++) {
        printf("P%d\t%d\t%d\t%d\t%d\t%d\n", process_id[i], arrival_time[i],
               burst_time[i], completion_time[i], waiting_time[i],
               turnaround_time[i]);
    }
    printf("-----------------------------------\n");

    return 0;
}
```
## OUTPUT:
<img width="335" alt="image" src="https://github.com/nivetharajaa/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/120543388/5539eeb1-e0e3-4fb4-a86d-c943733596a1">


## RESULT: Shortest Job First (SJF) Non-preemptive scheduling is implemented successfully.

## AIM: To implement Round Robin (RR) Scheduling

## ALGORITHM:
Initialize variables and arrays to store process information, scheduling data, and status flags. Read the number of processes (n) and the time quantum (tq) from the user.Input process information for each process, including process ID (PRO), arrival time (AT), and burst time (BUT). Also, calculate the total remaining burst time (totalsrt) and create a temporary array (tempsrt) to store the initial burst times. Initialize the queue (queue), front (f), rear (r), and count variables for the ready queue.

Also, initialize the timer to 0. Enqueue processes that arrive at time 0 into the ready queue and mark them as entered (isentered) with count increments.Enter the main scheduling loop, which continues until the timer reaches the total remaining burst time (totalsrt). Dequeue a process from the front of the ready queue (queue[f]) and select it for execution.If the selected process is starting for the first time (isstarted is 0), record its start time (ST) and calculate its waiting time (WT).Execute the process for a time quantum (tq) or until its burst time (BUT) is less than tq, whichever comes first.

Update the timer accordingly. If the process has completed its burst time (BUT becomes 0), record its finish time (FT), calculate its waiting time (WT), turnaround time (TT), and response ratio (RR), and mark it as completed (iscompleted).Check for processes that have arrived and have not entered the ready queue (isentered is 0). Enqueue them into the ready queue with count increments.If the selected process is not completed, enqueue it back into the ready queue Repeat the scheduling loop until the timer reaches totalsrt.

Display the scheduling results, including process ID (PRO), arrival time (AT), initial burst time (BUT), start time (ST), finish time (FT), waiting time (WT), turnaround time (TT), and response ratio (RR) for each process.Calculate and display the average waiting time (AWT) and average turnaround time (ATAT) for all processes.

## PROGRAM:
```
#include <stdio.h>

int main() {
    int n;
    printf("Enter the number of processes: ");
    scanf("%d", &n);

    int process_id[10];
    int arrival_time[10];
    int burst_time[10];
    int completion_time[10];
    int waiting_time[10];
    int turnaround_time[10];

    // Input process information
    for (int i = 0; i < n; i++) {
        process_id[i] = i + 1;
        printf("Enter arrival time for process %d: ", process_id[i]);
        scanf("%d", &arrival_time[i]);
        printf("Enter burst time for process %d: ", process_id[i]);
        scanf("%d", &burst_time[i]);
    }

    // Perform SJF Non-Preemptive Scheduling
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arrival_time[j] > arrival_time[j + 1]) {
                // Swap arrival_time
                int temp = arrival_time[j];
                arrival_time[j] = arrival_time[j + 1];
                arrival_time[j + 1] = temp;

                // Swap burst_time
                temp = burst_time[j];
                burst_time[j] = burst_time[j + 1];
                burst_time[j + 1] = temp;

                // Swap process_id
                temp = process_id[j];
                process_id[j] = process_id[j + 1];
                process_id[j + 1] = temp;
            }
        }
    }

    int time = 0; // Current time

    for (int i = 0; i < n; i++) {
        // Find the process with the smallest burst time that has arrived
        int shortest_job = -1;
        int shortest_time = 10000; // A large initial value

        for (int j = 0; j < n; j++) {
            if (arrival_time[j] <= time && burst_time[j] < shortest_time && burst_time[j] != -1) {
                shortest_job = j;
                shortest_time = burst_time[j];
            }
        }

        if (shortest_job == -1) {
            // No process is available to run at this time
            time++;
        } else {
            // Execute the selected process
            completion_time[shortest_job] = time + burst_time[shortest_job];
            waiting_time[shortest_job] = completion_time[shortest_job] - arrival_time[shortest_job] - burst_time[shortest_job];
            turnaround_time[shortest_job] = waiting_time[shortest_job] + burst_time[shortest_job];
            time = completion_time[shortest_job];
            burst_time[shortest_job] = -1; // Mark the process as completed
        }
    }

    // Display the scheduling information
    printf("\n-----------------------------------\n");
    printf("Process\tAT\tBT\tCT\tWT\tTAT\n");
    printf("-----------------------------------\n");
    for (int i = 0; i < n; i++) {
        printf("P%d\t%d\t%d\t%d\t%d\t%d\n", process_id[i], arrival_time[i],
               burst_time[i], completion_time[i], waiting_time[i],
               turnaround_time[i]);
    }
    printf("-----------------------------------\n");

    return 0;
}
```
## OUTPUT:

![image](https://github.com/nivetharajaa/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/120543388/9d85d382-3406-4731-a107-e9d3ae2af900)



## RESULT: Round Robin (RR) Scheduling is implemented successfully.


## AIM: To implement Priority Preemptive Scheduling

## ALGORITHM:

Initialize variables and arrays to store process information, scheduling data, and status flags. Read the number of processes (n) and the time quantum (tq) from the user.Input process information for each process, including process ID (PRO), arrival time (AT), and burst time (BUT). Also, calculate the total remaining burst time (totalsrt) and create a temporary array (tempsrt) to store the initial burst times. Initialize the queue (queue), front (f), rear (r), and count variables for the ready queue.

Also, initialize the timer to 0. Enqueue processes that arrive at time 0 into the ready queue and mark them as entered (isentered) with count increments.Enter the main scheduling loop, which continues until the timer reaches the total remaining burst time (totalsrt). Dequeue a process from the front of the ready queue (queue[f]) and select it for execution.If the selected process is starting for the first time (isstarted is 0), record its start time (ST) and calculate its waiting time (WT).Execute the process for a time quantum (tq) or until its burst time (BUT) is less than tq, whichever comes first.

Update the timer accordingly. If the process has completed its burst time (BUT becomes 0), record its finish time (FT), calculate its waiting time (WT), turnaround time (TT), and response ratio (RR), and mark it as completed (iscompleted).Check for processes that have arrived and have not entered the ready queue (isentered is 0). Enqueue them into the ready queue with count increments.If the selected process is not completed, enqueue it back into the ready queue Repeat the scheduling loop until the timer reaches totalsrt.

Display the scheduling results, including process ID (PRO), arrival time (AT), initial burst time (BUT), start time (ST), finish time (FT), waiting time (WT), turnaround time (TT), and response ratio (RR) for each process.Calculate and display the average waiting time (AWT) and average turnaround time (ATAT) for all processes.

## PROGRAM:
```
#include<stdio.h>
int main()
{
int n,i,pro[10],at[10],srt[10],st[10],ft[10],wt[10],tt[10];
static int iscompleted[10],isstarted[10],isentered[10];
int queue[10],f,r,count,tq,j,timer,totalsrt,tempsrt[10];
float rr[10],awt=0,atat=0;
printf("\n\t ROUND ROBIN");
printf("\nEnter the no. of process : ");
scanf("%d",&n);

printf("\nEnter the value for Time Quantum: ");
scanf("%d",&tq);
printf("\nEnter the process id for n process: \n");
for(i=0;i<n;i++)
{
scanf("%d",&pro[i]);
}
printf("\nEnter the arrival time for n process: \n");
for(i=0;i<n;i++)
{
scanf("%d",&at[i]);
}
printf("\nEnter the Burst time for n process:\n");
for(i=0;i<n;i++)
{
scanf("%d",&srt[i]);
}
totalsrt=0;
for(i=0;i<n;i++)
{
totalsrt=totalsrt+srt[i];
tempsrt[i]=srt[i];
}
f=0;
r=-1;
count=0;
timer=0;
for(i=0;i<n;i++)
{
if(at[i]==0)
{
r=(r+1)%n;
queue[r]=i;
isentered[i]=1;
count=count+1;
}
}
while(timer<totalsrt)
{
j=queue[f];
f=(f+1)%n;
if(isstarted[j]==0)
{
st[j]=timer;
wt[j]=st[j]-at[j];
isstarted[j]=1;
}
if(srt[j]>=tq)

{
timer=timer+tq;
srt[j]=srt[j]-tq;
}
else
{
timer=timer+srt[j];
srt[j]=srt[j]-srt[j];
}
if(srt[j]==0)
{
ft[j]=timer;
wt[j]=wt[j]+(ft[j]-(st[j]+tempsrt[j]));
tt[j]=wt[j]+tempsrt[j];
rr[j]=(float)tt[j]/tempsrt[j];
iscompleted[j]=1;
}
for(i=0;i<n&&count<n;i++)
{
if(at[i]<=timer&&isentered[i]==0)
{
r=(r+1)%n;
queue[r]=i;
isentered[i]=1;
count=count+1;
}
}
if(iscompleted[j]==0)
{
r=(r+1)%n;
queue[r]=j;
}
}
printf("\n\t CPU SCHEDULING\n\t **************");
printf("\n\t ROUND ROBIN\n\t ***********\n");
printf("------------------------------------------- \n");
printf("PRO AT BUT ST FT WT TT RR");
printf("\n------------------------------------------- \n");
for(i=0;i<n;i++)
{
printf("%3d %2d %2d",pro[i],at[i],tempsrt[i]);
printf(" %3d %3d %2d",st[i],ft[i],wt[i]);
printf(" %3d %4.2f\n",tt[i],rr[i]);
}
printf("------------------------------------------ ");

for(i=0;i<n;i++)
{
awt=awt+wt[i];
atat=atat+tt[i];
}
awt=awt/n;
atat=atat/n;
printf("\nAvg waiting time is %5.2f ",awt );
printf("\nAvg turn around time is %5.2f",atat);
}
```
## OUTPUT:
![image](https://github.com/nivetharajaa/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/120543388/8509a744-f657-4db8-925f-f2b97ad8050a)


## RESULT: 
Priority Preemptive scheduling is implemented successfully.


## AIM: To implement Priority Non-Preemptive Scheduling

## ALGORITHM:
Initialize variables and arrays to store process information, scheduling data, and status flags.Input the number of processes and their details, including process ID (PID), arrival time (AT), burst time (SRT), and priority.Calculate the total remaining burst time (totalsrt) by summing up the burst times of all processes and create a temporary array (tempsrt) to store the initial burst times.Initialize the timer to 0.Enter the main scheduling loop, which continues until all processes have completed execution (i.e., completed variable reaches n).

Within the loop, find the process with the highest priority that has arrived and not yet completed and has the lowest priority (higher priority value).If a process is found, update its start time (ST) and calculate waiting time (WT) if it's starting for the first time (isstarted[i] is 0).Reduce the remaining burst time (SRT) of the selected process by 1, indicating the execution of one time unit.Increment the timer by 1.

If the selected process has completed its execution (SRT becomes 0), update its finish time (FT), waiting time (WT), turnaround time (TT), response ratio (RR), and set the process as completed (iscompleted[i] is 1).Continue this loop until all processes are completed.After scheduling all processes, display the scheduling results in a tabular format, including PID, AT, SRT, ST, FT, WT, TT, RR, and priority for each process.Calculate and display the average waiting time (AWT) and average turnaround time (ATAT) for all processes.

## PROGRAM:
```
#include<stdio.h>
 // structure representing a structure
struct priority_scheduling {

  // name of the process
  char process_name;

  // time required for execution
  int burst_time;

  // waiting time of a process
  int waiting_time;

  // total time of execution
  int turn_around_time;

  // priority of the process
  int priority;
};

int main() {

  // total number of processes
  int number_of_process;

  // total waiting and turnaround time
  int total = 0;

  // temporary structure for swapping
  struct priority_scheduling temp_process;

  // ASCII numbers are used to represent the name of the process
  int ASCII_number = 65;

  // swapping position
  int position;

  // average waiting time of the process
  float average_waiting_time;

  // average turnaround time of the process
  float average_turnaround_time;

  printf("Enter the total number of Processes: ");
  // get the total number of the process as input
  scanf("%d", & number_of_process);

  // initializing the structure array
  struct priority_scheduling process[number_of_process];

  printf("\nPlease Enter the  Burst Time and Priority of each process:\n");

  // get burst time and priority of all process
  for (int i = 0; i < number_of_process; i++) {

    // assign names consecutively using ASCII number
    process[i].process_name = (char) ASCII_number;

    printf("\nEnter the details of the process %c \n", process[i].process_name);
    printf("Enter the burst time: ");
    scanf("%d", & process[i].burst_time);

    printf("Enter the priority: ");
    scanf("%d", & process[i].priority);

    // increment the ASCII number to get the next alphabet
    ASCII_number++;

  }

  // swap process according to high priority
  for (int i = 0; i < number_of_process; i++) {

    position = i;

    for (int j = i + 1; j < number_of_process; j++) {

      // check if priority is higher for swapping
      if (process[j].priority > process[position].priority)
        position = j;
    }
    // swapping of lower priority process with the higher priority process 
    temp_process = process[i];
    process[i] = process[position];
    process[position] = temp_process;
  }
  // First process will not have to wait and hence has a waiting time of 0
  process[0].waiting_time = 0;

  for (int i = 1; i < number_of_process; i++) {
    process[i].waiting_time = 0;
    for (int j = 0; j < i; j++) {
      // calculate waiting time
      process[i].waiting_time += process[j].burst_time;
    }

    // calculate total waiting time             
    total += process[i].waiting_time;
  }

  // calculate average waiting time
  average_waiting_time = (float) total / (float) number_of_process;

  // assigning total as 0 for next calculations
  total = 0;

  printf("\n\nProcess_name \t Burst Time \t Waiting Time \t  Turnaround Time\n");
  printf("------------------------------------------------------------\n");

  for (int i = 0; i < number_of_process; i++) {

    // calculating the turnaround time of the processes
    process[i].turn_around_time = process[i].burst_time + process[i].waiting_time;

    // calculating the total turnaround time.
    total += process[i].turn_around_time;

    // printing all the values
    printf("\t  %c \t\t  %d \t\t %d \t\t %d", process[i].process_name, process[i].burst_time, process[i].waiting_time, process[i].turn_around_time);
    printf("\n-----------------------------------------------------------\n");
  }

  // calculating the average turn_around time 
  average_turnaround_time = (float) total / (float) number_of_process;

  // average waiting time
  printf("\n\n Average Waiting Time : %f", average_waiting_time);

  // average turnaround time
  printf("\n Average Turnaround Time: %f\n", average_turnaround_time);

  return 0;
}
```
## OUTPUT:
![image](https://github.com/nivetharajaa/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/120543388/c351ffaf-3484-486c-b197-bf73a1b1510f)


## RESULT:
Priority Non-preemptive scheduling is implemented successfully.

