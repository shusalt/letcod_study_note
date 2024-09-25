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
