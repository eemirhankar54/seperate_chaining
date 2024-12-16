# seperate_chaining



#include <stdio.h>
#include <malloc.h>

typedef struct node{
	int data;
	struct node *next;
}node;

node *arr[10];

node *newNode()
{
	node *newnode = (node*)malloc(sizeof(node));
	newnode -> data = 0;
	newnode -> next = NULL;
	return newnode;
}

void init()
{
	for(int i = 0;i < 10;i++)
	{
		arr[i] = newNode();
	}
}


int hash(int search)
{
	return search % 10;
}

void insert(int add)
{
	int index = hash(add);
	if(arr[index] -> data == 0)
	{
		arr[index] -> data = add;
	}
	else
	{
		node *newnode = newNode();
		newnode -> data = add;
		
		node *temp = arr[index];
	
		while(temp -> next != NULL)
			temp = temp -> next;
		
		temp -> next = newnode;
	}
}

node *searching(int search)
{
	int index = hash(search);
	if(arr[index] -> data == search)
	{
		return arr[index];
	}
	else
	{
		node *temp = arr[index];
		while(temp != NULL)
		{
			if(temp -> data == search)
					return temp;
			temp = temp -> next;
		}
	}
}
void print()
{
	for(int i = 0;i < 10;i++)
	{
		printf("\n %d.index ==> %d",i,arr[i] -> data);
		node *temp = arr[i] -> next;
		while(temp != NULL)
		{
			printf(" => %d",temp -> data);
			temp = temp -> next;
		}
		
	}
	printf("\n------------------------\n");
}

int main()
{
	init();	
	insert(19);
	insert(25);
	insert(13);
	insert(225);
	insert(325);
	insert(555);
	insert(223);
	print();
	
	
	node *search = searching(325);
	if(search == NULL)
		printf("not found");
	else
		printf("found %d",search -> data);

	
return 0;
}
