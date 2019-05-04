# AUTHOR: HAOCHEN GOU

#include<stdio.h>


/*define the struct of job */
struct jobs{
 		short id;
  		int processing_time[3]; // the three processing times
		int machineA;  // the stage-1 machine selected
		int start_time[3];  // the start time on the three machines
		int johnson_B;   //use to check if machine B processes first
	};
int num_mac, num_job;
int jbegin_time = 0;
int count = 0;
void lpt(int begin_time, struct jobs j[num_job], int a);	
void lpt_mergesort(struct jobs j[num_job], int left, int right);
void john_sort1(struct jobs t_1[], int left, int right);
void john_sort2(struct jobs t_2[], int left, int right);
void mergesort(struct jobs j[num_job], int left, int right);
void johnson(int begin_time, struct jobs j[num_job],int b, int c);

int main(int argc, char** argv){
  	int begin_time = 0;
	if (strcmp(argv[1],"-i") == 0){
  		printf("Enter the number of machines in stage 1: "); 
  		scanf("%d",&num_mac); 
  
  		printf("Enter the number of jobs: ");
  		scanf("%d",&num_job);

  		/*make struct array */
  		struct jobs job[num_job]; 	
 
  	
 		/*get the processing times, use struct to store the times.*/
  		printf("Enter in each line the processing times for a job:\n");
	
  		for (int n = 0;n < num_job;n++){ 
    			scanf("%d %d %d", &job[n].processing_time[0],&job[n].processing_time[1],&job[n].processing_time[2]);
    			job[n].id = n+1;
  		}
		/*using the lpt_mergesort to sort the sequence of job by processing time of machine A.*/ 
  		lpt_mergesort(job, 0, num_job-1);
		int a = num_mac-1;			
  		lpt(begin_time,job,a);
		if (count == 2){
			count +=1;
			lpt_mergesort(job, 0, num_job-1);
			johnson(jbegin_time, job, 0,num_mac);
		}
	}
  	else if (strcmp(argv[1],"-r") == 0){
		FILE *fp;
		fp = fopen("instance.txt","a"); 
		for (int l = 0; l<100; l++){
			for(int i = 1;i<=10;i++){
				for (int m = 1; m <=10;m++ ){
					num_mac = m;
					num_job = m*10;
					struct jobs job[num_job]; 
					for (int n = 0;n < num_job;n++){ 
						job[n].processing_time[0] = rand() % (10*i) + 1;
						job[n].processing_time[1] = rand() % (10*i) + 1;
						job[n].processing_time[2] = rand() % (10*i) + 1;
						fprintf(fp,"%d %d %d\n",job[n].processing_time[0], job[n].processing_time[1], job[n].processing_time[2]);
					}
					/*using the lpt_mergesort to sort the sequence of job by processing time of machine A.*/ 
  					lpt_mergesort(job, 0, num_job-1);
					int a = num_mac-1;			
  					lpt(begin_time,job,a);
					if (count == 2){
						count +=1;
						lpt_mergesort(job, 0, num_job-1);
						johnson(jbegin_time, job, 0,num_mac);
					}
				
				}
			}	
			for(int i = 1;i<=10;i++){
				for (int m = 11; m <=20;m++ ){
					num_mac = m;
					num_job = m*10;
					struct jobs job[num_job]; 
					for (int n = 0;n < num_job;n++){ 
						job[n].processing_time[0] = rand() % (10*i) + 1;
						job[n].processing_time[1] = rand() % (10*i) + 1;
						job[n].processing_time[2] = rand() % (10*i) + 1;
						fprintf(fp,"%d %d %d\n",job[n].processing_time[0], job[n].processing_time[1], job[n].processing_time[2]);
					}
					/*using the lpt_mergesort to sort the sequence of job by processing time of machine A.*/ 
  					lpt_mergesort(job, 0, num_job-1);
					int a = num_mac-1;			
  					lpt(begin_time,job,a);
					if (count == 2){
						count +=1;
						lpt_mergesort(job, 0, num_job-1);
						johnson(jbegin_time, job, 0,num_mac);
					}

				}	
			}
		}
		fclose(fp);
		
	}
 	return 0; 
		
}




/*lpt function*/
void lpt(int begin_time, struct jobs j[num_job],int a){
	int t;
	int a_1 = j[num_job-1].processing_time[0];
	float L_1 = j[num_job-1].processing_time[0];
	printf("a_1 = %d\n", a_1);
	int average_load = 0;
	int all = 0;
	for(int i = 0; i <num_job-1;i++){
		all = all + j[i].processing_time[0];
	}
	average_load = (all/num_job);
	printf("average load  = %d\n", average_load);
	printf("L_1 = %d\n", L_1);
	/*compare the amount of machines and jobs, make sure the not come out overflow error */
	if (num_job > num_mac){
		/*use count to check the running time for function*/
	/*
  		printf("LPT order: ");
  		for (int n = 0; n < a; n++){
    			//printf("%d, ", j[n].id);
 		}
		printf("%d",j[a].id);//check the amount of job , let the end of last line is not comma
  		printf("\n");
		printf("\n");
		
  		printf("Job information: \n");
		if (a+1 > 1){
			int k = num_job-num_mac;
			for (int m= 0; m<num_mac-1;m++){
    				printf("Job %d is processed on A_%d starting %d;\n",j[m].id,m+1,begin_time);// print the job information result
				
  			}
			/*check if the lpt run more than once*/
			if (num_job-2*num_mac>0&&count == 2){
				for (int m= 0; m<num_mac;m++){
					k--;
					j[m].machineA  = m+1;
					j[m].start_time[0] = begin_time+j[m].processing_time[0]; 
				}
				if (num_mac==1){
					int t_1 = begin_time;
					for (int m= 0; m<a;m++){
    						printf("Job %d is processed on A_1 starting %d;\n",j[m].id,t_1);// print the job information result
						t_1 += j[m].processing_time[0];
					}
					printf("Job %d is processed on A_1 starting %d.\n",j[a].id,t_1);
					printf("\n");
					 t_1 = begin_time;
					printf("Machine information:\n");
					printf("A_1 processes ");
					for (int m= 0; m<a;m++){
						printf("job %d at %d,",j[m].id,t_1);
						t_1 += j[m].processing_time[0];
					}
					printf("job %d at %d.\n",j[a].id,t_1);
					t_1 += j[a].processing_time[0];
					int t = t_1 - begin_time;
					printf("The job processing time interval is [%d %d], and the makespan is %d\n",begin_time,t_1,t);

				}
				else{
					int t = 2;
					int t_1 = begin_time;
					for(int q = 0;q<(num_job/num_mac);q++){
						if (k==0){
							break;
						}
						
						for (int m=num_mac*(t-1); m<t*num_mac;m++){
							/*use mergesort to get the first finish machine */
							mergesort(j,0,num_mac-1); 
							j[m].machineA = j[m-num_mac].machineA;
							j[m].start_time[0] = j[m-num_mac].start_time[0];
							mergesort(j,0,num_mac-1); 
							printf("Job %d is processed on A_%d starting %d;\n",j[m].id,j[m].machineA,j[m].start_time[0]);
							j[m].start_time[0]  += j[m].processing_time[0];
							k--;
							if (k==0){
								break;
							}
					
						}
						mergesort(j,0,num_mac-1);
						t++;
						if (k==0){
							break;
						}
					
					}
					printf("\n");
					printf("Machine information:\n");
					int n = 0;
					for (n = 0; n<num_mac;n++){
						printf("A_%d processes ",n+1);
						for (int m = 0;m<num_job-num_mac;m++){
							if( j[m].machineA == n+1){
								printf("job %d at %d,",j[m].id,j[m].start_time[0]-j[m].processing_time[0]);
							}
						}
						printf("\n");
					}
					t_1 = j[num_mac-1].start_time[0]+j[0].processing_time[0];
					printf("The job processing time interval is [%d %d], and the makespan is %d",begin_time,t_1,t_1-begin_time);
					printf("\n");		

				}
			}
			else{
				printf("Job %d is processed on A_%d starting %d.\n",j[a].id,a+1,begin_time);//check the amount of machine , let the end of last line is period
				printf("\n");
				printf("Machine information:\n");
				for (int n = 0; n<a;n++){
    					printf("A_%d  processes job %d at %d;\n",n+1, j[n].id, begin_time);// print the machine information result
				}				
				printf("A_%d  processes job %d at %d.\n",a+1, j[a].id, begin_time);
				t  = j[0].processing_time[0];
				/*count makespan and print out*/
				printf("The job processing time interval is [%d, %d], and the makespan is %d\n", begin_time, j[0].processing_time[0]+begin_time,t);
			}
		}
		else{
			printf("Job %d is processed on A_%d staring %d.\n",j[a].id,num_mac,begin_time);
			printf("\n");
			printf("Machine information:\n");
			printf("A_%d  processes job %d at %d.\n",num_mac, j[a].id, begin_time);
			t  = j[0].processing_time[0];
			/*count makespan and print out*/
			printf("The job processing time interval is [%d, %d], and the makespan is %d\n", begin_time, j[0].processing_time[0]+begin_time,t);
		}
		if (count == 0){
			count +=1;
			johnson(begin_time, j, num_mac, num_job);
		}
	}
	else if (num_job <=  num_mac){
		printf("LPT order: ");
  		for (int n = 0; n < num_job-1; n++){
    			printf("%d, ", j[n].id);
  		}
		printf("%d",j[num_job-1].id);//check the amount of job , let the end of last line is not comma
  		printf("\n");
		printf("\n");
  		printf("Job information: \n");
		
		if (num_job > 1){
  			for (int n = 0; n<num_job-1;n++){
    				printf("Job %d is processed on A_%d starting %d;\n",j[n].id,n+1,begin_time);// print the job information result 
  			}
			printf("Job %d is processed on A_%d starting %d.\n",j[num_job-1].id,num_job,begin_time);//check the amount of machine , let the end of last line is period
			printf("\n");

			printf("Machine information:\n");
			for (int n = 0; n<num_job;n++){
    				printf("A_%d  processes job %d at %d;\n",n+1, j[n].id, begin_time);// print the machine information result
			}
			/*print put the remian machine information*/
			if (num_mac -num_job >=1){
				for(int n = num_job; n< num_mac-1;n++){
					printf("A_%d processes;\n", n);
				}
				printf("A_%d processes.\n", num_mac);
			}
			t  = j[0].processing_time[0]-begin_time;
			/*count makespan and print out*/
			printf("The job processing time interval is [%d, %d], and the makespan is %d\n", begin_time, j[0].processing_time[0],t);
		}
		else{
			printf("Job %d is processed on A_%d starting %d.\n",j[num_job-1].id,num_job,begin_time);
			printf("\n");	
			printf("Machine information:\n");
			printf("A_%d  processes job %d at %d;\n",num_job, j[num_job-1].id, begin_time);// print the machine information result
			/*print put the remian machine information*/
			if (num_mac -num_job >=1){
				for(int n = num_job; n< num_mac-1;n++){
					printf("A_%d processes;\n", n);
				}
				printf("A_%d processes.\n", num_mac);
			}
			t  = j[0].processing_time[0]-begin_time;
			/*count makespan and print out*/
			printf("The job processing time interval is [%d, %d], and the makespan is %d\n", begin_time, j[0].processing_time[0],t);
		}
		*/
		begin_time = t;
		johnson(begin_time,j, 0, 0);
	}
} 

/*johnson function*/
void johnson(int begin_time, struct jobs j[num_job], int b, int c){
	printf("\n");
	int m = 0;
	int k = 0;
	int t_3 = 0;
	int p = 0;
	int q = 0;
	if(num_job>num_mac){
		/*compare the processing time on B and C */
		for (int n = b;n<c;n++){
			if(j[n].processing_time[1]<= j[n].processing_time[2]){
				j[n].johnson_B = 1;
				m++;
			}
			else{
				j[n].johnson_B = 0;
				k++;
			}
		}
		/*use three struct array to copy the job struct*/
		struct jobs temp1[m];
		struct jobs temp2[k];

		for (int n = b;n<c;n++){
			if(j[n].johnson_B ==1){
				temp1[p] = j[n];//use temp1 to store the job processing time B smaller than C
				p++;
			}
			else{
				temp2[q] = j[n];//use temp1 to store the job processing time B bigger than C
				q++;
			}
		}
		/*use struct to combine the sort result*/
		struct jobs temp3[c-b];	
	
		/*sort as johnson rule*/
		john_sort1(temp1,0,p-1);
		john_sort2(temp2,0,q-1);
						
		/*combine the the sorted struct array*/
		int i =0;
		for (int n=0;n<p;n++){
			temp3[i] = temp1[n];//use temp3 to combine the struct
			i++;
		}
		for(int n = 0;n<q;n++){
			temp3[i] = temp2[n];
			i++;
		}
		int t_1 = begin_time;
		int t_2 = begin_time+temp3[0].processing_time[1];
		if (p+q>1){     //check the amount of machine
			//printf("Johnson's order: ");
  			for (int n = 0; n < p+q-1; n++){
    				printf("%d, ", temp3[n].id);
  			}
			//printf("%d\n",temp3[p+q-1].id);//check the amount of job , let the end of last line is not comma
		
			//printf("\n");
			
			//printf("Job information:\n");
			//printf("job %d is processed on B starting %d, on C starting %d;\n",temp3[0].id, t_1, t_2 );
			t_1 += temp3[0].processing_time[1];
			for (int n = 1; n<p+q-1;n++){
				if(temp3[n].processing_time[1]+t_1>temp3[n-1].processing_time[2]+t_2){  //compare the process time to determine the c starting time
					t_2 =t_1 + temp3[n].processing_time[1];
				}
				else{
					t_2 += temp3[n-1].processing_time[2];
				}
				//printf("job %d is processed on B starting %d, on C starting %d;\n",temp3[n].id, t_1, t_2 );
				t_1+= temp3[n].processing_time[1];
				
			}
			if(temp3[p+q-1].processing_time[1]+t_1>temp3[p+q-2].processing_time[2]+t_2){  //compare the process time to determine the c starting time
				t_2 =t_1 + temp3[p+q-1].processing_time[1];
			}
			else{
				t_2 += temp3[p+q-2].processing_time[2];
			}		
			//printf("job %d is processed on B starting %d, on C starting %d.\n",temp3[p+q-1].id, t_1, t_2);   // let the end of last line is period
			t_2 += temp3[p+q-1].processing_time[2];
			//printf("\n");

			//printf("Machine information:\n");
			int m_1 = begin_time;
			int m_2 = begin_time+temp3[0].processing_time[1];

			/*machine B information*/
			//printf("B processes ");
			for (int n = 0; n<p+q-1;n++){
				printf("job %d at %d, ",temp3[n].id, m_1 );
				m_1+= temp3[n].processing_time[1];	
			}
			//printf("job %d at %d;\n",temp3[p+q-1].id,m_1);  // let the end of last  is semicolon

			/*machine C information*/
			//printf("C processes ");
			m_1 = begin_time + temp3[0].processing_time[1];
			//printf("job %d at %d, ",temp3[0].id, m_2 );
			for (int n = 1; n<p+q-1;n++){
				if(temp3[n].processing_time[1]+m_1>temp3[n-1].processing_time[2]+m_2){  //compare the process time to determine the c starting time
					m_2 =m_1+ temp3[n].processing_time[1];
				}
				else{
					m_2 += temp3[n-1].processing_time[2];
				}
				printf("job %d at %d, ",temp3[n].id, m_2 );
				m_1 += temp3[n].processing_time[1];
			}
			if(temp3[p+q-1].processing_time[1]+m_1>temp3[p+q-2].processing_time[2]+m_2){  //compare the process time to determine the c starting time
				m_2 = m_1 + temp3[p+q-1].processing_time[1];			}
			else{
				m_2 +=temp3[p+q-2].processing_time[2];
			}		
			//printf("job %d at %d.\n",temp3[p+q-1].id,m_2);   // let the end of last is period

			/*print out makespan*/
			//printf("\n");
			t_3 = t_2-begin_time;
			int L_2 = t_3;
			printf("L_2 = %d\n",L_2);
			//printf("The job processing time interval is [%d, %d], and the makespan is %d.\n",begin_time, t_2, t_3); 
			//printf("\n");
		}
		else{	/*
			printf("Johnson's order: ");
			printf("%d\n",temp3[p+q-1].id);
			printf("\n");
			printf("Job information:\n");
			printf("job %d is processed on B starting %d, on C starting %d;\n",temp3[p+q-1].id, t_1, t_2 );
			printf("\n");
			printf("Machine information:\n");
			printf("B processes ");
			printf("job %d at %d;\n",temp3[p+q-1].id, begin_time); 
			printf("C processes ");
			printf("job %d at %d.\n",temp3[p+q-1].id, t_2);*/
			t_2 += temp3[p+q-1].processing_time[2];
			t_3 = t_2-begin_time;
			int L_2 = t_3;
			printf("L_2 = %d",L_2);

			/*printf("\n");
			printf("The job processing time interval is [%d, %d], and the makespan is %d.\n",begin_time, t_2, t_3); 
			printf("\n");*/
		} 
		jbegin_time = t_3;
		if (count == 1){
			count +=1;
			int a = num_job-num_mac-1;
			lpt_mergesort(temp3, 0, num_job-num_mac-1);
			lpt(t_3,temp3,a);
		}
		else if(count == 3){
			//printf("The LPT-Johnson schedule has an overall makespan %d.\n ",t_2);
			printf("LPT_Johnson schedule makespan = %d\n",t_2); 
		}			
	}	
	else if (num_job<=num_mac){
		/*compare the processing time on B and C */
		for (int n = 0;n<num_job;n++){
			if(j[n].processing_time[1]<= j[n].processing_time[2]){
				j[n].johnson_B = 1;
				m++;
			}
			else{
				j[n].johnson_B = 0;
				k++;
			}
		}
		/*use three struct array to copy the job struct*/
		struct jobs temp1[m];
		struct jobs temp2[k];

		for (int n = 0;n<num_job;n++){
			if(j[n].johnson_B ==1){
				temp1[p] = j[n];//use temp1 to store the job processing time B smaller than C
				p++;
			}
			else{
				temp2[q] = j[n];//use temp1 to store the job processing time B bigger than C
				q++;
			}
		}
		/*use struct to combine the sort result*/
		struct jobs temp3[num_job];	

		/*sort as johnson rule*/
		john_sort1(temp1,0,p-1);
		john_sort2(temp2,0,q-1);
						
		/*combine the the sorted struct array*/
		int i =0;
		for (int n=0;n<p;n++){
			temp3[i] = temp1[n];//use temp3 to combine the struct
			i++;
		}
		for(int n = 0;n<q;n++){
			temp3[i] = temp2[n];
			i++;
		}
		int t_1 = begin_time;
		int t_2 = begin_time+temp3[0].processing_time[1];
		if (num_job>1){     //check the amount of machine
			//printf("Johnson's order: ");
  			for (int n = 0; n < num_job-1; n++){
    				printf("%d, ", temp3[n].id);
  			}
			//printf("%d\n",temp3[num_job-1].id);//check the amount of job , let the end of last line is not comma
		
			//printf("\n");
			
			//printf("Job information:\n");
			//printf("job %d is processed on B starting %d, on C starting %d;\n",temp3[0].id, t_1, t_2 );
			t_1+= temp3[0].processing_time[1];
			for (int n = 1; n<num_job-1;n++){
				if(temp3[n].processing_time[1]+t_1>temp3[n-1].processing_time[2]+t_2){  //compare the process time to determine the c starting time
					t_2 =t_1 + temp3[n].processing_time[1];
				}
				else{
					t_2 += temp3[n-1].processing_time[2];
				}
				//printf("job %d is processed on B starting %d, on C starting %d;\n",temp3[n].id, t_1, t_2 );
				t_1+= temp3[n].processing_time[1];
				
			}
			if(temp3[p+q-1].processing_time[1]+t_1>temp3[p+q-2].processing_time[2]+t_2){  //compare the process time to determine the c starting time
				t_2 =t_1 + temp3[num_job-1].processing_time[1];
			}
			else{
				t_2 += temp3[num_job-2].processing_time[2];
			}				
			//printf("job %d is processed on B starting %d, on C starting %d.\n",temp3[num_job-1].id, t_1, t_2);   // let the end of last line is period
			t_2 += temp3[num_job-1].processing_time[2];
			//printf("\n");

			//printf("Machine information:\n");
			int m_1 = begin_time;
			int m_2 = begin_time+temp3[0].processing_time[1];

			/*machine B information*/
			//printf("B processes ");
			for (int n = 0; n<num_job-1;n++){
				printf("job %d at %d, ",temp3[n].id, m_1 );
				m_1+= temp3[n].processing_time[1];	
			}
			//printf("job %d at %d;\n",temp3[num_job-1].id,m_1);  // let the end of last  is semicolon

			/*machine C information*/
			m_1 = begin_time+temp3[0].processing_time[1];
			//printf("C processes ");
			//printf("job %d at %d, ",temp3[0].id, m_2 );
			for (int n = 1; n<num_job-1;n++){
				if(temp3[n].processing_time[1]+m_1>temp3[n-1].processing_time[2]+m_2){  //compare the process time to determine the c starting time
					m_2 =m_1+ temp3[n].processing_time[1];
				}
				else{
					m_2 += temp3[n-1].processing_time[2];
				}
				//printf("job %d at %d, ",temp3[n].id, m_2 );
				m_1 += temp3[n].processing_time[1];
			}
			if(temp3[p+q-1].processing_time[1]+m_1>temp3[p+q-2].processing_time[2]+m_2){  //compare the process time to determine the c starting time
				m_2 =m_1 + temp3[num_job-1].processing_time[1];
			}
			else{
				m_2 += temp3[num_job-2].processing_time[2];
			}		
			//printf("job %d at %d.\n",temp3[num_job-1].id,m_2);   // let the end of last is period
			
			/*print out makespan*/
			//printf("\n");
			t_3 = t_2-begin_time;
			//printf("The job processing time interval is [%d, %d], and the makespan is %d.\n",begin_time, t_2, t_3); 
			int L_2 = t_3;
			printf("L_2 = %d\n",L_2);

		}
		else{/*
			printf("Johnson's order: ");
			printf("%d\n",temp3[num_job-1].id);
			printf("\n");
			printf("Job information:\n");
			printf("job %d is processed on B starting %d, on C starting %d;\n",temp3[num_job-1].id, t_1, t_2 );
			printf("\n");
			printf("Machine information:\n");
			printf("B processes ");
			printf("job %d at %d;\n",temp3[num_job-1].id, begin_time); 
			printf("C processes ");
			printf("job %d at %d.\n",temp3[num_job-1].id, t_2);*/
			t_2 += temp3[0].processing_time[2];
			t_3 = t_2-begin_time;
			int L_2 = t_3;
			printf("L_2 = %d\n",L_2);
		}
			/*
			printf("\n");
			printf("The job processing time interval is [%d, %d], and the makespan is %d.\n",begin_time, t_2, t_3); 
		
		printf("\n");
		printf("The LPT-Johnson schedule has an overall makespan %d.\n ",t_2);
		*/
		printf("LPT_Johnson schedule makespan = %d\n",t_2); 
  	}
	return;		
}


/*lpt_mergesort function*/
void lpt_mergesort(struct jobs j[num_job], int left, int right){
	if (left >= right) { //termination condition: at most 1 element in the array
    		return;
  	}
  	int mid = (left + right) / 2;
  
  	lpt_mergesort(j, left, mid);
  	lpt_mergesort(j, mid + 1, right);
	struct jobs temp;
	
  	/* merge two sorted subarrays*/
  	/* merging inside job*/
  	for (int i = left; i <= mid; i++){
    		for (int m = mid + 1; m <= right; m++){
      			if (j[i].processing_time[0] < j[m].processing_time[0]) { //move
				temp = j[m];
				for (int k = m; k > i; k--){
					j[k] = j[k-1];
				}  	
				j[i] = temp;
				mid++; // keep the end of left subarray unchanged
      			}
  		} 
	}
	return;
}

/*john_mergesort function*/
void john_sort1(struct jobs t_1[], int left, int right){
  	if (left >= right) { //termination condition: at most 1 element in the array
		return;
  	}
  	int mid = (left + right) / 2;
  
  	john_sort1(t_1, left, mid);
  	john_sort1(t_1, mid + 1, right);
	struct jobs temp;
	
  	/* merge two sorted subarrays*/
  	/* merging inside job*/
  	for (int i = left; i <= mid; i++){
    		for (int m = mid + 1; m <= right; m++){
      			if (t_1[i].processing_time[1] > t_1[m].processing_time[1]) { //move
				temp = t_1[m];
				for (int k = m; k > i; k--){
					t_1[k] = t_1[k-1];
				}  	
				t_1[i] = temp;
				mid++; // keep the end of left subarray unchanged
      			}
  		} 
	}
	return;
}

void john_sort2(struct jobs t_2[], int left, int right){
	if (left >= right) { //termination condition: at most 1 element in the array
    		return;
  	}
  	int mid = (left + right) / 2;
  	john_sort2(t_2, left, mid);
  	john_sort2(t_2, mid + 1, right);
	struct jobs temp;
	
  	/* merge two sorted subarrays*/
  	/* merging inside job*/
  	for (int i = left; i <= mid; i++){
    		for (int m = mid + 1; m <= right; m++){
      			if (t_2[i].processing_time[2] < t_2[m].processing_time[2]) { //move
				temp = t_2[m];
				for (int k = m; k > i; k--){
					t_2[k] = t_2[k-1];
				}  	
				t_2[i] = temp;
				mid++; // keep the end of left subarray unchanged
      			}
  		} 
	}
	return;
}
		
		
void mergesort(struct jobs j[num_job], int left, int right) {
	if (left >= right)
		return;
	
	int mid = (left + right) / 2;
	mergesort(j, left, mid);
	mergesort(j, mid + 1, right);
	struct jobs temp;
	// insert below C statements to merge two sorted subarrays:
	// v3: merging inside a[], but needs a lot of data moving
	for (int i = left; i <= mid; i++){
    		for (int m = mid + 1; m <= right; m++){
      			if (j[i].start_time[0] > j[m].start_time[0]) { //move
				temp = j[m];
				for (int k = m; k > i; k--){
					j[k] = j[k-1];
				}  	
				j[i] = temp;
				mid++; // keep the end of left subarray unchanged
      			}
  		} 
	}
	return;
}
