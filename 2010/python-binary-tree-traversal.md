---
title: 'Python binary tree traversal'
date: 2010-05-27T07:30:00.000-07:00
oldUrl: "http://ciantic.blogspot.com/2010/05/python-binary-tree-traversal.html"
tags : [python]
---

![](http://upload.wikimedia.org/wikipedia/commons/thumb/6/67/Sorted_binary_tree.svg/250px-Sorted_binary_tree.svg.png)

```python
# Python  
from itertools import chain  
from collections import deque  
  
class n(object):  
    left = None  
    right = None  
    value = None  
      
    def __init__(self, value=None, left=None, right=None):  
        self.value = value  
        self.left = left  
        self.right = right  
          
    def __call__(self, left=None, right=None):  
        self.left = left  
        self.right = right  
        return self.value  
  
def preorder(node):  
    lefts = []  
    rights = []  
      
    if node.left != None:  
        lefts = preorder(node.left)  
          
    if node.right != None:  
        rights = preorder(node.right)  
          
    return chain([node], lefts, rights)  
          
def inorder(node):  
    lefts = []  
    rights = []  
      
    if node.left != None:  
        lefts = inorder(node.left)  
      
    if node.right != None:  
        rights = inorder(node.right)  
          
    return chain(lefts, [node], rights)  
  
  
def postorder(node):  
    lefts = []  
    rights = []  
      
    if node.left != None:  
        lefts = postorder(node.left)  
      
    if node.right != None:  
        rights = postorder(node.right)  
          
    return chain(lefts, rights, [node])  
      
      
def levelorder(node):  
    queue = deque([node])  
      
    while len(queue) > 0:  
        node = queue.pop() # Remove from right  
        yield node  
        if node.left:  
            queue.appendleft(node.left)  
        if node.right:  
            queue.appendleft(node.right)  
  
# Create nodes  
_ = None  
A = n('A')  
B = n('B')  
C = n('C')  
D = n('D')  
E = n('E')  
F = n('F')  
G = n('G')  
H = n('H')  
I = n('I')  
  
# Link the nodes  
F(B,G)  
B(A,D)  
D(C,E)  
  
G(_,I)  
I(H,_)  
  
print "Pre order:"  
print list(node.value for node in preorder(F))  
      
print "In order:"  
print list(node.value for node in inorder(F))  
  
print "Post order:"  
print list(node.value for node in postorder(F))  
      
print "Level order (queue):"  
print list(node.value for node in levelorder(F))  

```