# MP5---Trees
# Binary Search Tree with remove_min() operation

class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None


class BinarySearchTree:
    def __init__(self):
        self.root = None

    def insert(self, key):
        if self.root is None:
            self.root = Node(key)
        else:
            self._insert(self.root, key)

    def _insert(self, node, key):
        if key < node.key:
            if node.left is None:
                node.left = Node(key)
            else:
                self._insert(node.left, key)
        else:
            if node.right is None:
                node.right = Node(key)
            else:
                self._insert(node.right, key)

    def traverse_inorder(self):
        result = []
        self._inorder(self.root, result)
        return result

    def _inorder(self, node, result):
        if node:
            self._inorder(node.left, result)
            result.append(node.key)
            self._inorder(node.right, result)

    def remove_min(self):
        """Removes the smallest value (leftmost node) in the tree."""
        if self.root is None:
            print("Tree is empty.")
            return
        self.root = self._remove_min(self.root)

    def _remove_min(self, node):
        # If there's no left child, this is the smallest node
        if node.left is None:
            return node.right  # Return the right child (may be None)
        node.left = self._remove_min(node.left)
        return node


# --- Example Usage ---
bst = BinarySearchTree()
for value in [8, 3, 10, 1, 6, 14, 4, 7, 13]:
    bst.insert(value)

print("In-order before removing min:", bst.traverse_inorder())
bst.remove_min()
print("In-order after removing min:", bst.traverse_inorder())
