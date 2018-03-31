#include<stdio.h>
#include<unistd.h>
#include<pthread.h>
#include<fcntl.h>
#include<malloc.h>
static int counter1=0,counter2;
struct man {
	int burst ;
	int arrival;

}z[100];
struct ReadyQueue{
	int burst;
}y[100];
int x=0;
void timer(int a);
void readyQueue(int b,int c);
void execution1(int d);
void sort(int e);
void sjf(int f);
void status(int g);

main()
{	int a,i;
	printf("Welcome user please enter the number of processes");
	scanf("%d",&a);
	int *bt=(int*)malloc(a*sizeof(int));
	int *at=(int*)malloc(a*sizeof(int));
	for(i=0;i<a;i++)
	{

		printf("Enter burst time of process %d : " , i+1);
		scanf("%d" , &z[i].burst);
		printf("Enter the arrival time of process : ",i+1);
		scanf("%d" , &z[i].arrival);
		
	}
	timer(a);
		
	
}

void timer(int a)
{
	int i,z;
	z=0;
	for(i=0;i<20;i++)
	{
		readyQueue(i,a);
		if(y[z].burst!=0 && z<=a )					//&& i<(3*a) no need
		{
			y[z].burst=y[z].burst-1;
			counter1=counter1+1;
		}
		if(x!=0 && (counter1%3==0) && counter2!=counter1)
		{
			z++;
			
			counter2=counter1;
		}
		if(i==19)
		{
			
			printf("\nExecution of step 1 has completed successfully ");
			status(a);
			execution1(a);
		}
	}
	
	
	
}

void readyQueue(int b,int c)
{
	int i;
	
	for(i=0;i<c;i++)
	{
		if(z[i].arrival==b )
		{
			
			y[x].burst=z[i].burst;
			x=x+1;
			
				printf("%d",x);
	//			execution1(x-1);
		}
	}
//	

	
}
void execution1(int d)
{
	int i;
	int j;
	for(i=0;i<d;i++)
	{
		for(j=0;j<6;j++)
		{
			y[i].burst=y[i].burst-1;
			if(y[i].burst==0)
			{goto out;
			}
		
		}
			out:{}
	}
	printf("\nExecution of step 2 has completed successfully ");
	status(d);
	sort(d);

	
}

void sort(int e)
{
	
   int i, j,temp;
   for (i = 0; i < e; i++)      
    {    
       for (j = 0; j < e-i; j++) 
       {
           if (y[j].burst > y[j+1].burst)
           {
              temp=y[j].burst;
              y[j].burst=y[j+1].burst;
              y[j+1].burst=temp;
        	}
        }
    }
	sjf(e);
}

void sjf(int f)
{int a,i;
	for(i=0;i<f;i++)
	{
		if(y[i].burst==0)
		{
			printf("\n process %d completed successfully ",i+1);
		}
		else
		{
			a=y[i].burst;
			y[i].burst=y[i].burst-a;
			printf("\n process %d completed successfully ",i+1);
		}
	}
}

void status(int a)
{
	int i;
	for(i=0;i<a;i++)
	{
		if(y[i].burst==0)
		{
			printf("\n Process %d completed successfully ",i+1);
		}
		else
		{
		
			printf("\n Process %d is in progress : %d",i+1,y[i].burst);
		}
		
	}
}
