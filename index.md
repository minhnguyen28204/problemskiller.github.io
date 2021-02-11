# Blog để lưu trữ solutions cho các bài tập online (Cses, vnoi, etc...)
## I. Đồ thị Cses problems
### 1) Counting Rooms
#### Code:
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
#### Solutions:
bfs từng tọa độ, nếu tại vị trí (i,j) chưa thăm thì bắt đầu bfs tại (i,j) và tăng số rooms lên 1.

### 2) Labyrinth
#### Code:
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
int stx, sty, enx, eny;
 
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
        for(int j=1; j<=m; j++){
            cin >> a[i][j];
            if (a[i][j] == 'A') stx = i, sty = j;
            if (a[i][j] == 'B') enx = i, eny = j;
        }
    }
}
 
int d[N][N];
ii trace[N][N];
int dx[4] = {1,-1,0,0};
int dy[4] = {0,0,1,-1};
 
void bfs()
{
    queue<ii> q;
    q.push(ii(stx,sty));
    d[stx][sty] = 0;
    trace[stx][sty] = ii(-1,-1);
    while (q.size())
    {
        int u = q.front().fi;
        int v = q.front().se;
        q.pop();
        for(int i=0; i<4; i++)
        {
            int x = u + dx[i];
            int y = v + dy[i];
            if (a[x][y] == '#' || x < 1 || x > n || y < 1 || y > m || a[x][y] == 'A') continue;
            if (!d[x][y])
            {
                d[x][y] = d[u][v] + 1;
                trace[x][y] = ii(u,v);
                q.push(ii(x,y));
            }
        }
    }
}
 
void find_path()
{
    stack<char> st;
    int x = enx;
    int y = eny;
    while (x != -1 && y != -1)
    {
        int u = trace[x][y].fi;
        int v = trace[x][y].se;
        int diffx = x-u;
        int diffy = y-v;
        if (diffx > 0 && diffy == 0) st.push('D');
        else if (diffx < 0 && diffy == 0) st.push('U');
        else if (diffy > 0 && diffx == 0) st.push('R');
        else if (diffy < 0 && diffx == 0) st.push('L');
        x = u;
        y = v;
    }
    while (st.size())
    {
        cout << st.top();
        st.pop();
    }
}
 
void proc()
{
    bfs();
    if (d[enx][eny]) cout << "YES \n";
    else {cout << "NO \n"; return ;}
    cout << d[enx][eny] << '\n';
    find_path();
}
 
signed main()
{
    readfile();
    proc();
    return 0;
}
```

#### Solution:
Dfs từ điểm A, gọi d[i][j] là khoảng cách nhỏ nhất để đi từ A đến (i,j), pair<int,int> trace[i][j] để lưu vị trí trước và truy vết.
