## AC自动机入门(以hdu2222为例)

前置知识点：
1. trie树
2. 失配指针概念（参考KMP的next数组）

题目链接：http://acm.hdu.edu.cn/showproblem.php?pid=2222

AC自动机简析：

  AC自动机其实就是增强版trie树，其作用一样是字符串多模式匹配，与trie树相比，增强之处就是多了一个fail数组，或者叫失配指针域，提供类似KMP的功能，在失配的时候无需从头开始匹配，而是回到可能的最近点处直接匹配下一字符，这使得trie树的效率大大提高。下面以hdu2222为例，使用AC自动机解决此题。
  
  ![](/assets/img/AC自动机初学/0.jpg)
  
  第一步建树，和trie树一样，建出trie树如上图，其中蓝色边框的是单词结束节点。
  
  ![](/assets/img/AC自动机初学/1.jpg)
  
  然后开始用BFS算法层序遍历trie树，先将根节点的直接子节点的fail域赋值指向根节点，如上图。
  
  ![](/assets/img/AC自动机初学/2.jpg)
  
  遍历时，处理队列中每个节点的所有子节点，若某节点p的某子节点存在，则将此子节点的fail域设为p节点的fail域对应的子节点(有点绕，看图+代码肯定能明白)。若p节点不存在此子节点，那么此子节点域也不能指向NULL，而是要指向p节点的fail域所对应的此子节点。AC自动机全部建完如上图，其中黑色虚线是fail指针，红色字的节点是不存在的子节点域；为了方便看图，除第一层外，指向根节点的fail指针都没有画出(用虚线箭头就没了QAQ，但是肯定都是从下层指向上层的)。

AC自动机大概就是这样，下面上题目的AC代码

```c++
#include<stdio.h>
#include<string.h>
#include<queue>
using namespace std;
//hdu2222 Keywords Search
int node[240000][26],trie_end,tail[240000],fail[240000];
void create_trie(char*str)
{
    int p=0;
    for(int i=0;i<strlen(str);i++)
    {
        int id=str[i]-'a';
        if(node[p][id]==0)
        {
            node[p][id]=trie_end++;
            memset(node[node[p][id]],0,sizeof(int)*26);
            tail[node[p][id]]=0;
        }
        if(i==strlen(str)-1){
            tail[node[p][id]]++;
        }
        p=node[p][id];
    }
}
void put_fail()
{
    queue<int>q;
    for(int i=0;i<26;i++)
    {
        if(node[0][i])
        {
            fail[node[0][i]]=0;
            q.push(node[0][i]);
        }
    }
    while(!q.empty())
    {
        int now=q.front();
        q.pop();
        for(int i=0;i<26;i++)
        {
            if(node[now][i])
            {
                fail[node[now][i]]=node[fail[now]][i];
                q.push(node[now][i]);
            }
            else node[now][i]=node[fail[now]][i];
        }
    }
}
int search_trie(char*str)
{
    int ans=0,j,p=0;
    int l=strlen(str);
    for(int i=0;i<l;i++)
    {
        p=node[p][str[i]-'a'];
        for(j=p;j&&tail[j]!=-1;j=fail[j])
        {
            ans+=tail[j];
            tail[j]=-1;
        }
    }
    return ans;
}
void freetrie()
{
    memset(node,0,sizeof(int)*26*trie_end);
    memset(tail,0,sizeof(int)*trie_end);
    memset(fail,0,sizeof(int)*trie_end);
}
char input[66],desc[1000007];
int main()
{
    int t,n;
    scanf("%d",&t);
    while(t--)
    {
        trie_end=1;
        scanf("%d",&n);
        while(n--)
        {
            scanf("%s",input);
            create_trie(input);
        }
        put_fail();
        scanf("%s",desc);
        printf("%d\n",search_trie(desc));
        freetrie();
    }
    return 0;
}
```

PS：我参考的是 https://bestsort.cn/2019/04/28/402/ 这一篇，它的算法介绍里“如果不存在这个子节点我们就让他指向根节点”这句说错了，图也跟着错了，应该是指向其父节点的fail指针指向的节点的对应子节点，但是它代码里也有注释，代码和注释是对的。
