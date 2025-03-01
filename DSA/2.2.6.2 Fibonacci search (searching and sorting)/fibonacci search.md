@@ -3,20 +3,16 @@
## **What is fibonacci search?**<br>
Fibonacci Search is a comparison-based technique that uses Fibonacci numbers to search an element in a sorted array.
Given a sorted array arr[] of size n and an element x to be searched in it. Return index of x if it is present in array else return -1. 
 <br><br>

## **Explaination:**
<br>
     1. Works for sorted arrays<br>
     2. A Divide and Conquer Algorithm.<br>
     3.Fibonacci Search divides given array into unequal parts<br>
     4.Binary Search uses a division operator to divide range. Fibonacci Search doesn’t use /, but uses + and -. The division operator may be costly on some CPUs.<br>
     5.Fibonacci Search examines relatively closer elements in subsequent steps. <br>
     So when the input array is big that cannot fit in CPU cache or even in RAM, Fibonacci Search can be useful.<br>
     6. Has Log n time complexity.

<br><br>

## **Background:** 
<br>
Fibonacci Numbers are recursively defined as F(n) = F(n-1) + F(n-2), F(0) = 0, F(1) = 1. First few Fibinacci Numbers are 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, …
<br><br>


## **Observations:** 
<br>
Below observation is used for range elimination, and hence for the O(log(n)) complexity.  

F(n - 2) &approx; (1/3)*F(n) and 
F(n - 1) &approx; (2/3)*F(n).



Steps:

1.  Find F(k){kth fibonacci number}, which is greater than or equal to n.

             Description{ k= 0   1   2   3   4   5   6     7......
                       F(k)= 0   1   1   2   3   5   8   13.......}

2.  If F(K)=0 
         stop and print massage as element not found.

3.  Offset=-1

4.  i=min(offset+F(k-2),n-1)
            To check if fibMm2 is a valid location

5.  If x==A[i]     return i and stop the search
     If x>A[i]       k=k-1, offset=i and repeat step 4 then 5.
     If x<A[i]      k=k-2  repeat step 4 then 5.
     Description{If x matches, return index
                       Else If x is less than the element, move the three Fibonacci variables two Fibonacci down, indicating elimination of                        approximately rear two-third of the remaining array.
                       Else x is greater than the element, move the three Fibonacci variables one Fibonacci down. Reset offset to index. Together                        these indicate the elimination of approximately front one-third of the remaining array.
                       Since there might be a single element remaining for comparison, check if fibMm1 is 1. If Yes, compare x with that remaining                        element. If match, return index.}




<br><br>
## **Algorithm:**
<br>
             /* This function used to find mininum of given number */<br>
 int min(int x, int y)<br>
 {<br>
     return (x<=y)? x : y;<br>
 }<br>
<br>

 int fibonaccianSearch(int arr[], int x, int n)<br>
 {<br>
     /* Here fibonacci numbers are initializing*/<br>
     int fbK2 = 0;   // (k-2)'th Fibonacci number<br>
     int fbK1 = 1;   // (k-1)'th Fibonacci number<br>
     int fbK = fbK2 + fbK1;  // k'th Fibonacci<br>
<br>
     int offset = -1;<br>
<br>
     /* fbK is going to store the smallest Fibonacci<br>
        number greater than or equal to n */<br>
     while (fbK < n)<br>
     {<br>
         fbK2 = fbK1;<br>
         fbK1 = fbK;<br>
         fbK  = fbK2 + fbK1;<br>
     }<br>
     while (fbK > 1)<br>
     {<br>
     int i = min(offset+fbK2, n-1);<br>
<br>
     /* If x is greater than the value at index fbK2,<br>
        cut the subarray array from offset to i */<br>
     if (arr[i] < x)<br>
     {<br>
         fbK  = fbK1;<br>
         fbK1 = fbK2;<br>
         fbK2 = fbK - fbK1;<br>
         offset = i;<br>
     }<br>
<br>
     /* If x is greater than the value at index fbKk2,
        cut the subarray after i+1  */<br>
     else if (arr[i] > x)<br>
     {<br>
         fbK  = fbK2;<br>
         fbK1 = fbK1 - fbK2;<br>
         fbK2 = fbK - fbK1;<br>
     }<br>
<br>
     /* element found. return index */<br>
     else return i;<br>
     }<br>
<br>
     /* comparing the last element with x */<br>
     if(fbK1 && arr[offset+1] == x)<br>
     return offset+1;<br>
     /*element not found. return -1 */<br>
     return -1;<br>
 }<br>


<br><br>
## **Implementation:**
<br>

#include<stdio.h><br>
 #include<conio.h><br>


 int min(int x, int y);<br>
int fibonaccianSearch(int arr[], int x, int n);<br>
 
 /* main function */<br>
 int main(void)<br>
 {<br>
     int l,i;<br>
     printf("\nEnter the total number of elements:");<br>
     scanf("%d",&l);<br>
     int arr[l];<br>
     printf("Enter elements in array\n");<br>
     for(i=0;i<l;i++)<br>
     {<br>
     scanf("%d",&arr[i]);<br>
     }<br>
     int n = sizeof(arr)/sizeof(arr[0]);<br>
     int x;<br>
     printf("\nEnter element to be searched:");<br>
     scanf("%d",&x);<br>
     printf("Found at index: %d",fibonaccianSearch(arr, x, n));<br>
     getch();<br>
     return 0;<br>
 } <br>





<br>

## *Output:*<br>
Enter the total number of elements:9<br>
Enter elements in array<br>
 4 6 7 9 11 34 67 87 901 1002<br>
Enter element to be searched:901<br>
<br>
Found at index:8
