Q.1(19)Given the head of a linked list, remove the nth node from the end of the list and return its head.

Follow up: Could you do this in one pass?
Example 1:
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode temp=head;int count=0;ListNode current=head;ListNode previous=head;
        if(head==null)
            return null;                         //base case
        
        while(count<n)
        {
            temp=temp.next;               //point to node n+1 from front
            count++;
           }
        if(temp==null)
            return head.next;                  //case in which nth node from end point to first node of list
        while(temp!=null)
        {
            temp=temp.next;                 //icementing both variable temp and current together ,at end of loop current will pont nth node form end
            previous=current;
            current=current.next;
            
        }
        previous.next=current.next;            //deleting nth node from end
        return head;
    }
}

Q.2(24)Given a linked list, swap every two adjacent nodes and return its head.
Example 1:
Input: head = [1,2,3,4]
Output: [2,1,4,3]

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head==null || head.next==null)                                         //base case
            return head;
       ListNode current=head;ListNode Next=null;ListNode previous=head;
        while(current!=null && current.next!=null)
        {
            Next=current.next;                                      
            current.next=Next.next;                                           //Swaping two node 
            Next.next=current;
            if(previous!=head)                                                //Logic to connect second node of previous step to first node of next step after swapping
            previous.next=Next;
            else
                head=Next;
            previous=current;
            current=current.next;
            
        }
        return head;
        
    }
}
