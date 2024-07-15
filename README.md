# Create-Binary-Tree-From-Descriptions

You are given a 2D integer array descriptions where descriptions[i] = [parenti, childi, isLefti] indicates that parenti is the parent of childi in a binary tree of unique values. Furthermore,

If isLefti == 1, then childi is the left child of parenti.
If isLefti == 0, then childi is the right child of parenti.
Construct the binary tree described by descriptions and return its root.

The test cases will be generated such that the binary tree is valid.

Example 1:

Input: descriptions = [[20,15,1],[20,17,0],[50,20,1],[50,80,0],[80,19,1]]
Output: [50,20,80,15,17,19]
Explanation: The root node is the node with value 50 since it has no parent.
The resulting binary tree is shown in the diagram.
Example 2:


Input: descriptions = [[1,2,1],[2,3,0],[3,4,1]]
Output: [1,2,null,null,3,4]
Explanation: The root node is the node with value 1 since it has no parent.
The resulting binary tree is shown in the diagram.
 

Constraints:

1 <= descriptions.length <= 104
descriptions[i].length == 3
1 <= parenti, childi <= 105
0 <= isLefti <= 1
The binary tree described by descriptions is valid.

# SOLUTION 

# Approach
We can use two hashmaps, one which maps node.val to node to build the tree and keep track of nodes we have created already (map) and another one which indicates whether node is a child of another node (child or alternatively you can use a HashSet like I did in Python) . Then we iterate through descriptions.

If descriptions[i][0] is not in map then it's the first time it is appearing, so we create it and put it in map since it is the parent node of descriptions[i][1].
Then we create the node for descriptions[i][1] if it is not already created.
We assign this node to its parent's (descriptions[i][0]) left/right pointer depending on if descriptions[i][2] is true/false respectively.
Add descriptions[i][1] to the map and set its value in child to true, to indicate that it's a child node of some other node.
Lastly, for our return value we return the root, which will be whichever node in the map is not a child node of another node.

Complexity
Time complexity: O(n)
Space complexity: O(n)

# JAVA CODE

class Solution {

    public TreeNode createBinaryTree(int[][] descriptions) {

        TreeNode[] map = new TreeNode[100001];
        
        boolean[] child = new boolean[100001];
        
        for (int[] d : descriptions){
        
            if (map[d[0]] == null) map[d[0]] = new TreeNode(d[0]);
            
            TreeNode node = (map[d[1]] == null ? new TreeNode(d[1]) : map[d[1]]);
            
            if (d[2] == 1) map[d[0]].left = node;
            
            else map[d[0]].right = node;
            
            map[node.val] = node;
            
            child[d[1]] = true;
        }
        for (int[] d : descriptions)
        
            if (!child[d[0]])
            
                return map[d[0]];
                
        return null;
        
    }
}
