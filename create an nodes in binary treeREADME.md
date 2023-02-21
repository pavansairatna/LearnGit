class Node {
    int data;
    Node left, right;

    public Node(int data) {
        this.data = data;
        left = right = null;
    }
}

class BinaryTree {
    Node root;

    public BinaryTree() {
        root = null;
    }

    // Method to insert a new node in the binary tree
    public void insert(int data) {
        root = insertNode(root, data);
    }

    private Node insertNode(Node root, int data) {
        if (root == null) {
            root = new Node(data);
            return root;
        }

        if (data < root.data) {
            root.left = insertNode(root.left, data);
        } else if (data > root.data) {
            root.right = insertNode(root.right, data);
        }

        return root;
    }

    // Method to eliminate duplicates from the binary tree
    public void eliminateDuplicates() {
        root = eliminateDuplicatesNode(root);
    }

    private Node eliminateDuplicatesNode(Node root) {
        if (root == null) {
            return null;
        }

        root.left = eliminateDuplicatesNode(root.left);
        root.right = eliminateDuplicatesNode(root.right);

        if (root.left != null && root.left.data == root.data) {
            root.left = null;
        }
        if (root.right != null && root.right.data == root.data) {
            root.right = null;
        }

        return root;
    }

    // Method to print the binary tree using inorder traversal
    public void printInorder() {
        printInorderNode(root);
    }

    private void printInorderNode(Node root) {
        if (root != null) {
            printInorderNode(root.left);
            System.out.print(root.data + " ");
            printInorderNode(root.right);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        tree.insert(10);
        tree.insert(5);
        tree.insert(20);
        tree.insert(5);
        tree.insert(8);

        System.out.print("Original binary tree: ");
        tree.printInorder();
        System.out.println();

        tree.eliminateDuplicates();

        System.out.print("Binary tree after eliminating duplicates: ");
        tree.printInorder();
    }
}

