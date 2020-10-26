# 2020.10.26———有效的括号
## 题目
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

  > 1.左括号必须用相同类型的右括号闭合。
  
  > 2.左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。

示例 1:
```
输入: "()"
输出: true
```
示例 2:
```
输入: "()[]{}"
输出: true
```
示例 3:
```
输入: "(]"
输出: false
```
示例 4:
```
输入: "([)]"
输出: false
```
示例 5:
```
输入: "{[]}"
输出: true
```
## 解题
### 语言
java
### 思路
运用栈和哈希表来解决问题。

需要注意的点：

1.首先遍历字符串，遇到左括号就找右括号，后遇到的左括号就需要先找到对应的右括号与之配对，所以先放在栈。

2.遇到右括号时，我们需要一个对应的右括号对应。我们取栈顶的左括号，判断是否配对或者栈中没有左括号，那么字符串无效。

3.遍历结束时，如果栈中没有左括号，说明我们将字符串中所有左括号闭合，返回true。

4.字符串长度为奇数，一定是false。

### 代码
```java
class Solution {
    public boolean isValid(String s) {
        int n = s.length();
        if(n%2==1){//如果字符串数是奇数直接返回否值
            return false;
        }
        Map<Character,Character> pairs = new HashMap<Character,Character>(){{//创建哈希表保存各个右括号和左括号的对应值
            put(')','(');
            put(']','[');
            put('}','{');
        }};
        Deque<Character> stack = new LinkedList<Character>();
        for(int i=0;i<n;i++){
            char ch = s.charAt(i);//取字符
            if(pairs.containsKey(ch)){//如果哈希表中包含这个右括号字符
                if(stack.isEmpty()||stack.peek()!=pairs.get(ch)){//如果栈不空且栈顶取值和哈希表中对应值不符合
                    return false;
                }
                stack.pop();//弹出栈顶值
            }else{
                stack.push(ch);//将字符放入栈顶
            }
        }
        return stack.isEmpty();//如果全部符合，那就一定会为空值，因为凑够一对括号就会全部弹出
    }   
}
```
