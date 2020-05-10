import java.util.*;

/*It is a Sliding Window ques done by using Doubly Ended Queue(Deque). Basically a window of suppose four number moves
 * from left ot right of an array like in an array of 1,2,3,4,5,6 it will start with 1,2,3 and print the highest number 
 * among these and then move one step forward thereby now considering 2,3,4 and print max value between them. */
public class SlidingWindow {

	public static void main(String[] args) {
    Solution an= new Solution();
    int a[]= {4};
    
    int ans[]= an.maxSlidingWindow(a, 3);
    for(int x:ans)
    	System.out.print(x+" ");
	}

	
	static class Solution{
		public int[] maxSlidingWindow(int[] a, int k)
		{int n= a.length;
		 if((n==0) ||(n==1))
			 return a;
		Deque<Integer> dq= new LinkedList<>();
		int ans[]= new int[n-k+1];
		
		int i=0;
		for(;i<k;i++)
		{while(!dq.isEmpty()  && a[dq.peekLast()] <=a[i]) {
			   dq.removeLast();
			}
			dq.addLast(i);
		}
		
		for(;i<n;i++)
		{
			ans[i-k]=a[dq.peekFirst()];
			
			while(!dq.isEmpty() && dq.peekFirst()<=i-k)
				{dq.removeFirst();}
			
			while(!dq.isEmpty() && a[dq.peekLast()]<=a[i])
				{dq.removeLast();}
			
			dq.addLast(i);
		}
		
		ans[i-k]=a[dq.peekFirst()];
		return ans;
		}
	}
}
