import java.util.*;

public class JobScheduler {
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
	System.out.println("enter the number of jobs");
        int n = sc.nextInt(); // number of jobs
        
        // Create an array of Jobs
        Job[] jobs = new Job[n];
        for (int i = 0; i < n; i++) 
{
         System.out.println("Enter the startTime, endTime, profit");

            int startTime = sc.nextInt();
            int endTime = sc.nextInt();
            int profit = sc.nextInt();
            jobs[i] = new Job(startTime, endTime, profit);
        }
        
        // Sort the jobs in non-decreasing order of their end times
        Arrays.sort(jobs, new Comparator<Job>() {
            public int compare(Job j1, Job j2) {
                return j1.endTime - j2.endTime;
            }
        });
        
        int maxProfit = 0;
        int numJobsPicked = 0;
        int lastEndTime = 0;
        
        // Pick jobs starting from the earliest end time
        for (Job job : jobs) {
            if (job.startTime >= lastEndTime) {
                maxProfit += job.profit;
                numJobsPicked++;
                lastEndTime = job.endTime;
            }
        }
        
        // Print the number of jobs left and the total earnings of those jobs
        int numJobsLeft = n - numJobsPicked;
        int totalEarnings = 0;
        for (int i = numJobsPicked; i < n; i++) {
            totalEarnings += jobs[i].profit;
        }
        System.out.println("Task:"+numJobsLeft);
        System.out.println("Earnings: "+totalEarnings);
    }
}

class Job {
    int startTime;
    int endTime;
    int profit;
    
    public Job(int startTime, int endTime, int profit) {
        this.startTime = startTime;
        this.endTime = endTime;
        this.profit = profit;
    }
}
