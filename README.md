# letcode刷题

## z字形变换

Python:
```Python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows < 2: return s
        res = ["" for _ in range(numRows)]
        i, flag = 0, -1
        for c in s:
            res[i] += c
            # 到转折点取反
            if i == 0 or i == numRows - 1:
                flag = -flag
            i += flag  # 遍历行索引
        return "".join(res)
```

Rust:
```Rust
impl Solution {
    pub fn convert(s: String, num_rows: i32) -> String {
        if (num_rows < 2) {
            return s;
        }
        let mut res = vec![String::new(); num_rows as usize];
        let mut i = 0;
        let mut flag = -1;

        for c in s.chars() {
            res[i as usize].push(c);
            if i == 0 || i == num_rows - 1 {
                flag = -flag;
            }
            i += flag;
        }
    
        res.concat()
    }
}
```

## 整数取反

Python:
```Python
class Solution:
    def reverse(self, x: int) -> int:
        INT_MIN, INT_MAX = -2**31, 2**31 - 1
        
        rev = 0
        while x!= 0:
            # INT_MIN 也是一个负数， 不能写成 rev < INT_MIN // 10
            if rev < INT_MIN // 10 + 1 or rev > INT_MAX // 10:
                return 0
            
            digit = x % 10

            # Python3 的取模运算在 x 为负数时也会返回 [0, 9) 以内的结果，因此这里需要进行特殊判断
            if x < 0 and digit > 0:
                digit -= 10
            
            # 同理，Python3 的整数除法在 x 为负数时会向下（更小的负数）取整，因此不能写成 x //= 10
            x = (x - digit) // 10
            rev = rev * 10 + digit
        
        return rev
```

Rust:
```Rust
impl Solution {
    pub fn reverse(x: i32) -> i32 {
        let mut x = x;
        let mut reversed = 0;

        while x != 0 {
            let last_digit = x % 10;
            x /= 10;

            // 检查溢出
            if reversed > i32::MAX / 10 || (reversed == i32::MAX / 10 && last_digit > 7) {
                return 0;
            }
            if reversed < i32::MIN / 10 || (reversed == i32::MIN / 10 && last_digit < -8) {
                return 0;
            }

            reversed = reversed * 10 + last_digit;
        }

        reversed
    }
}
```

