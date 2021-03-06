
# Simple LinkedList

### Implement insert()

[15 Days LinkedList](https://www.hackerrank.com/challenges/30-linked-list)

### Implement removeDuplicates()
[24 Days More LinkedList](https://www.hackerrank.com/challenges/30-linked-list-deletion)

### Template for the question

```cpp
#include <iostream>
#include <cstddef>
using namespace std;

class Node {
public:
	int data;
	Node *next;
	Node(int d) {
		data = d;
		next = NULL;
	}
};

class Solution {
public:

	Node* insert(Node *head, int data) {
		//Complete this method
	}
	Node* removeDuplicates(Node *head) {
      		//Complete this method
	}
    
	void display(Node *head) {
		Node *start = head;
		while (start) {
			cout << start->data << " ";
			start = start->next;
		}
	}
};

int main() {
	Node* head = NULL;
	Solution mylist;
	int T, data;
	cin >> T;
	while (T-- > 0) {
		cin >> data;
		head = mylist.insert(head, data);
	}
	mylist.display(head);
	head=mylist.removeDuplicates(head);
	mylist.display(head);
}

```
### Implement insert()

input
```
4
2
3
4
1
```
output
```
2 3 4 1
```

Solution
```cpp

# Solution -1
	Node* insert(Node *head, int data) {
		//Complete this method
		Node *tmp;
		if(head == NULL){
			head = (Node *) malloc(sizeof(Node));
			head->data = data;
			head->next = NULL;
		} else{
			tmp = head;
			while(tmp->next != NULL){
				tmp = tmp->next;
			}
			tmp->next = (Node *) malloc(sizeof(Node));
			tmp = tmp->next;
			tmp->data = data;
			tmp->next = NULL;
		}

		return head;
	}
	
# Solution 2
	Node* insert(Node *head, int data) {
		if (head == NULL) {
			head = new Node(data);
		} else {
			Node *curr = head;
			while (curr->next != NULL)
				curr = curr->next;

			curr->next = new Node(data);
		}

		return head;
	}

# Solution -3
	Node* insert(Node *head, int data) {

		Node* newNode = new Node(data);

		if (head == NULL) {
			head = new Node(data);
		} else {
			Node *curr = head;
			while (curr->next != NULL){
				curr = curr->next;
			}
			newNode->next = curr->next;
			curr->next = newNode;
		}

		return head;
	}

```

### Implement removeDuplicates()
```cpp
// My solution
    Node* removeDuplicates(Node *head) {

		Node *tmp = head;
		int i = tmp->data;
		Node *current = NULL;
		current = insert(current,i);

    	while(tmp->next!=NULL){
    		tmp = tmp->next;
    		int j = tmp->data;
            if(i!=j) current = insert(current,j);
            i = j;
    	}

    	return current;
    }

// Others
 Node* removeDuplicates(Node *head)
          {
            Node *current = head;
            //Write your code here
            while (current->next != NULL) // iterate until there are no more elements 
            {
                
                // If next is same as current, remove next
                if (current->data == (current->next)->data)
                {
                    Node *temp = current->next;
                    current->next = current->next->next;
                    temp->next = NULL;
                }
                else
                    current = current->next;
                               
            }
            
              
            return head;
          }
	  
// Other2
          Node* removeDuplicates(Node *head)
          {
              Node* start = head;
              while (start) {
                  if (start->next!=NULL) {
                      if (start->data == start->next->data) {
                          start->next = start->next->next;
                      } else {
                          start = start->next;
                      }
                  } else {
                      start = start->next;
                  }
              }
              return head;
          }

```

---

# Binary Tree Search

### Implement getHeight()

[22 Days BST-Question](https://www.hackerrank.com/challenges/30-binary-search-trees)


### Implement levelOrder()

[23 Days BST-Question](https://www.hackerrank.com/challenges/30-binary-trees)

### Template for the question

```cpp
#include <iostream>
#include <cstddef>
#include <queue>

using namespace std;

class Node {
public:
	int data;
	Node *left;
	Node *right;
	Node(int d) {
		data = d;
		left = NULL;
		right = NULL;
	}
};

class Solution {
public:
	Node* insert(Node* root, int data) {
		if (root == NULL) {
			return new Node(data);
		} else {
			Node* cur;
			if (data <= root->data) {
				cur = insert(root->left, data);
				root->left = cur;
			} else {
				cur = insert(root->right, data);
				root->right = cur;
			}

			return root;
		}
	}
	int getHeight(Node* root) {
		//Write your code here
		if(root == NULL) return 0;

		int leftHeight = getHeight(root->left);
		int rightHeight = getHeight(root->right);

		return 1+ max(leftHeight,rightHeight);
	}

	void levelOrder(Node * root){
		// Complete code here
	}
	
	void display(Node *head) {
        	Node *start=head;
        	while(start) {
                  cout<<start->data<<" ";
                  start=start->next;
              }
	}

};


int main() {
	Solution myTree;
	Node* root = NULL;
	int T;
	int data;

	cin >> T;

	while (T-->0) {
		cin >> data;
		root = myTree.insert(root, data);
	}
	int height = myTree.getHeight(root);
	cout << endl << "H=" << height << endl;

	myTree.levelOrder(root);

	return 0;
}

```


```cpp
// My Solution
	void levelOrder(Node * root){
		if(root == NULL) return;

		queue<Node *> q;
		q.push(root);

		while(!q.empty()){
			Node* tree = q.front();
			q.pop();

			cout << tree->data << " ";
			if(tree->left) q.push(tree->left);
			if(tree->right) q.push(tree->right);
		}

	}
// Others

     void levelOrder(Node* root){
  	
       queue <Node*> q;
       q.push(root);
        // Don't use recursion on bfs
          
        while (!q.empty())
        {
            Node* current = q.front();
            q.pop();
            cout << current->data << " ";
            
            if (current->left != NULL)
                q.push(current->left);
            
            if (current->right != NULL)
                q.push(current->right);
        }
	
    }
```


---
### Reference

[LinkedList Basic PDF](http://cslibrary.stanford.edu/103/LinkedListBasics.pdf)

[LinkedList Basic Coding](https://www.codeproject.com/Articles/24684/How-to-create-Linked-list-using-C-C)



---

Below is the another template for other operation (insert/delete/reverse/print)
```cpp
#include <stdio.h>
#include <stdlib.h>


typedef struct linked_list {
	int data;
	struct linked_list *next;
}linked_list;




linked_list* Insert(linked_list *lst,int number){
	struct linked_list *temp;
	printf("=========Insert: %d ============\n",number);


	if(lst == NULL) {
		lst = (linked_list *) malloc(sizeof(linked_list));
		lst->data = number;
		lst->next = NULL;
	} else {
		temp = lst;
		while(temp->next != NULL) {
		temp = temp->next;
		}
		temp->next = (linked_list *) malloc(sizeof(linked_list));
		if(temp->next == NULL){
			printf("Error! memory is not available\n");
			exit(0);
		}
		temp = temp->next;
		temp->data = number;
		temp->next = NULL;
	}


	return lst;


}


void Print(linked_list *lst){
	linked_list *temp_list;
	temp_list = lst;    


	do{
		printf("%d ", temp_list->data);
		temp_list = temp_list->next;
	}while(temp_list != NULL) ;


	printf("\n");
}




linked_list* Reverse(linked_list *lst){
	linked_list *reverse = NULL;
	linked_list *temp;


	while(lst != NULL){
		temp = lst->next;
		lst->next = reverse;
		reverse = lst;
		lst =temp;
	}
	return reverse;
}


void Delete(linked_list *lst,int num){
	linked_list *temp;
	linked_list *del;
	temp = (linked_list *) malloc(sizeof(linked_list));
	del = (linked_list *) malloc(sizeof(linked_list));
	del = lst;
	printf("=========Delete: ============\n");
	if(lst->data == num){
		temp = lst->next;
		free(lst);
		lst = temp;
	}else{
		do{
			printf("delete>>1 %d \n", lst->data);
			if(lst->data == num){
				printf("found %d \n",lst->data);
			}
			//printf("delete>>2 %d \n", lst->data);
			temp = lst;
			lst = lst->next;
		}while(lst != NULL) ;
	}


	printf("\n");
}


void main(){
	printf("Linked List Program\n");
	linked_list *start_node = NULL;


	start_node = Insert(start_node,10);
	Print(start_node);


	start_node = Insert(start_node,20);
	Print(start_node);


	start_node = Insert(start_node,30);
	Print(start_node);


	start_node = Insert(start_node,40);
	Print(start_node);


	start_node = Reverse(start_node);
	Print(start_node);

}

```

