

#                                        动态规划

* [Alchemist (dp 填表练习地址)](https://alchemist-al.com/algorithms/is-subsequence)

  ![image-20211006220212465](https://i.loli.net/2021/10/06/7JsHx1ilO3bLvQB.png)

### <font color =03A9F4>1. 判断子序列</font>

![image-20211006213354402](https://i.loli.net/2021/10/06/Mmlwo5HJLOVdav2.png)

> 一个比较直观的思路是双指针，但是数据量大了就不行，上 DP
>
> 为便于分清，设要验证的子序列名为sub ，主序列为sequence
>
> 对于前缀sub[ i ],若sub[ i ]是sequence[ j ]的子序列，则sub[ i ] 一定是sequence 的子序列
>
> 所以可以设二维dp方程 dp [ m+1] [ n+1] 行代表sub 列代表sequence
>
> 再初始化空串的状态，从小往大转移即可

状态方程如下：
$$
dp[i][j]=
\begin{cases}
  & true & if \quad dp[i-1][j-1]=true \ \&\& \ sub[i-1]==sequence[j-1]\\
  & false & else& 
\end{cases}
$$



![image-20211006222526292](https://i.loli.net/2021/10/06/ThCizdvUI2cxYm1.png)

**代码**

```c++
class Solution {
public:
    bool isSubsequence(string s, string t) {
         int m = s.length(), n = t.length();
         vector<vector<bool> > dp(m+1,vector<bool> (n+1,true));
         for(int i = 1; i < m+1; i++) dp[i][0] = false;
         //初始化dp
         for(int i = 1; i < m+1; i++){
             for(int j = 1; j < n+1; j++){
                 if(s[i-1] == t[j-1] && dp[i-1][j-1]){
                    dp[i][j] = true;
                    break;
                 }else{
                    dp[i][j] = false; 
                 }
             }
         }
         return dp[m][n];
    }
};
```





---



### <font color =03A9F4>2. 除数博弈</font>

![image-20211007222724655](https://i.loli.net/2021/10/07/869qldbYefzQgns.png)

> 这个博弈有个结论，但我们还是得用dp求解.

![image-20211007222857751](https://i.loli.net/2021/10/07/qiYzydCA1f6RHDZ.png)

> dp 思路如下：
>
> 对于1 2 的状态我们可以很容易推出 ：1 为先手false ，2 为先手 true
>
> 对于下一个状态 i ，我们依次枚举 [1 ，i -1 ]  如果有满足的因子 j ，且替换时可以把必败态转给对手，那么dp[ i ] = true

**状态方程如下：**
$$
dp[i] = ( \, !dp[i-j] \, \&\& \, i \% j == 0 \ )\, ? \,true : false
$$
**代码**

```c++
class Solution {
public:
    bool divisorGame(int n) {
        vector<bool> dp(n+1,false);
        dp[1] = false;
        dp[2] = true;
        for(int i = 3; i <= n; i++)
            for(int j = 1; j < i; j++)
                if(i%j == 0 && dp[i-j] == false){
                    dp[i] = true;
                    break;
                }
        return dp[n];
    }
};
```





---



### <font color='03A9F4'>3. 三步问题</font>

![image-20211008211446659](https://i.loli.net/2021/10/08/mitf78Pn9oyeW3B.png)

> 思路如下：
>
> 零阶：可以看成不动，那么有一种 1
>
> 一阶：只有一种 1
>
> 二阶：有两种 1+1 和 2
>
> 三阶：有 1+1+1 和 2+1 和 3
>
> 四阶： 四阶可以由一阶或二阶或三阶上来
>
> 那么四阶的总数为 1 + 2 + 4 = 7
>
> ......
>
> 不难想到
>
> 第n阶 = 第n-1阶 + 第n-2阶 + 第n-3 阶

**状态转移方程如下:**
$$
dp[i] = dp[i-1] + dp[i-2] + dp[i-3]
$$
**另外还要取模 关于取模公式如下：**
$$
(a+b) \% p = (a \% p + b \% p) \% p
$$
**代码**

```c++
class Solution {
public:
    static const long mod =1000000007;
    static const int N = 1000010;
    int dp[N];
    int waysToStep(int n) { 
        dp[0] = 1,dp[1] = 1, dp[2] = 2,dp[3] =4;
        for(int i = 4; i <= n; i++){
            dp[i] = (dp[i-1] % mod + dp[i-2] % mod + dp[i-3] % mod ) % mod;
        }
        return dp[n];
    }
};
```





___

### <font color='03A9F4'>4.  连续子数组最大和</font>

![image-20211010172750795](https://i.loli.net/2021/10/10/YF7GpRoxfunmMIU.png)

>思路如下：
>
>这道题，很容易想到一个前缀和的方法，但是容易超时。
>
>令 dp[i] 表示 以i结尾的连续子数组的最大和，对于dp[i+1] ,显然有
>
>dp[i+1] = max(dp[i] + nums[i+1] , nums[i+1])
>
>即dp[i] = max(dp[i-1] + nums[i] , nums[i])
>
>合并起来就是
>
>dp[i+1] = max(max(dp[i-1] + nums[i] , nums[i]) + nums[i+1], nums[i+1])
>
>其中dp[0] = nums[0]
>
>所以我们可以在枚举每个nums[i]结尾的子数组时，依次计算最大和，最后便可以得到答案了

**代码**

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp(n);
        
        dp[0] = nums[0];
        if(n == 1) return dp[0];

        dp[1] = max(dp[0]+nums[1], nums[1]);
        if(n == 2) return max(dp[1],dp[0]);

        for(int i = 2; i < n; i++){
            dp[i] =  max( dp[i-1] + nums[i] , nums[i]);
        }
        return *max_element(dp.begin(),dp.end());
    }
};
```

**可以发现 最后我们还要求一下最大的dp[i] 所以简化一下写法，就是下面这样啦**

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int ans = nums[0], pre = 0;
        for(auto && n : nums){
            pre = max(pre+n,n);
            ans = max(pre,ans);
        }
        return ans;
    }
};
```

