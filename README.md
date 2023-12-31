# trees-and-graph
#include<iostream>

using namespace std;
class Node {
public:
	int data;
	Node* left;
	Node* right;
	Node* next;

	Node(int value) {
		data = value;
		left = nullptr;
		right = nullptr;
		next = nullptr;
	}
};
class queue {
public:
	Node* front;
	Node* rear;

	queue() {
		front = NULL;
		rear = NULL;
	}
	void enqueue(Node* newNode) {
		if (rear == nullptr) {
			front = rear = newNode;
		}
		else {
			rear->next = newNode;
			rear = newNode;
		}
	}
	void dequeue() {
		if (front == nullptr) {
			cout << "Queue is empty";
			return;
		}
		else {
			Node* t = front;
			front = front->next;
			if (front == nullptr) {
				rear = nullptr;
			}
			delete t;
		}
	}

	};
class binaryTree {
public:
	Node* root;
	binaryTree() {
		root = NULL;

	}
	void inOrder(Node* root)
	{
		if (root != NULL)
		{
			inOrder(root->left);
			cout << root->data << "  ";
			inOrder(root->right);
		}
	}
	
void preOrder(Node* root)
{
	if (root != NULL)
	{
		cout << root->data << "  ";
		preOrder(root->left);
		preOrder(root->right);
	}
}


void postOrder(Node* root)
{
	if (root != NULL)
	{
		postOrder(root->left);
		postOrder(root->right);
		cout << root->data<<"  ";
	}
}

Node* levelOrderPoint(Node* root) {
	if (root == NULL) {
		return NULL;
	}

	queue q;

	q.enqueue(root);
	Node* current = NULL;

	while (q.front != NULL) {
		current = q.front;
		q.dequeue();

		if (current->left) {
			q.enqueue(current->left);
		}
		if (current->right) {
			q.enqueue(current->right);
		}
	}

	return current; 
}
};


int main() {
	binaryTree bt;
	bt.root = new Node(10);
	bt.root->left = new Node(20);
	bt.root->right = new Node(30);
	bt.root->right->left = new Node(40);
	bt.root->right->right = new Node(50);
	cout << "Pre Order :";
	bt.preOrder(bt.root);
	cout << endl;
	cout << "Post Order :";
	bt.postOrder(bt.root);
	cout << endl;
	cout << "In Order :";
	bt.inOrder(bt.root);
	Node* lastNode = bt.levelOrderPoint(bt.root);
	if (lastNode) {
		cout << "Last node in level order traversal: " << lastNode->data << endl;
	}
	else {
		cout << "Tree is empty!" << endl;
	}
	delete bt.root->right->left;
	bt.root->right->left = nullptr;
	delete bt.root->right->right;
	bt.root->right->right = nullptr;
	delete bt.root->right;
	bt.root->right = nullptr;
	delete bt.root->left;
	bt.root->left = nullptr;
	delete bt.root;
	bt.root = nullptr;
}
