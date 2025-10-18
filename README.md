挺明显的一道板子题。

## 题目大意

就是普通的二维费用背包，只是会给出 q 个询问，每个询问给出一个**总价格**和一个总**新鲜值**。
我们需要求出在不同的要求下可以获得的**最大美丽值**。

## 题目分析

回想一下，我们在做这类题目的时候，在计算出最终的答案的过程中，我们是不是也把每个状态的最优解也算出来了？所以，我们可以直接进行一次这样的预处理以获得全部状态的最优解，接下来输出就行了。

### 动态规划预处理

由于有两个需要注意的量，我们把动态规划数组设为两维的。

设 fi,j 为使用 i 费用，新鲜值为 j 时的最大美丽值。易得方程：

fi,j=max(fi,j,fi−costk,j−frk+bek)

## 代码实现

cpp

```
#include
#define int long long
using namespace std;
int n,m,f[1005][1005],tmp1,tmp2;
struct str{
    int cost,fr,be;
}q[505];
signed main()
{
    scanf("%lld%lld",&n,&m);//输入数据
    for(int j=0;j<=500;j++)
    {
        for(int k=1;k<=500;k++) f[j][k]=-0x7fffffff;
    }
    for(int i=1;i<=n;i++) scanf("%lld%lld%lld",&q[i].cost,&q[i].fr,&q[i].be);
    for(int i=1;i<=n;i++)//动态规划预处理
    {
        for(int j=500;j>=q[i].cost;j--)
        {
            for(int k=500;k>=0;k--) f[j][k]=max(f[j][k],f[j-q[i].cost][max(k-q[i].fr,0ll)]+q[i].be);//这里，我们不能直接将k定到q[i].fr以达到无需特判的效果，因为如果它小于0的话我们可以直接使用0的状态进行转移（血的教训呜呜呜）
        }
    }
    for(int i=1;i<=m;i++)//输出答案
    {
        scanf("%lld%lld",&tmp1,&tmp2);
        printf("%lld",max(0ll,f[tmp1][tmp2]));
        if(i!=m)printf("\n");
    }
    return 0;
}
```



\_\_EOF\_\_

![](https://github.com/linruicong)linruicong - **本文链接：** [https://github.com/linruicong/p/19149861](https://github.com)
- **关于博主：** 评论和私信会在第一时间回复。或者[直接私信](https://github.com):[悠兔机场加速器订阅](https://www.baijiatu.com)我。
- **版权声明：** 除特殊说明外，转载请注明出处～[知识共享署名-相同方式共享 4.0 国际许可协议]
- **声援博主：** 如果您觉得文章对您有帮助，可以点击文章右下角**【[推荐](javascript:void(0);)】**一下。
