# Ex19 B+ Tree
## DATE: 19/03/2025
## AIM:
To write a C function to traverse the elements in a B+ Tree.

## Algorithm
1. Start from the root node.
2. Recursively traverse all internal nodes until a leaf node is reached.
3. At the leaf level, traverse all keys and linked leaf nodes (if present).
4. Collect and display the keys in order.
5. End traversal once all leaf nodes are visited 

## Program:
```
/*
Program to traverse the elements in a B+ Tree.
Developed by: Joel John Jobinse
RegisterNumber: 212223240062
*/

#include <stdio.h>
#include <stdlib.h>

#define MAX 3

struct BPlusNode {
    int data[MAX];
    struct BPlusNode *child[MAX + 1];
    int isLeaf;
    int count;
};

void traverse(struct BPlusNode* root) {
    if (root != NULL) {
        int i;
        for (i = 0; i < root->count; i++) {
            if (!root->isLeaf)
                traverse(root->child[i]);
            printf("%d ", root->data[i]);
        }
        if (!root->isLeaf)
            traverse(root->child[i]);
    }
}

// Sample stub main (actual insertion not implemented in this stub)
int main() {
    struct BPlusNode *root = NULL;
    // Note: Full B+ Tree creation is not shown here.
    printf("Traversal of B+ Tree:\n");
    traverse(root);
    return 0;
}

```

## Output:
![image](https://github.com/user-attachments/assets/c26aeaf6-38e5-487d-adfd-1aa21ce83d3b)



## Result:
Thus, the function to traverse the elements in a B+ Tree is implemented successfully.
