## 牛客网 19校招 网易49题 数对

题目链接：https://www.nowcoder.com/practice/bac5a2372e204b2ab04cc437db76dc4f?tpId=98&tags=&title=&diffculty=0&judgeStatus=0&rp=1

题目类型：数论

题目分析：就是找规律，然后按规律写程序。根据除数y，取x从1~n，其余数是1，2，3，……，y-1，0……这样的循环规律，其中k≤y≤n时结果符合要求，n/y得到总共有几个整循环，再计算出不足整循环的数的个数。

```c++
#include<stdio.h>
#define max(x,y) ((x)>(y)?(x):(y))
int main() {
    int n, k;
    while (~scanf("%d%d", &n, &k)) { 
        int y;  
        long long count = 0; 
        if(!k)
        {
            count=n;
            count*=n;
            printf("%lld\n",count);
            continue;
        }
        for (y = k+1; y <= n; ++y) { 
            count += (n / y)*(y - k) + max(n%y+1-k, 0); 
            if (!k) count--; 
        } 
        printf("%lld\n", count); 
    } 
    return 0;
}

```

PS：没能自己做出来，参考的题解。得到教训：这种找规律的题，如果从一个角度不能总结出规律，就应该换一个角度继续找。
