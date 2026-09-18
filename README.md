# Binary-Search-Tree..........-
#include <iostream>
using namespace std;

template <typename T>
class BST
{
private:
    // Node structure
    struct Node
    {
        T data;
        Node* left;
        Node* right;

        Node(T value)
        {
            data = value;
            left = nullptr;
            right = nullptr;
        }
    };

    Node* root;

    // Insert helper function
    Node* insert(Node* node, T value)
    {
        if (node == nullptr)
        {
            return new Node(value);
        }

        if (value < node->data)
        {
            node->left = insert(node->left, value);
        }
        else if (value > node->data)
        {
            node->right = insert(node->right, value);
        }

        return node;
    }

    // Search helper function
    bool search(Node* node, T value)
    {
        if (node == nullptr)
        {
            return false;
        }

        if (node->data == value)
        {
            return true;
        }

        if (value < node->data)
        {
            return search(node->left, value);
        }

        return search(node->right, value);
    }

    // Find minimum node
    Node* findMin(Node* node)
    {
        while (node != nullptr && node->left != nullptr)
        {
            node = node->left;
        }

        return node;
    }

    // Delete helper function
    Node* deleteNode(Node* node, T value)
    {
        if (node == nullptr)
        {
            return nullptr;
        }

        if (value < node->data)
        {
            node->left = deleteNode(node->left, value);
        }
        else if (value > node->data)
        {
            node->right = deleteNode(node->right, value);
        }
        else
        {
            // Case 1: No child
            if (node->left == nullptr && node->right == nullptr)
            {
                delete node;
                return nullptr;
            }

            // Case 2: Only right child
            else if (node->left == nullptr)
            {
                Node* temp = node->right;
                delete node;
                return temp;
            }

            // Case 3: Only left child
            else if (node->right == nullptr)
            {
                Node* temp = node->left;
                delete node;
                return temp;
            }

            // Case 4: Two children
            else
            {
                Node* temp = findMin(node->right);

                node->data = temp->data;

                node->right = deleteNode(node->right, temp->data);
            }
        }

        return node;
    }

    // In-order traversal
    void inOrder(Node* node)
    {
        if (node == nullptr)
        {
            return;
        }

        inOrder(node->left);
        cout << node->data << " ";
        inOrder(node->right);
    }

    // Pre-order traversal
    void preOrder(Node* node)
    {
        if (node == nullptr)
        {
            return;
        }

        cout << node->data << " ";
        preOrder(node->left);
        preOrder(node->right);
    }

    // Post-order traversal
    void postOrder(Node* node)
    {
        if (node == nullptr)
        {
            return;
        }

        postOrder(node->left);
        postOrder(node->right);
        cout << node->data << " ";
    }

    // Destroy tree and free memory
    void destroy(Node* node)
    {
        if (node == nullptr)
        {
            return;
        }

        destroy(node->left);
        destroy(node->right);

        delete node;
    }

public:
    // Constructor
    BST()
    {
        root = nullptr;
    }

    // Insert
    void insert(T value)
    {
        root = insert(root, value);
    }

    // Search
    bool search(T value)
    {
        return search(root, value);
    }

    // Delete
    void remove(T value)
    {
        root = deleteNode(root, value);
    }

    // In-order traversal
    void inOrder()
    {
        inOrder(root);
        cout << endl;
    }

    // Pre-order traversal
    void preOrder()
    {
        preOrder(root);
        cout << endl;
    }

    // Post-order traversal
    void postOrder()
    {
        postOrder(root);
        cout << endl;
    }

    // Destructor
    ~BST()
    {
        destroy(root);
    }
};

int main()
{
    BST<int> tree;

    // Insert elements into BST
    tree.insert(50);
    tree.insert(30);
    tree.insert(70);
    tree.insert(20);
    tree.insert(40);
    tree.insert(60);
    tree.insert(80);

    cout << "Binary Search Tree" << endl;
    cout << "==================" << endl;

    // Traversals
   