## 牛客网 19校招 网易47题 安置路灯

题目链接：https://www.nowcoder.com/practice/3a3577b9d3294fb7845b96a9cd2e099c?tpId=98&tqId=32826&tPage=1&rp=1&ru=/ta/2019test&qru=/ta/2019test/question-ranking

题目类型：模拟，贪心

题目大意：在路上安置路灯，一个字符串表示路，路上有两种地块，'.'和'X'，点是必须照亮的地块，X是不用管的地块，每盏灯能照亮其安置的地块和旁边两块地，问最终完成照亮任务最少需要多少路灯。

题目分析：这题没什么坑，从分析到实现都比较容易，不卡时也不卡空间，当然我实现容易是因为用来python，用c/c++的话需要自己实现split函数，估计要麻烦一些。

```python
t=int(input())
while t>0:
    t-=1
    input()
    road=input()
    road_segments=road.split("XX")
    ans=0
    for i in road_segments:
        blocks=i.split("X")
        flag=False
        for block in blocks:
            blen=len(block)
            if flag:
                blen-=1;
                flag=False;
            ans+=int((blen+2)/3);
            if blen%3==1:flag=True
    print(ans)
```

PS：被逼无奈用了python，谢谢python救我（鞠躬）
