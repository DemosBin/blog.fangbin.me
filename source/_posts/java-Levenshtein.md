---
title: 编辑距离(Levenshtein 距离)计算的简单实现
date: 2018-10-26 12:23:09
tags:
  - 编辑距离
  - java
categories:
  - 算法
---
上周参与会议提出需要计算两个字符串编辑距离的需求，刚好从简单的开始学习算法。
## 从思考到行动
### 思考：什么是编辑距离？
所谓编辑距离就是把一个字符串Str1最少经过最少多少步操作变成字符串Str2,操作包含且仅包含
- 添加一个字符
- 删除一个字符
- 修改一个字符

这么三种
emmm……最少？是不是应该叫最小编辑距离？

### 怎么计算编辑距离
计算编辑距离的核心就是Function——edit（i,j），它表示字符串s1的长度为i的子串到字符串s2的长度为j的子串的编辑距离。
可以有如下动态规划公式：
> if i == 0 且 j == 0，edit(i, j) = 0
if i == 0 且 j > 0，edit(i, j) = j
if i > 0 且j == 0，edit(i, j) = i
if i ≥ 1  且 j ≥ 1 ，edit(i, j) == min{ edit(i-1, j) + 1, edit(i, j-1) + 1, edit(i-1, j-1) + f(i, j) }，
当str1的第i 个字符不等于str2的第j个字符时，f(i, j) = 1；否则，f(i, j) = 0。

## 行动：实现
```
package com.best.oasis.asrserver.util;


public class LevenshteinTest {
    private int[][] array;
    private String str1;
    private String str2;

    private LevenshteinTest(String str1, String str2){
        this.str1 = str1;
        this.str2 = str2;
    }

    /**
     * 计算字符串str1的长度为i的子串到字符串str2的长度为j的子串的编辑距离
     *  if i == 0 且 j == 0，edit(i, j) = 0
     *   if i == 0 且 j > 0，edit(i, j) = j
     *   if i > 0 且j == 0，edit(i, j) = i
     *   if i ≥ 1  且 j ≥ 1 ，edit(i, j) == min{ edit(i-1, j) + 1, edit(i, j-1) + 1, edit(i-1, j-1) + f(i, j) }，
     *   当str1的第i 个字符不等于str2的第j个字符时，f(i, j) = 1；否则，f(i, j) = 0。
     */
    private void edit() {
        int max1 = str1.length();
        int max2 = str2.length();
        //建立数组，比字符长度大一个空间
        array = new int[max2+1][max1+1];
        for(int i=0;i<=max1;i++){
            array[0][i] = i;
        }
        for(int j=0;j<=max2;j++){
            array[j][0] = j;
        }
        for(int i=1;i<=max1;i++){
            for(int j=1;j<=max2;j++){
                array[j][i] = levenshtein(i,j,str1.charAt(i-1),str2.charAt(j-1));
                System.out.println("比较str2第"+j+"位与str1第"+i+"位   "+array[j][i]);
            }
        }
        System.out.println("最小编辑距离是：" + array[max2][max1]);
    }

    private int levenshtein(int i, int j, char si, char sj) {
        int result = 0;
        if(i>=1&&j>=1){
            int a = array[j-1][i] + 1;
            int b = array[j][i-1] + 1;
            int c = array[j-1][i-1] + ((si!=sj)?1:0);
            result = min(a,b,c);
        }
        return result;
    }

    private int min(int a, int b, int c) {
        int temp = a<b?a:b;
        return temp<c?temp:c;
    }

    public static void main(String args[]){
        String str1 = "我爱中国共产党";
        String str2 = "中国共产党爱我";
        LevenshteinTest lt = new LevenshteinTest(str1,str2);
        lt.edit();
    }
}
```
至此，完成！

参考文档：[文本相似度——编辑距离算法&java简单实现](https://blog.csdn.net/ssjjy/article/details/19127117)
