###### Blog để lưu trữ solutions cho các bài tập online (Cses, vnoi, etc...)
### I. Đồ thị Cses problems
## 1) Counting Rooms
# Code:
```C++
//Nguyen Huu Hoang Minh
#include <bits/stdc++.h>
#define sz(x) int(x.size())
#define all(x) x.begin(),x.end()
#define reset(x) memset(x, 0,sizeof(x))
#define pb push_back
#define mp make_pair
#define fi first
#define se second
#define N 1005
#define remain(x) if (x > MOD) x -= MOD
#define ii pair<int, int>
#define vi vector<int>
#define vii vector< ii >
#define bit(x, i) (((x) >> (i)) & 1)
#define Task "test"
#define int long long
 
using namespace std;
 
typedef long double ld;
 
int n, m;
char a[N][N];
 
void readfile()
{
    ios_base::sync_with_stdio(false);
    cin.tie(0);cout.tie(0);
    if (fopen(Task".inp","r"))
    {
        freopen(Task".inp","r",stdin);
        //freopen(Task".out","w",stdout);
    }
    cin >> n >> m;
    for(int i=1; i<=n; i++)
    {
        for(int j=1; j<=m; j++) cin >> a[i][j];
    }
}
 
int d[N][N];
int dx[4] = {1,-1,0,0};
int dy[4] = {0,0,1,-1};
 
void dfs(int x, int y)
{
    d[x][y] = 1;
    for(int i=0; i<4; i++)
    {
        int xx = x + dx[i];
        int yy = y + dy[i];
        if (!d[xx][yy] && a[xx][yy] == '.')
            dfs(xx,yy);
    }
}
 
void proc()
{
    int ans = 0;
    for(int i=1; i<=n; i++)
    {
        for(int j=1; j<=m; j++)
        {
            if (a[i][j] == '.' && !d[i][j]) dfs(i,j), ++ans;
        }
    }
    cout << ans;
}
 
signed main()
{
    readfile();
    proc();
    return 0;
}
```
# Solutions:
bfs từng tọa độ, nếu tại vị trí (i,j) chưa thăm thì bắt đầu bfs tại (i,j) và tăng số rooms lên 1.
