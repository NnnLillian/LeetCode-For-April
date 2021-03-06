April 3rd的题目[`8. 字符串转换整数 (atoi)`](https://leetcode-cn.com/problems/string-to-integer-atoi/) 

题目规则（具体请看官方），此处概括为：

1. 去除字符串开头的空格
2. 字符串开头的是数字（有符号）则返回有符号数字，否则返回0
3. 忽略有效数字字符串之后的字符
4. 数字范围（`Math.pow(-2, 31)`,`Math.pow(2, 31) - 1`)

-

字符串转换成整数，可以想想parseInt()

**parseInt(string, radix)**  将一个字符串 string 转换为 radix 进制的整数， radix 为介于2-36之间的数。
关于这个API的详解可以参考[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)

如果仔细看了这篇MDN，你可以注意到这样一句话
> `parseInt`的字符不是指定基数中的数字，则忽略该字符和所有后续字符，并返回解析到该点的整数值。`parseInt`将数字截断为整数值。允许使用前导空格和尾随空格。

那么`parseInt()`已经替我们完成 **2.字符串开头的是数字（有符号）则返回有符号数字**、**3.忽略有效数字字符串之后的字符**、**1.忽略字符串开头空格** 这三个部分了。 只不过`parseInt()`如果转换不成功返回的不是`0`，而是`NaN`；并且他没有32位的数组大小限制。

因此我们可以

- `isNaN()`判断是否转换成功
- `Math.max(Math.min(number,INT_MAX),INT_MIN)`限制number大小


Javascript代码如下：

```
var myAtoi = function(str) {
   const number = parseInt(str, 10),
         INT_MAX = Math.pow(-2, 31),   
         INT_MIN = Math.pow(2, 31) - 1;   
   return isNaN(number)?0:Math.max(Math.min(number,INT_MAX),INT_MIN)
};
```

小细节请注意：
`parseInt(string, radix)`转换时，如果没有radix参数，会有很多问题，所以请**永远都要明确给出radix参数的值**
