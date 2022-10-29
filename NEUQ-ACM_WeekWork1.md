# NEUQ-ACM WeekWork1

## 1.乒乓球

注意比赛结束条件：分差大于2才能结束

```C++
#include <bits/stdc++.h>
using namespace std;

int main()
{
    char c;
    int w11[1000]={0},l11[1000]={0},w21[1000]={0},l21[1000]={0};		//不同分制下的赢输局数
    int i11=0,i21=0;													//局目的计数器
    
    while((c=getchar())!='E')
    {
        if(c=='W') w11[i11]++,w21[i21]++;
        else if(c=='L') l11[i11]++,l21[i21]++;
        else if(c=='\n') continue;										//每20个字母一个换行，跳过
        if((w11[i11]>=11||l11[i11]>=11)&&abs(w11[i11]-l11[i11])>=2) 	//赛制要求
        {
            i11++;
        }
        if((w21[i21]>=21||l21[i21]>=21)&&abs(w21[i21]-l21[i21])>=2)
        {
            i21++;
        }
    }
    
    int n11=999,n21=999;												//抹零环节
    for(n11=999;w11[n11]==0;n11--);
    for(n21=999;w21[n21]==0;n21--);
    
    for(int i=0;i<=n11;i++)												//输出
        printf("%d:%d\n",w11[i],l11[i]);
    printf("\n");
    for(int i=0;i<=n21;i++)
        printf("%d:%d\n",w21[i],l21[i]);
    return 0;
}
```



## 2.高精度加法

按照竖式加法模拟

```C++
#include <bits/stdc++.h>
using namespace std;

int main()
{
    string num1,num2;							//采用字符串处理数字
    cin>>num1>>num2;
    vector<int> a,b,c;
    for(int i=num1.size()-1;i>=0;i--)
        a.push_back(num1[i]-'0');
    for(int i=num2.size()-1;i>=0;i--)
        b.push_back(num2[i]-'0');
    int t=0;
    for(int i=0;i<a.size()||i<b.size();i++)
    {
        if(i<a.size()) t+=a[i]+b[i];			//普通的竖式加法模拟
        c.push_back(t%10);
        t/=10;									//处理进位
    }
    if(t!=0) c.push_back(t);					//补入最高位进位
    for(int i=c.size()-1;i>=0;i--)
    {
        printf("%d",c[i]);						//输出
    }
    return 0;
} 
```



## 3.高精度累加和

使用等差数列求和公式



面对循环累加和，程序对此的反应是。。。。。。

给我超时，三回啊三回

```C++
#include <bits/stdc++.h>
using namespace std;
#define N 1000

vector<int> div(vector<int>& A, int b)
{
	vector<int> C;
	int r = 0;
	for (int i = A.size() - 1; i >= 0; i--)
	{
		r=r*10+A[i];
		C.push_back(r/b);
		r%=b;
	}
	reverse(C.begin(), C.end());
	while (C.size()>1&&C.back()==0)
        C.pop_back();
	return C;
}
 
 
int main()
{
	string s;
	cin >> s;
    int l=s.size();
    int m=2*l;
	int a[N],b[N],c[N]={0};
	
	for (int i=0;i<l;i++)
    {
		a[i]=s[l-i-1]-'0';
		b[i]=s[l-i-1]-'0';
	}
	b[0]+=1;                                	//(n+1)
	
	for (int i=0;i<l;i++)
    {
		for (int j=0;j<l;j++)
        {
			c[i+j]+=a[i]*b[j];        			//乘法部分，n*(n+1)
		}
	}
	for (int i=0;i<m;i++)
    {
		if (c[i]>=10) 
        {
			c[i+1]+=c[i]/10;            		//处理进位
			c[i]%=10;
		}
	}
	
	while (m>0&&c[m]==0) 
        m--;									//抹去多余的0
	vector<int> d;
	for (int i=0;i<=m;i++)
		d.push_back(c[i]);
	vector<int> result = div(d,2);         		//除以2
	for (int i=result.size()-1;i>=0;i--)
        cout<<result[i];
	return 0;
}
```

本来想定义结构体然后暴力重载，但是写不动了，附一个半成品代码留档

```c++
#include <bits/stdc++.h>
using namespace std;

struct xlNum
{
    vector<int> n;
    
    void operator= (string s)
    {
        for(int i=0;i<s.size();i++)
        {
            n.push_back(s[i]-'0');
        }
        reverse(n.begin(),n.end());
    }
    void operator= (xlNum a)
    {
        for(int i=0;i<a.n.size();i++)
        {
            n.push_back(a.n[i]);
        }
    }
    xlNum operator+ (xlNum l)
    {
        xlNum c;
        int t=0;
        for(int i=0;i<n.size()||i<l.n.size();i++)
        {
            t+=n[i]+l.n[i];
            c.n.push_back(t%10);
            t/=10;
        }
        if(t==1) c.n.push_back(t);
        return c;
    }
    xlNum operator* (int a)
    {
        xlNum p;
        int t=0;
        for(int i=0;i<n.size();i++)
        {
            t+=n[i]*a;
            p.n.push_back(t%10);
            t/=10;
        }
        if(t!=0) p.n.push_back(t);
        return p;
    }
    xlNum operator* (xlNum a)
    {
        
        string z="0";
        xlNum p;
        p=z;
        xlNum t[n.size()];
        for(int i=0;i<n.size();i++)
        {
            t[i]=a*n[i]; 
            for(int j=0;j<i;j++)
            {
                t[i].print();
                t[i].n.insert(t[i].n.begin()+j,0);
            }
        }
        for(int i=0;i<n.size();i++)
        {
            p=p+t[i];
        }
        return p;
    }
    
    xlNum operator/ (int b)
    {
	    xlNum C;
	    int r = 0;
	    for (int i = n.size() - 1; i >= 0; i--)
	    {
	    	r = r * 10 + n[i];
	    	C.n.push_back(r / b);
	    	r %= b;
	    }
	    reverse(C.n.begin(), C.n.end());
	    while (C.n.size() > 1 && C.n.back() == 0) C.n.pop_back();
	    return C;
    }
    void print()
    {
        for(int i=n.size()-1;i>=0;i--)
        {
            printf("%d",n[i]);
        }
        printf("\n");
    }
};

int main()
{
    string s1,s2;			//纯测试用主函数，与题无关
    cin>>s1>>s2;
    xlNum n1,n2,n3;
    n1=s1;
    n2=s2;
    n3=n1*n2;
    n3.print();
    return 0;
}
```

