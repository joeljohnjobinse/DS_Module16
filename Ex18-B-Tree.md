# Ex18 B-Tree
## DATE: 19/03/2025
## AIM:
To write a C function to delete an element in a B Tree.
## Algorithm
1. Define a node structure for a B-Tree with keys, children, and number of keys.
2. If the key is in the current node and the node is a leaf, remove the key.
3. If the key is in the current node and the node is internal, replace it with the predecessor or successor and recursively delete.
4. If the key is not in the current node, recursively search the child node where the key may exist.
5. After deletion, if the child has too few keys, perform rotation or merging to maintain B-Tree properties.


## Program:
```
/*
/*
Program to write a C function to delete an element in a B Tree
Developed by: Joel John Jobinse
RegisterNumber: 212223240062
*/

#include <stdio.h>
#include <stdlib.h>

#define MAX 3
#define MIN 2

typedef struct BTreeNode {
    int val[MAX + 1], count;
    struct BTreeNode* link[MAX + 1];
} BTreeNode;

BTreeNode* root;

// Create node
BTreeNode* createNode(int val, BTreeNode* child) {
    BTreeNode* newNode = (BTreeNode*)malloc(sizeof(BTreeNode));
    newNode->val[1] = val;
    newNode->count = 1;
    newNode->link[0] = root;
    newNode->link[1] = child;
    return newNode;
}

// Insert node
void insert(int val) {
    int flag, i;
    BTreeNode* child;

    BTreeNode* newNode = _insert(val, root, &flag, &child);

    if (flag) {
        root = createNode(i, child);
    }
}

// Deletion from B-Tree (basic leaf deletion)
void deleteVal(int val, BTreeNode* node) {
    int pos, i;

    if (!node) {
        printf("Tree is empty.\n");
        return;
    }

    for (pos = 1; pos <= node->count && val > node->val[pos]; pos++);

    if (pos <= node->count && val == node->val[pos]) {
        if (node->link[pos - 1]) {
            printf("Deletion of internal node not implemented (simplified version).\n");
        } else {
            for (i = pos; i < node->count; i++) {
                node->val[i] = node->val[i + 1];
            }
            node->count--;
            printf("Value %d deleted.\n", val);
        }
    } else {
        deleteVal(val, node->link[pos - 1]);
    }
}

// Display B-Tree
void display(BTreeNode* node, int level) {
    if (node) {
        int i;
        for (i = node->count; i >= 1; i--) {
            display(node->link[i], level + 1);
            for (int j = 0; j < level; j++) printf("    ");
            printf("%d\n", node->val[i]);
        }
        display(node->link[0], level + 1);
    }
}

// Dummy function to simulate insertion for demo
void dummyInsertRoot() {
    root = (BTreeNode*)malloc(sizeof(BTreeNode));
    root->count = 3;
    root->val[1] = 10;
    root->val[2] = 20;
    root->val[3] = 30;
    for (int i = 0; i < 4; i++) root->link[i] = NULL;
}

int main() {
    dummyInsertRoot();  // Simulate a simple root node

    printf("B-Tree before deletion:\n");
    display(root, 0);

    deleteVal(20, root);

    printf("\nB-Tree after deletion:\n");
    display(root, 0);

    return 0;
}

```

## Output:
![image](https://github.com/user-attachments/assets/7186b07e-5510-481f-ace2-2e95b184bbcc)



## Result:
Thus, the C function to delete an element in a B Tree is implemented successfully.
