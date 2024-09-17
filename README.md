#include<iostream>
using namespace std;
struct Node {
	int data;
	Node* left;
	Node* right;
};
Node* createNode(int data) {
	Node* temp = new Node;
	temp->data = data;
	temp->left = temp->right = NULL;
	return temp;
}
Node* insertNode(Node* node, int data) {
	if (node == NULL) {
		return createNode(data);
	}
	if (node->data < data) {
		node->right = insertNode(node->right, data);
	}
	else if (node->data > data) {
		node->left = insertNode(node->left, data);
	}
	return node;
}
void inorder(Node* node) {
	if (node != NULL) {
		inorder(node->left);
		cout << node->data << " ";
		inorder(node->right);
	}
}
void findMax(Node* node) {
	if (node->right != NULL) {
		return findMax(node->right);
	}
	cout << "\nmax: " << node->data;
}void find2Max(Node* node) {
	Node* temp = node->left;
	while (node->right != NULL) {
		temp = node;
		node = node->right;
	}
	if (node->left == NULL || node->left == temp) {
		cout << "Max 2th: " << temp->data;
	}
	else
	{
		node = node->left;
		while (node->right != NULL) {
			node = node->right;
		}
		cout << "Max 2th: " << node->data;
	}
}
int main() {
	int A[34] = { 10,5,15,2,7,12,18,1,3,6,8,11,13,16,19,,0,4,9,14,17,20,25,22,27,21,23,26,28,29,30,31,32,33 };
	Node* node;
	for (int i = 0; i < 34; i++) {
		node = insertNode(node, A[i]);
	}
	inorder(node);
	find2Max(node);
}
