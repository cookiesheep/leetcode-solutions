```cpp
#include<iostream>
using namespace std;

int a[100005],sum[100005];
int main()
{
    int n;
    cin>>n;
    int presum=0;
    for(int i=0;i<n;i++)
    {
        cin>>a[i];
        presum+=a[i];
        sum[i]=presum;
    }
    int a,b;
    while(cin>>a>>b)
    {
        cout<<sum[b]-sum[a-1]<<endl;   
    }
    return 0;
    
}
```
