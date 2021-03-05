
# Problem Description
Write a serialize function and deserialize function to convert a tree to a string and a string to a tree

# Solution
This is a very interesting problem. For a long time, I thought tree can't be serialize LOL. The reason is that given a pre-order or any order of traversal, we can't find what the tree looks like. But it turns out it's pretty easy to do if we have a good protocal between serialization and deserialization. And the important thing here is to add a "X" for each None node. We can use a pre oreder tarversal and add a "X" whenever met with a None.

The thing to note here is there are two ways to keep the index whiling deserializing. One is we can use a nonlocal variable. The other is we use iterator. Use iter() to convert a list to a iterator. It's pretty neat to use an iterator to creat less difficulty in reading.

'''python
# Serialize and deserialize a tree
class Node:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


def serialize(root):
    def helper(result_list, root):
        if root is None:
            result_list.append('X')
            return

        result_list.append(root.val)

        helper(result_list, root.left)
        helper(result_list, root.right)
        return
    result_list = []
    helper(result_list, root)
    return ",".join(result_list)


def deserialize(s):
    # Given a string, construct a list
    s_list = s.split(",")
    s_iter = iter(s_list)

    # return the current constructed node
    def helper():
        node_val = next(s_iter)
        if node_val == "X":
            return None

        cur_node = Node(node_val)

        cur_node.left = helper()
        cur_node.right = helper()

        return cur_node

    return helper()


print(serialize(deserialize("1,2,3,X,X,X,2,X,X")))
