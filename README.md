# CPP-program-2
Merge two unsorted linked lists to get a sorted list
#include <bits/stdc++.h>
using namespace std;
  
// Create structure for a node
struct node {
    int data;
    node* next;
};
  
// Function to print the linked list
void setData(node* head)
{
    node* tmp;
  
    // Store the head of the linked
    // list into a temporary node*
    // and iterate
    tmp = head;
  
    while (tmp != NULL) {
  
        cout << tmp->data
             << " -> ";
        tmp = tmp->next;
    }
}
  
// Function takes the head of the
// LinkedList and the data as
// argument and if no LinkedList
// exists, it creates one with the
// head pointing to first node.
// If it exists already, it appends
// given node at end of the last node
node* getData(node* head, int num)
{
  
    // Create a new node
    node* temp = new node;
    node* tail = head;
  
    // Insert data into the temporary
    // node and point it's next to NULL
    temp->data = num;
    temp->next = NULL;
  
    // Check if head is null, create a
    // linked list with temp as head
    // and tail of the list
    if (head == NULL) {
        head = temp;
        tail = temp;
    }
  
    // Else insert the temporary node
    // after the tail of the existing
    // node and make the temporary node
    // as the tail of the linked list
    else {
  
        while (tail != NULL) {
  
            if (tail->next == NULL) {
                tail->next = temp;
                tail = tail->next;
            }
            tail = tail->next;
        }
    }
  
    // Return the list
    return head;
}
  
// Function to concatenate the two lists
node* mergelists(node** head1,node** head2)
{
  
    node* tail = *head1;
  
    // Iterate through the head1 to find the
    // last node join the next of last node
    // of head1 to the 1st node of head2
    while (tail != NULL) {
  
        if (tail->next == NULL
            && head2 != NULL) 
        {
            tail->next = *head2;
            break;
        }
        tail = tail->next;
    }
  
    // return the concatenated lists as a
    // single list - head1
    return *head1;
}
  
// Sort the linked list using bubble sort
void sortlist(node** head1)
{
    node* curr = *head1;
    node* temp = *head1;
  
    // Compares two adjacent elements
    // and swaps if the first element
    // is greater than the other one.
    while (curr->next != NULL) {
  
        temp = curr->next;
        while (temp != NULL) {
  
            if (temp->data < curr->data) {
                int t = temp->data;
                temp->data = curr->data;
                curr->data = t;
            }
            temp = temp->next;
        }
        curr = curr->next;
    }
}
  
// Driver Code
int main()
{
    node* head1 = new node;
    node* head2 = new node;
  
    head1 = NULL;
    head2 = NULL;
  
    // Given Linked List 1
    head1 = getData(head1, 1);
    head1 = getData(head1, 2);
    head1 = getData(head1, 4);
  
    // Given Linked List 2
    head2 = getData(head2, 1);
    head2 = getData(head2, 3);
    head2 = getData(head2, 4);
  
    // Merge the two lists
    // in a single list
    head1 = mergelists(&head1,&head2);
  
    // Sort the unsorted merged list
    sortlist(&head1);
  
    // Print the final
    // sorted merged list
    setData(head1);
    return 0;
}

