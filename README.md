# double-data-structure

#include <iostream>
using namespace std;

struct Node {
	int data;
	Node* next;
	Node* prev;

};
Node* last = NULL;
Node* first = NULL;



void insertFirst(int value) {
	Node* newnode = new Node;
	newnode->next = NULL;
	newnode->prev = NULL;
	newnode->data = value;
	if (first == 0) {
		first = last = newnode;
		newnode->next = NULL;
		newnode->prev = NULL;
	}

	else {
		newnode->next = first;
		newnode->prev = NULL;
		first->prev = newnode;
		first = newnode;
	}
}

void insertLast(int value) {
		Node* newnode = new Node;
	newnode->next = NULL;
	newnode->prev = NULL;
	newnode->data = value;
	if (first == 0) {
		first = last = newnode;
		newnode->next = NULL;
		newnode->prev = NULL;
	}
	else {
		last->next = newnode;
		newnode->prev = last;
		last = newnode;
	}
}

void insertAt(int pos, int value) {
	Node* newnode = new Node;
	newnode->next = NULL;
	newnode->prev = NULL;
	newnode->data = value;
	if (first == 0) {
		first = last = newnode;
		newnode->next = NULL;
		newnode->prev = NULL;
	}
	else {
		Node* temp = first;
		for (int i = 1; i < pos - 1 && temp != NULL; i++) {
			temp = temp->next;
		}
		if (temp != NULL) {
			newnode->next = temp->next;
			newnode->prev = temp;
			if (temp->next != NULL) {
				temp->next->prev = newnode;
			}
			temp->next = newnode;
			if (newnode->next == NULL) {
				last = newnode;
			}
		}
		else {
			cout << "Position out of bounds" << endl;
		}
	}
}

void deleteFirst() {
	if (first == NULL) {
		cout << "List is empty" << endl;
		return;
	}
	Node* temp = first;
	first = first->next;
	if (first != NULL) {
		first->prev = NULL;
	}
	else {
		last = NULL;
	}
	delete temp;
}

void deleteLast() {
	if (first == NULL) {
		cout << "List is empty" << endl;
		return;
	}
	Node* temp = last;
	last = last->prev;
	if (last != NULL) {
		last->next = NULL;
	}
	else {
		first = NULL;
	}
	delete temp;
}

void deleteAt(int pos) {
	if (first == NULL) {
		cout << "List is empty" << endl;
		return;
	}
	if (pos == 1) {
		deleteFirst();
		return;
	}
	Node* temp = first;
	for (int i = 1; i < pos && temp != NULL; i++) {
		temp = temp->next;
	}
	if (temp != NULL) {
		if (temp->prev != NULL) {
			temp->prev->next = temp->next;
		}
		if (temp->next != NULL) {
			temp->next->prev = temp->prev;
		}
		if (temp == last) {
			last = temp->prev;
		}
		delete temp;
	}
	else {
		cout << "Position out of bounds" << endl;
	}
}
void display() {
	Node* temp = first;
	while (temp != NULL) {
		cout << temp->data << " ";
		temp = temp->next;
	}
	cout << endl;
}

int main() {
	insertFirst(10);
	insertFirst(20);
	insertFirst(30);
	insertFirst(40);
	display();

	insertLast(50);
	insertLast(60);
	display();

	insertAt(3, 25);
	display();
	return 0;
}
