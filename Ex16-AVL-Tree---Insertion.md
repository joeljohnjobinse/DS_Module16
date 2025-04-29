# Ex16 AVL Tree - Insertion
## DATE: 19/03/2025
## AIM:
To write a C function to insert the elements in an AVL Tree.

## Algorithm
1. Create a structure for AVL tree node with data, height, left and right pointers.
2. Write a utility function to get the height of the node.
3. Write a utility function to get the balance factor of the node.
4. Implement the four rotation functions (LL, RR, LR, RL) to maintain AVL balance.
5. Write the insertion function that updates height, checks balance factor, and applies appropriate rotations.

## Program:
```
/*
Program to insert the elements in an AVL Tree
Developed by: Joel John Jobinse
RegisterNumber: 212223240062
*/

#include <stdio.h>
#include <stdlib.h>

// AVL Tree Node
struct Node {
    int data;
    struct Node *left, *right;
    int height;
};

// Function to get the height of a node
int height(struct Node *N) {
    if (N == NULL)
        return 0;
    return N->height;
}

// Utility function to get maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Create a new AVL node
struct Node* newNode(int key) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->data = key;
    node->left = node->right = NULL;
    node->height = 1;
    return node;
}

// Right rotate
struct Node* rightRotate(struct Node* y) {
    struct Node* x = y->left;
    struct Node* T2 = x->right;

    x->right = y;
    y->left = T2;

    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    return x;
}

// Left rotate
struct Node* leftRotate(struct Node* x) {
    struct Node* y = x->right;
    struct Node* T2 = y->left;

    y->left = x;
    x->right = T2;

    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    return y;
}

// Get balance factor
int getBalance(struct Node* node) {
    if (node == NULL)
        return 0;
    return height(node->left) - height(node->right);
}

// AVL insertion function
struct Node* insert(struct Node* node, int key) {
    if (node == NULL)
        return newNode(key);

    if (key < node->data)
        node->left = insert(node->left, key);
    else if (key > node->data)
        node->right = insert(node->right, key);
    else
        return node;  // Duplicates not allowed

    node->height = 1 + max(height(node->left), height(node->right));

    int balance = getBalance(node);

    // Left Left Case
    if (balance > 1 && key < node->left->data)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->data)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->data) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->data) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    return node;
}

// In-order traversal
void inOrder(struct Node* root) {
    if (root != NULL) {
        inOrder(root->left);
        printf("%d ", root->data);
        inOrder(root->right);
    }
}

int main() {
    struct Node* root = NULL;

    // Insert sample nodes
    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 10);
    root = insert(root, 25);
    root = insert(root, 50);

    printf("In-order Traversal of AVL Tree: ");
    inOrder(root);
    printf("\n");

    return 0;
}

```

## Output:

![image](https://github.com/user-attachments/assets/4d88d262-ff5c-42f4-bd4a-59b4b7656650)


## Result:
Thus, the function to insert the elements in an AVL Tree is implemented successfully in C programming language.
