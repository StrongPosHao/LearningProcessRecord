## Leetcode869. 重新排序得到2的幂
给定正整数 N ，我们按任何顺序（包括原始顺序）将数字重新排序，注意其前导数字不能为零。

如果我们可以通过上述方式得到 2 的幂，返回 true；否则，返回 false。

 

示例 1：

输入：1
输出：true
示例 2：

输入：10
输出：false
示例 3：

输入：16
输出：true
示例 4：

输入：24
输出：false
示例 5：

输入：46
输出：true
 

提示：

1 <= N <= 10^9

### 方法一：
**思路**
* 对N全排列，对每个排列检查是不是2的幂
#### 产生所有的排列组合
* 把任意数字放在首位(start = 0)，接着从剩余数字任意找一个放在第二个位置(start = 1)，依此类推。
#### 检查当前排列是不是2的幂
* 首先检查有没有前置0，再不断除2直到当前数为奇数，如果结果是1，那就是2的幂
