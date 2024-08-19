# 整理字符串

给你一个由大小写英文字母组成的字符串 `s` 。

一个整理好的字符串中，两个相邻字符 `s[i]` 和 `s[i+1]`，其中 `0<= i <= s.length-2` ，要满足如下条件:

- 若 `s[i]` 是小写字符，则 `s[i+1]` 不可以是相同的大写字符。
- 若 `s[i]` 是大写字符，则 `s[i+1]` 不可以是相同的小写字符。
请你将字符串整理好，每次你都可以从字符串中选出满足上述条件的 **两个相邻** 字符并删除，直到字符串整理好为止。

请返回整理好的 **字符串** 。题目保证在给出的约束条件下，测试样例对应的答案是唯一的。

**注意**：空字符串也属于整理好的字符串，尽管其中没有任何字符。

## 示例 1：
>### 输入：
>s = "leEeetcode"
>### 输出：
>"leetcode"
>### 解释：
>从字符串中选出下标 3 和 4，它们分别属于 "L" 和 "e"，所以字符串整理后为 "leetcode"。

## 示例 2：
>### 输入：
>s = "abBAcC"
>### 输出：
>""
>### 解释：
>从字符串中选出下标 1 和 4，它们分别属于 "a" 和 "c"，所以字符串整理后为 ""。

## 代码：

1.
```c#
public class Solution {
    public string MakeGood(string s) {
        StringBuilder stack = new StringBuilder();
        int index = -1;
        foreach (char c in s) {
            if (index >= 0 && SameLetterDifferentCases(stack[index], c)) {
                stack.Length--;
                index--;
            } else {
                stack.Append(c);
                index++;
            }
        }
        return stack.ToString();
    }

    public bool SameLetterDifferentCases(char c1, char c2) {
        return Math.Abs(c1 - c2) == 32;
    }
}
```
2.
```c#
public class Solution {
    public string MakeGood(string s) {
        if(s.Length==1){
            return s;
        }
        for(int i=0;i<s.Length-1;i++){
            if(s[i]-32==s[i+1]||s[i]+32==s[i+1]){
                s=s.Remove(i,1);
                s=s.Remove(i,1);
                i=-1;
            }
        }  
        return s;
    }
}
```
3.
```c#
public class Solution
{
    public string MakeGood(string s)
    {
        Stack<char> stack = new Stack<char>();

        foreach (char c in s)
        {
            if (stack.Count > 0 && Math.Abs(stack.Peek() - c) == 32)
            {
                // 如果栈顶字符与当前字符满足删除条件（一个大写一个小写）
                stack.Pop();
            }
            else
            {
                // 否则，将当前字符压入栈
                stack.Push(c);
            }
        }

        // 构造整理好的字符串
        StringBuilder result = new StringBuilder();
        while (stack.Count > 0)
        {
            result.Insert(0, stack.Pop());
        }

        return result.ToString();
    }
}
```
