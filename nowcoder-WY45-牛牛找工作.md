## 牛客网 19校招 网易45题 牛牛找工作

题目类型：模拟，贪心，排序

题目链接：https://www.nowcoder.com/practice/46e837a4ea9144f5ad2021658cb54c4d?tpId=98&tqId=32824&tPage=1&rp=1&ru=/ta/2019test&qru=/ta/2019test/question-ranking

题目大意：帮人找工作，设定工作有难度Di和报酬Pi两个属性，求职者有能力值Ai一项属性，给出n种工作，m个人，按人的输入顺序给出这些人所能拿到的最大薪资值。多个样例。

题目分析：会卡时，需要尽可能优化时间，n方的算法一定TLE，那么只可能n*logn，立刻想到排序，先把工作数组优化一下，因为能力能覆盖更高要求的工作时，更低要求的工作一定也能胜任，这时拿到的工资必定是其中最高的，所以先把工作按能力要求排序，然后把其报酬修改为（非严格）升序，方便后续处理。将求职者记下序号（用来保证最后的输出顺序），按能力值排序，这样顺刷一遍，就能得到每个人的工资，然后按输入顺序排序回来，直接输出，其中两趟排序的复杂度是n*logn，顺序查找的复杂度是线性，我的总用时225ms。

```c++
#include<iostream>
#include<algorithm>
#include<vector>

using namespace std;

int main()
{
    int m,n,d,p,a;
    while(cin>>n>>m)
    {
        vector<pair<int, int> >job(n+1);
        vector<pair<int, pair<int,int> > >guy(m);
        //三元组guy中的第一维是序号，第二维中的第一维是能力，第二维是工资
        for(int i=1;i<=n;i++)
        {
            cin >> job[i].first >> job[i].second;
        }
        sort(job.begin(),job.end(),[&](pair<int,int>a,pair<int,int>b){return a.first<b.first;});
        int mx=0;
        for(int i=1;i<=n;i++)
        {
            mx=max(mx,job[i].second);
            job[i].second=mx;
        }
        for(int i=0;i<m;i++)
        {
            cin>>a;
            guy[i].second.first=a;
            guy[i].first=i;
        }
        sort(guy.begin(),guy.end(),[&](pair<int,pair<int,int> >a,pair<int,pair<int,int> >b){return a.second.first<b.second.first;});
        int left=0,index=0;
        while(left < m && index < n + 1) {
            if(guy[left].second.first >= job[index].first) ++ index;
            else {
                guy[left].second.second = job[index - 1].second;
                ++ left;
            }
        }
        for(int i = left; i < m; ++ i) {
            guy[i].second.second = job[n].second;
        }
        sort(guy.begin(),guy.end(),[&](pair<int,pair<int,int> >a,pair<int,pair<int,int> >b){return a.first<b.first;});
        for(vector<pair<int, pair<int,int> > >::iterator it=guy.begin();it<guy.end();it++)
        {
            cout<<it->second.second<<endl;
        }
    }
    return 0;
}
```

PS：今天起转战牛客校招，本来想来虐一虐水题，结果被第一道题虐了，查题解做出来的，就是NarcissusAbyss那个。学习了vector存pair用法，复习了排序的写法，我比他改进的地方在于我用了三元组，节省了代码，不知道是不是还节省了时间（我比他只少15ms）。

PPS：继续加油吧
