# Ex17 AVL Tree – Rotation
## DATE: 19/03/2025
## AIM:
To write a C function to perform right rotation in an AVL Tree.

## Algorithm
1. Define a structure for AVL Tree node with fields: data, height, left, and right.
2. Write a function to get the height of a node.
3. Create a utility function to return the maximum of two integers.
4. Implement the right rotation logic:
   - Let y be the root of the unbalanced subtree.
   - Let x = y->left and T2 = x->right.
   - Perform the rotation: x->right = y, y->left = T2.
   - Update the heights of y and x.
   - Return x as the new root.
5. Test the function using a small tree that causes imbalance requiring a right rotation.


## Program:
```
/*
Program to perform right rotation in AVL Tree
Developed by: Joel John Jobinse
RegisterNumber: 212223240062
*/

#include <stdio.h>
#include <stdlib.h>

// AVL Tree Node
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
    int height;
};

// Get the height of a node
int height(struct Node* N) {
    if (N == NULL)
        return 0;
    return N->height;
}

// Get max of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Create a new node
struct Node* newNode(int key) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->data = key;
    node->left = node->right = NULL;
    node->height = 1;
    return node;
}

// Right Rotation
struct Node* rightRotate(struct Node* y) {
    struct Node* x = y->left;
    struct Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
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
    /*
    Manually creating the tree:
         30
        /
      20
     /
   10

    Needs right rotation at 30
    */

    struct Node* root = newNode(30);
    root->left = newNode(20);
    root->left->left = newNode(10);

    // Before rotation
    printf("In-order before rotation: ");
    inOrder(root);
    printf("\n");

    // Perform right rotation at root
    root = rightRotate(root);

    // After rotation
    printf("In-order after right rotation: ");
    inOrder(root);
    printf("\n");

    return 0;
}

```

## Output:

![image](https://github.com/user-attachments/assets/682ad72b-74e3-4579-a5fd-4ee66000bed2)


## Result:
Thus, the function to perform right rotation in an AVL Tree is implemented successfully.
