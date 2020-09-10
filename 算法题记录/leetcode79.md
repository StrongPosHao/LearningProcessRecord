## Leetcode 79 单词搜索（剑指offer12）

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

 

示例:

board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true
给定 word = "SEE", 返回 true
给定 word = "ABCB", 返回 false
 

提示：

board 和 word 中只包含大写和小写英文字母。
1 <= board.length <= 200
1 <= board[i].length <= 200
1 <= word.length <= 10^3
### 思路
* 深度优先搜索（DFS）+ 剪枝
### 算法原理
* DFS：通过递归，先朝一个方法搜到底，再回溯至上个结点，沿另一个方向搜索，以此类推。
* 剪枝：在搜索中，遇到**这条路不可能和目标字符串匹配成功**的情况，则应立即返回，称之为**可行性剪枝**。情况有：
  * 此矩阵元素和目标字符不同
  * 此元素已被访问
### 算法剖析
* 递归参数：当前元素在矩阵board中的行列索引i和j，当前目标字符在word中的索引k
* 终止条件：
   * 返回false:
   		1. 行或列索引越界
      	2. 当前矩阵元素与目标字符不同
      	3. 当前矩阵元素已访问过
	* 返回true：字符串word已全部匹配，即`k = len(word) - 1`
* 递推工作：
	1. 标记当前矩阵元素：将board[i][j]值暂存于变量temp，并修改为字符'/'，代表此元素已访问过，防止之后搜索时重复访问
	2. 搜索下一单元格：朝当前元素的上、下、左、右四个方向开启递归，使用or连接（代表只需一条可行路径），并记录结果至res
	3. 还原当前矩阵元素，将tmp暂存值还原至board[i][j]元素
* 回溯返回值：返回res，代表是否搜索到目标字符串。
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        char[] chars = word.toCharArray();
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (dfs(board, chars, i, j, 0)) {
                    return true;
                }
            }
        }
        return false;
    }

    public boolean dfs(char[][] board, char[] word, int i, int j, int k) {
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] != word[k]) {
            return false;
        }
        if (k == word.length - 1) {
            return true;
        }
        char temp = board[i][j];
        board[i][j] = '/';
        boolean res = dfs(board, word, i + 1, j, k + 1) || dfs(board, word, i - 1, j, k + 1) || 
            dfs(board, word, i, j - 1, k + 1) || dfs(board, word, i, j + 1, k + 1);
        board[i][j] = temp;
        return res;
    }
}
```
