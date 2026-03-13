def __init__(self, key):
self.key = key
self.left = None
self.right = None

class BinarySearchTree:
def __init__(self):
self.root = None

def insert(self, root, key):
if root is None:
return Node(key)
if key < root.key:
root.left = self.insert(root.left, key)
elif key > root.key:
root.right = self.insert(root.right, key)
return root

def search(self, root, key):
if root is None or root.key == key:
return root
if key < root.key:
return self.search(root.left, key)
return self.search(root.right, key)

def _min_value_node(self, node):
current = node
while current.left is not None:
current = current.left
return current

def delete(self, root, key):
if root is None:
return root

if key < root.key:
root.left = self.delete(root.left, key)
elif key > root.key:
root.right = self.delete(root.right, key)
else:
# Case 1 & 2: No child or one child
if root.left is None:
return root.right
elif root.right is None:
return root.left

# Case 3: Two children
# Get inorder successor (smallest in right subtree)
temp = self._min_value_node(root.right)
root.key = temp.key
root.right = self.delete(root.right, temp.key)

return root

def inorder(self, root):
if root:
self.inorder(root.left)
print(root.key, end=" ")
self.inorder(root.right)

# --- Real-Time Menu Interface ---
def main():
bst = BinarySearchTree()
print("--- Binary Search Tree Operations ---")

while True:
print("\n1. Insert  2. Search  3. Delete  4. Display (Inorder)  5. Exit")
choice = input("Select operation (1-5): ")

if choice == '1':
val = int(input("Enter value to insert: "))
bst.root = bst.insert(bst.root, val)
print(f"Inserted {val}")

elif choice == '2':
val = int(input("Enter value to search: "))
if bst.search(bst.root, val):
print(f"Result: {val} is FOUND in the tree.")
else:
print(f"Result: {val} NOT FOUND.")

elif choice == '3':
val = int(input("Enter value to delete: "))
if bst.search(bst.root, val):
bst.root = bst.delete(bst.root, val)
print(f"Deleted {val}")
else:
print(f"Error: {val} not found in tree.")

elif choice == '4':
print("Tree Elements (Inorder):", end=" ")
bst.inorder(bst.root)
print()

elif choice == '5':
print("Exiting...")
break
else:
print("Invalid choice!")

if __name__ == "__main__":
main()


Output:
--- Binary Search Tree Operations ---

1. Insert  2. Search  3. Delete  4. Display (Inorder)  5. Exit
Select operation (1-5): 1
Enter value to insert: 50
Inserted 50

Select operation (1-5): 1
Enter value to insert: 30
Inserted 30

Select operation (1-5): 1
Enter value to insert: 70
Inserted 70

Select operation (1-5): 4
Tree Elements (Inorder): 30 50 70

Select operation (1-5): 2
Enter value to search: 30
Result: 30 is FOUND in the tree.

Select operation (1-5): 3
Enter value to delete: 50
Deleted 50
Select operation (1-5): 4
Tree Elements (Inorder): 30 70
