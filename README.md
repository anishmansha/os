# os
lab task
                                                                FCFS
#include<iostream>
using namespace std;
 
int main()
{
    int n,BurstT[q],WT[q],TAT[q],avgWt=0,avgTat=0,i,j;
    int q=20;
    cout<<"Enter total number of processes(maximum 20):";
    cin>>n;
 
    cout<<endl;
    cout<<"Enter Process Burst Time”<<endl;
    for(i=0;i<n;i++)
    {
        cout<<"P["<<i+1<<"]:";
        cin>>BurstT[i];
    }
 
    WT[0]=0;     
    for(i=1;i<n;i++)
    {
        WT[I]=0;
        for(j=0;j<i;j++)
            WT[I]+=BurstT[j];
    }
 
    cout<<"\nProcess\t\tBurst Time\tWaiting Time\tTurnaround Time”<<endl;

    for(i=0;i<n;i++)
    {
        TAT[I]=BurstT[i]+WT[I];
        avgWT+=WT[i];
        avgTAT+=TAT[I];
        cout<<"\nP["<<i+1<<"]"<<"\t\t"<<BurstT[i]<<"\t\t"<<WT[I]<<"\t\t"<<TAT[I];
    }
 
    avgWT/=i;
    avgTAT/=i;
    cout<<"\n\nAverage Waiting Time:"<<avgWT;
    cout<<"\nAverage Turnaround Time:"<<avgTAT;
 
    return 0;
}

=======================================================================================================================================
                                                                   SJf
#include<iostream>
using namespace std;

int main()
{   cout<<"\n=====================================";
  
  int p, i, j, sum=0, min, index;
    float awt=0, atat=0;
    
 cout<<"\nEnter The Total Number of Process: ";
    cin>>p;
    
    int proc[p];
    
 int *cbt = new int[p];
    int  *wt = new int[p];
  int  *gc = new int[p];
    int *tat = new int[p];
  int *tmp = new int[p];
    
 cout<<"\nEnter CBT of Process:\n";
    
 for(i=0; i<p; i++)
    {   cin>>cbt[i];
     tmp[i]=cbt[i];
  }
 
  sort(cbt, cbt+p);
  
  cout<<"\n========================================================\n";
    cout<<"\t\tGantt. Chart";
    cout<<"\n========================================================\n";
 
  for(j=0; j<=p; j++)
  {
    min=100;
    for(i=0; i<p; i++)
    {
      if(min>tmp[i]&&tmp[i]!=-1)
      { 
       min=tmp[i];  
       index=i;
      }
   }
   
    gc[j]=sum;
    wt[j]=sum;
    sum+=tmp[index];
    tat[j]=sum;
    tmp[index]=-1;
   
    if(j==p)
     break;
    cout<<'P'<<index+1<<"  |  ";
    proc[j]=index+1;
  } 
    
 cout<<"\n--------------------------------------------------------\n";
 
  sum=0;
  
 for(j=0; j<=p; j++)
  {
    if(gc[j]<10)
      cout<<0;
    cout<<gc[j]<<"    ";
     sum+=gc[j];
  }
  
 cout<<endl;
    
    atat=(sum*1.0)/p;
    
    cout<<"\n--------------------------------------------------------";
    cout<<"\nProcess\t\tCBT\tWaiting Time\tTurn Around Time";
    cout<<"\n--------------------------------------------------------\n";
    
    for(i=0; i<p; i++)
    {
     cout<<"P["<<proc[i]<<"]\t\t"<<cbt[i]<<"\t"<<wt[i]<<"\t\t"<<tat[i]<<endl;
     awt=awt+wt[i];
 }
 awt=(awt*1.0)/p;
 
 cout<<"\n\nTotal Waiting Time: "<<awt;
 cout<<"\n\nTotal Turn Around Time: "<<atat<<endl;
 
 return 0;
}

=======================================================================================================================================
                                                          RoundRobin
#include<iostream> 
using namespace std; 
const int P = 5; 
  

const int R = 3; 

void calculateNeed(int need[P][R], int maxm[P][R], 
                   int allot[P][R]) 
{ 
    // Calculating Need of each P 
    for (int i = 0 ; i < P ; i++) 
        for (int j = 0 ; j < R ; j++) 
  
         
            need[i][j] = maxm[i][j] - allot[i][j]; 
} 

 bool isSafe(int processes[], int avail[], int maxm[][R], 
            int allot[][R]) 
{ 
    int need[P][R]; 
  
    calculateNeed(need, maxm, allot); 

    bool finish[P] = {0}; 

    int safeSeq[P]; 
  
    int work[R]; 
    for (int i = 0; i < R ; i++) 
        work[i] = avail[i]; 

    int count = 0; 
    while (count < P) 
    { 
 
        bool found = false; 
        for (int p = 0; p < P; p++) 
        { 
     
            if (finish[p] == 0) 
            { 
        
                int j; 
                for (j = 0; j < R; j++) 
                    if (need[p][j] > work[j]) 
                        break;  
                if (j == R) 
                { 
                    for (int k = 0 ; k < R ; k++) 
                        work[k] += allot[p][k]; 
  
            
                    safeSeq[count++] = p; 
  
                    // Mark this p as finished 
                    finish[p] = 1; 
  
                    found = true; 
                } 
            } 
        } 
        if (found == false) 
        { 
            cout << "System is not in safe state"; 
            return false; 
        } 
    }  
    cout << "System is in safe state.\nSafe"
         " sequence is: "; 
    for (int i = 0; i < P ; i++) 
        cout << safeSeq[i] << " "; 
  
    return true; 
} 
  

