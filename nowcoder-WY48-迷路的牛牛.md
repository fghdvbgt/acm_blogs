## 牛客网 19校招 网易48题 迷路的牛牛

题目链接：https://www.nowcoder.com/practice/fc72d3493d7e4be883e931d507352a4a?tpId=98&tqId=32827&tPage=1&rp=1&ru=/ta/2019test&qru=/ta/2019test/question-ranking

题目类型：模拟

题目大意：转向，判断方向。初始面向北，给出一系列转向操作，判断最后是面向哪个方向。

```c++
#include<stdio.h>
#include<string.h>
//方向数组的含义：4个元素分别代表从朝向北向左转0123次，得到的方向
int main()
{
    int n,left;
    char direction[6]="NWSE",input[1009];
    while(scanf("%d",&n)!=EOF)
    {
        left=0;
        scanf("%s",input);
        for(int i=0;i<strlen(input);i++)
        {
            if(input[i]=='L')left++;
        }
        left-=strlen(input)-left;
        left%=4;
        if(left<0)left+=4;
        printf("%c\n",direction[left]);
    }
    return 0;
}
```

PS：纯水欢乐送，期待下一题
