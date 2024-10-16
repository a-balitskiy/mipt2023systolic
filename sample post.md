---
title: "Тизер курса + теорема Липтона--Тарьяна"
permalink: sample
---

+ [<mark>Видео</mark>](https://drive.google.com/file/d/1RXC171bbQnui_-lpQU6ZCwRgLc0E3Bqb/view?usp=sharing)
+ [<mark>Доска</mark>]({{site.baseurl}}/whiteboard/lec1.pdf)


$\sum_i x_i = 1$

$$
\sum_i x_i = 1
$$

## ---Тезисы---

_Пермутоэдром_ \\(P_{n-1}\\) называется многогранник в \\(\\{(x_1, \ldots, x_n) \in \mathbb{R}^{n} ~\vert~ \sum x_i = n(n-1)/2\\} \cong \mathbb{R}^{n-1}\\), заданный как
+ выпуклая оболочка точек, получаемых из \\((0,1,\ldots,n-1)\\) всевозможными перестановками координат;
+ или многогранник Ньютона вандермондовского детерминанта \\(\det (x_i^{j-1})_{i,j=1}^n\\);
+ или сумма Минковского рёбер симплекса \\(\\{(x_1, \ldots, x_n) \in \mathbb{R}^{n} ~\vert~ x_i \ge 0, \sum x_i = 1\\}\\);
+ или ячейка Вороного решётки \\(A_{n-1}^*\\) (см. задачи).

> **Теорема.** \\((n-1)\\)-мерный объём \\(P_{n-1}\\) равен \\(n^{n-3/2}\\).

_Набросок доказательства._
Пермутоэдр является _графическим зонотопом_, то есть он представим в виде суммы Минковского
\\[
Z_G = \sum\limits_{(i,j) \in E(G)} [e_i, e_j],
\\]
где \\(G\\) --- клика на \\(n\\) вершинах. Зонотоп можно разрезать на параллелепипеды, которые представляют собой суммы Минковского \\((n-1)\\) рёбер, не лежащих в одной гиперплоскости. В нашем случае все они имеют объём \\(\sqrt{n}\\). Параллелепипеды разбиения графического зонотопа отождествляются с остовными деревьями в \\(G\\), а в клике их \\(n^{n-2}\\), что легко вывести из матричной теоремы Кирхгофа.
\\(\square\\)

## ---Cсылки---
+ L. Lovász, [Graphs and Geometry](http://web.cs.elte.hu/~lovasz/bookxx/geomgraphbook/geombook2019.01.11.pdf). _American Mathematical Society_ (2019).

<!-- {% raw %} -->

<!-- 123 -->

```cpp
#include <bits/stdc++.h>
using namespace std;
const pair<int, int> dir[4] = {{-1, 0}, {0, 1}, {1, 0}, {0, -1}};
const int maxn = 105;
char a[maxn][maxn];
bool vis[maxn][maxn];
int main()
{
	int _;
	cin >> _;
	while (_--)
	{
		int n;
		cin >> n;
		memset(vis, 0, sizeof(vis));
		for (int i = 0; i < n; i++)
			cin >> a[i];
		queue<pair<int, int>> q;
		for (int i = 0; i < n; i++)
		{
			for (int j = 0; j < n; j++)
			{
				if ((i == 0 || j == 0 || i == n - 1 || j == n - 1) && a[i][j] != '#')
				{
					vis[i][j] = true;
					q.emplace(i, j);
				}
			}
		}
		while (q.size())
		{
			auto it = q.front();
			q.pop();
			for (int i = 0; i < 4; i++)
			{
				int r = it.first + dir[i].first;
				int c = it.second + dir[i].second;
				if (r < 0 || r >= n || c < 0 || c >= n)
					continue;
				if (vis[r][c] || a[r][c] == '#')
					continue;
				vis[r][c] = true;
				q.emplace(r, c);
			}
		}
		int ans = 0;
		for (int i = 0; i < n; i++)
		{
			for (int j = 0; j < n; j++)
			{
				if (!vis[i][j] && a[i][j] == 'O')
					ans++;
			}
		}
		cout << ans << "\n";
	}
}
```

<!-- {% endraw %} -->

