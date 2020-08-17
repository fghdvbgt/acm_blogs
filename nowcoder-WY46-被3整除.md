## 牛客网 19校招 网易46题 被3整除

题目链接：https://www.nowcoder.com/practice/51dcb4eef6004f6f8f44d927463ad5e8?tpId=98&tqId=32825&tPage=1&rp=1&ru=/ta/2019test&qru=/ta/2019test/question-ranking

题目类型：数论

题目大意：一个有某种规律的数列，给出左右端点的序号，让找里面有多少数能被3整除。

题目分析：这题用到的技术只有一个——找规律。题目难度相当于小学奥数，涉及整除，那么用到的就是数论中的环理论，有两个数，那么就是找两层环。就这样。

```c
#include<stdio.h>
int main()
{
    int l,r,ans,mod,lmod;
    while(~scanf("%d%d",&l,&r))
    {
        ans=((r-l+1)/3+1)*2;
        mod=(r-l+1)%3;
        lmod=l%3;
        if(lmod==1&&mod)
        {
            ans-=(3-mod);
        }
        if(lmod==2&&mod==1)
        {
            ans-=1;
        }
        printf("%d\n",ans);
    }
}
```

PS：遇到数论的简单题还是很开心的^^
