#include<cstdio>
#include<cstring>
#include<algorithm>
#include<cmath>
#define eps 1e-8
#define ll __int64
using namespace std;
const int N=200005;
ll a[N];
int num[N*10];
ll ans[N];
struct Query
{
    int l,r;
    int id;
}query[N];
int bsize;
int block[N];
bool cmp(Query q1,Query q2)
{
    return block[q1.l]<block[q2.l]||(block[q1.l]==block[q2.l]&&q1.r<q2.r);
}
int main()
{
    int n,q;
    scanf("%d%d",&n,&q);
    bsize=sqrt((double)n+eps);

    for(int i=1;i<=n;i++) {
        block[i]=i/bsize;
        scanf("%d",&a[i]);
    }

    for(int i=1;i<=q;i++){
        scanf("%d%d",&query[i].l,&query[i].r);
        query[i].id=i;
    }
    sort(query+1,query+q+1,cmp);
    int L=1,R=1;
    num[a[L]]++;
    ll sum=a[L];
    for(int i=1;i<=q;i++)
    {
        int l=query[i].l,r=query[i].r;
        while(R<r){
            R++;
            sum+=a[R]*(2ll*num[a[R]]+1ll);
            num[a[R]]++;
        }
        while(R>r){
            sum-=a[R]*(2ll*num[a[R]]-1ll);
            num[a[R]]--;
            R--;
        }
        while(L>l){
            L--;
            sum+=a[L]*(2ll*num[a[L]]+1ll);
            num[a[L]]++;
        }
        while(L<l){
            sum-=a[L]*(2ll*num[a[L]]-1ll);
            num[a[L]]--;
            L++;
        }
        ans[query[i].id]=sum;
    }

    for(int i=1;i<=q;i++)
    {
        printf("%I64d\n",ans[i]);
    }

    return 0;

}​
