# Huffman-Coding
## Aim
To implement Huffman coding to compress the data using Python.

## Software Required
1. Anaconda - Python 3.7

## Algorithm:

Step 1: Read the input string from the user.

Step 2: Count how many times each character occurs (its frequency).

Step 3: Sort the characters by frequency, then repeatedly take the two lowest-frequency nodes and merge them into a new parent node whose frequency is their sum.

Step 4: Repeat Step 3 until only one node (the root of the Huffman tree) is left.

Step 5: Traverse the tree from the root, assigning 0 for every left branch and 1 for every right branch. The path to each character is its Huffman code. Print the characters with their codes.

 
## Program:

``` Python
# Get the input String
string = input("Vasanth")



# Create tree nodes
class NodeTree:
    def __init__(self, left=None, right=None):
        self.left = left
        self.right = right

    def children(self):
        return (self.left, self.right)


# Main function to implement huffman coding

def huffman_code_tree(node, binString=''):
    # A leaf node is a single character
    if type(node) is str:
        return {node: binString if binString != '' else '0'}
    (l, r) = node.children()
    d = dict()
    d.update(huffman_code_tree(l, binString + '0'))
    d.update(huffman_code_tree(r, binString + '1'))
    return d

# Calculate frequency of occurrence
freq = {}
for c in string:
    freq[c] = freq.get(c, 0) + 1

freq = sorted(freq.items(), key=lambda x: x[1], reverse=True)

nodes = freq
while len(nodes) > 1:
    (key1, c1) = nodes[-1]
    (key2, c2) = nodes[-2]
    nodes = nodes[:-2]
    node = NodeTree(key1, key2)
    nodes.append((node, c1 + c2))
    nodes = sorted(nodes, key=lambda x: x[1], reverse=True)

huffmanCode = huffman_code_tree(nodes[0][0])



# Print the characters and its huffmancode

print(' Char | Huffman code ')
print('----------------------')
for char, frequency in freq:
    print(' %-4r |%12s' % (char, huffmanCode[char]))

# Compression summary
original_bits = len(string) * 8
compressed_bits = sum(frequency * len(huffmanCode[char]) for char, frequency in freq)
print("\nOriginal size   :", original_bits, "bits")
print("Compressed size :", compressed_bits, "bits")



```
## Output:

### Print the characters and its huffmancode
<img width="347" height="186" alt="image" src="https://github.com/user-attachments/assets/d9ba7972-96d9-4d5e-a689-40ff3af230b4" />




## Result
Thus the huffman coding was implemented to compress the data using python programming.
