## 牛客网 19校招 网易50题 矩形重叠

题目链接：https://www.nowcoder.com/practice/a22dd98b3d224f2bb89142f8acc2fe57?tpId=98&tags=&title=&diffculty=0&judgeStatus=0&rp=1

题目类型：几何

题目分析：判断两矩形是否重合，情况较复杂，有两直角边交叉的，有一段伸如另一矩形的，有呈“十”字状交叉的，有其中一个完全在另一个之内的。那么就需要改变一下方向，考虑没有重合的情况。没有重合，无非就是其中一个的下边比另一个的上边还低，或一个的左边比另一个的右边还靠右。按照题中数据格式，即x1[i]>x2[j]∪x1[j]>x2[i]∪y1[i]>y2[j]∪y1[j]>y2[i]，将此式取反即为有重叠的情况，x1[i]≤x2[j]∩x1[j]≤x2[i]∩y1[i]≤y2[j]∩y1[j]≤y2[i]，其中等号需处理为半开半闭区间，具体可见代码。

```c++
#include<stdio.h>
int main()
{
    int n,x1[55],y1[55],x2[55],y2[55];
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        scanf("%d",&x1[i]);
    for(int i=0;i<n;i++)
        scanf("%d",&y1[i]);
    for(int i=0;i<n;i++)
        scanf("%d",&x2[i]);
    for(int i=0;i<n;i++)
        scanf("%d",&y2[i]);
    int cnt,ans=0;
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            cnt=0;
            for(int k=0;k<n;k++)
            {
                if(x1[i]>=x1[k] && x1[i]<x2[k] && y1[j]>=y1[k] && y1[j]<y2[k])
                {
                    cnt++;
                }
            }
            if(cnt>ans)
                ans=cnt;
        }
    }
    printf("%d\n",ans);
    return 0;
}
```

PS：参考的题解，有一点至今不明，三重循环的最内层选取了一个矩形，但外两层是任选两矩形的两个点，这样是什么意思呢？网上的题解代码几乎全一样，但没有一个能说清楚的……
