#include<stdio.h>
#include<unistd.h>

static int counter1=0,counter2;
struct man {
	int burst ;
	int arrival;
	int id;

}z[100];

struct ReadyQueue{
	int burst;
	int flag;
	int id;
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
	write(1,"Welcome user please enter the number of processes",50);
	scanf("%d",&a);
	write(1,"The arrival time should be less than 15 seconds\n",50);
	for(i=0;i<a;i++)
	{

		printf("\nEnter burst time of process %d : " , i+1);
		scanf("%d" , &z[i].burst);
		printf("Enter the arrival time of process : ",i+1);
		scanf("%d" , &z[i].arrival);
		z[i].id=i+1;
		
	}
	system("cls");
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
			
			write(1,"\nExecution of Round Robin 1 has completed successfully\n ",50);
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
			y[x].id=z[i].id;
			y[x].flag=0;
			x=x+1;
		
			
		
		
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
		
			if(y[i].burst==0)
			{goto out;
			}
			else
			{
					y[i].burst=y[i].burst-1;
			}
		
		}
			out:{}
	}
	write(1,"\n\nExecution of Round Robin 2 has completed successfully \n",50);
	status(d);
	sort(d);

	
}

void sort(int e)
{
	
   int i, j,temp,temp2,temp3;
   for (i = 0; i < e-1; i++)      
    {    
       for (j = 0; j < e-i-1; j++) 
       {
           if (y[j].burst > y[j+1].burst)
           {
              temp=y[j].burst;
              temp2=y[j].id;
              temp3=y[j].flag;
             
              y[j].burst=y[j+1].burst;
              y[j].id=y[j+1].id;
              y[j].flag=y[j+1].flag;
              
              y[j+1].burst=temp;
              y[j+1].id=temp2;
              y[j+1].flag=temp3;
        	}
        }
    }
	sjf(e);
}

void sjf(int f)
{int a,i;
		write(1,"\n\nExecution of step 3 'shortest job first' has completed successfully \n",70);
	for(i=0;i<f;i++)
	{
		if(y[i].burst==0 && y[i].flag ==0)
		{
			printf("\n process %d completed successfully ",y[i].id);
		
		}
		else if(y[i].burst!=0)
		{
			a=y[i].burst;
			y[i].burst=y[i].burst-a;
			printf("\n process %d completed successfully ",y[i].id);
			
		}
	}
}

void status(int a)
{
	int i;
	for(i=0;i<a;i++)
	{
		if(y[i].burst==0 && y[i].flag==0)
		{
			printf("\n Process %d completed successfully ",y[i].id);
			y[i].flag=1;
				
		
		}
		else if(y[i].burst!=0)
		{
		
			printf("\n Process %d is in progress : %d",y[i].id,y[i].burst);
		
		
		}
		
	}
}
