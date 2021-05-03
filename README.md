Q.1(2).You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

 Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.

Input: l1 = [0], l2 = [0]
Output: [0]

Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int a=0;int c=0;int d=0;
        ListNode head=new ListNode();
        ListNode temp=head;
        while(l1!=null || l2!=null)
        {
            a=0;ListNode nextnode;
            if(l1!=null && l2!=null)
            {
             a=l1.val+l2.val;
                d=(a+c)%(10);                               //finding sum
                c=(a+c)/10;                                //finding the Carry
             nextnode=new ListNode(d);
                l1=l1.next;
                l2=l2.next;
            }
           else if(l1!=null && l2==null                   //if l1 is of higher length than l2
            {
                a=l1.val;
               d=(a+c)%(10);
                c=(a+c)/10;
             nextnode=new ListNode(d);
                l1=l1.next;
            }
            else                                        //if l2 is of higher length than l1
            {
                a=l2.val;
                d=(a+c)%(10);
                c=(a+c)/10;
                 nextnode=new ListNode(d);
                l2=l2.next;
            }
            temp.next=nextnode;
            temp=temp.next;
        }
        if(c!=0)                                          //if there is carry at the end
        {
            ListNode nextnode=new ListNode(c);
            temp.next=nextnode;
        }
        return head.next;
        
    }
}

Q.2(19)Given the head of a linked list, remove the nth node from the end of the list and return its head.

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

Q.3.(21).Merge two sorted linked lists and return it as a sorted list. The list should be made by splicing together the nodes of the first two lists.
Input: l1 = [1,2,4], l2 = [1,3,4]
Output: [1,1,2,3,4,4]

Input: l1 = [], l2 = []
Output: []

Input: l1 = [], l2 = [0]
Output: [0]

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
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {

    ListNode head= new ListNode();
    ListNode temp = head;
    while(l1 != null || l2 != null )
    {  
        ListNode nextNode = null;
        if(l2 == null || ( l1!= null && l1.val < l2.val) )
        {                             
            nextNode = l1;            
            l1 = l1.next;               
        }           
        else 
        {
            nextNode = l2;
            l2 = l2.next;             
        }   
                             
        temp.next = nextNode;                                       
        temp = nextNode;
    }
         
    return head.next;
}
}

Q.4(24)Given a linked list, swap every two adjacent nodes and return its head.
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


Q.5.(61).Given the head of a linked list, rotate the list to the right by k places.
Example 1:
Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
Example 2:
Input: head = [0,1,2], k = 4
Output: [2,0,1]
 
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
    public ListNode rotateRight(ListNode head, int k) {
        
        int count=0;int k1=0;
        ListNode temp=head;
        while(temp!=null)
        {
            count++;                                //Finding the lengthof listnode
            temp=temp.next;
        }
        if(count==k || head==null)                  //If list is empty or kth element from last is first element of the list
            return head;
        else if(count<k)
            k1=k%count;                             //kth element from end if the length of list is smaller than k
        else
            k1=k;
        ListNode ptr1=head;
        ListNode ptr2=head;
        ListNode previous=null;
        int c=0;
        while(c<k1)
        {
            ptr1=ptr1.next;                        //Advancing pointer 1 by k1 node
            c++;
        }
        while(ptr1.next!=null)
        {
            ptr1=ptr1.next;                    //When pointer 1 reaches to the last node pointer 2 point to the (k+1)th element from end
            ptr2=ptr2.next;
        }
        ptr1.next=head;                        
        head=ptr2.next;
        ptr2.next=null;
    
    return head;
    }
}
