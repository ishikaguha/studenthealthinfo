# studenthealthinfo
Implementation of priority queue-allows to enter weight of a number of students, where the weight acts as priority and sorts the queue everytime a new weight is entered
//WAP to store student health info sorted by roll, edit weight.
#include<stdio.h>
#include<stdlib.h>
struct node
{
    int roll;
    float hgt,wgt;
    struct node *next;
};
struct node *topA=NULL,*topB=NULL;
void push(struct node **top,int roll,float hgt,float wgt)
{
    struct node *newNode;
    newNode=(struct node *)malloc(sizeof(struct node));
    newNode->roll=roll;
    newNode->hgt=hgt;
    newNode->wgt=wgt;
    if(*top==NULL)
    {
        newNode->next=NULL;
    }
    else
    {
        newNode->next=*top;
    }
    *top=newNode;
    printf("Node is inserted");
}
struct node *pop(struct node **top)
{
    if(*top==NULL)
    {
        printf("\nStack Underflow");
    }
    else
    {
        struct node *temp=*top;
        int temp_roll=(*top)->roll;
        float temp_hgt=(*top)->hgt;
        float temp_wgt=(*top)->wgt;
        *top=(*top)->next;
        return temp;
    }
}
void insert()
{
    int rll, wt, ht;
    printf("Enter the Roll No: ");
    scanf("%d",&rll);
    printf("Enter the height: ");
    scanf("%d",&ht);
    printf("Enter the weight: ");
    scanf("%d",&wt);
    if (topA==NULL)
    {
        push(&topA,rll,ht,wt);
    }
    else
    {
        struct node *temp=topA;
        while (temp->next!=NULL)
        {
            temp=temp->next;
        }
        if (temp->roll<rll)
        {
            push(&topA,rll,ht,wt);
        }
        else
        {
            while (temp->roll>rll)
            {
                push(&topB,temp->roll,temp->hgt,temp->wgt);
                pop(&topA);
                temp=temp->next;
            }
            push(&topA,rll,ht,wt);
            while (topB!=NULL)
            {
                push(&topA,topB->roll,topB->hgt,topB->wgt);
                pop(&topB);
            }
        }
    }
}
void editwt()
{
    int rll, wt;
    printf("Enter the Roll No: ");
    scanf("%d",&rll);
    printf("Enter the weight: ");
    scanf("%d",&wt);
    struct node *temp=topA;
    while (temp->roll!=rll)
    {
        struct node *temp=pop(&topA);
        push(&topB,temp->roll,temp->hgt,temp->wgt);
        temp=temp->next;
    }
    temp->wgt=wt;
    while (topB!=NULL)
    {
        struct node *temp=pop(&topB);
        push(&topA,temp->roll,temp->hgt,temp->wgt);
    }
}
void display(){
    struct node *temp=topA;
    printf("Roll\tHeight\tWeight");
    while (temp!=NULL)
    {
        printf("%d\t%f\t%f",temp->roll,temp->hgt,temp->wgt);
        temp=temp->next;
    }
}
void main()
{
    int sel=1;
    while (sel!=0)
    {
        printf("1. Insert\n2. Edit Weight\n3. Display\n0. Exit\n");
        scanf("%d",&sel);
        switch (sel)
        {
        case 1:
            insert();
            break;
        case 2:
            editwt();
            break;
        case 3:
            display();
            break;
        case 0:
            break;
        default:
            printf("Invalid Selection\n");
            break;
        }
    }
}
