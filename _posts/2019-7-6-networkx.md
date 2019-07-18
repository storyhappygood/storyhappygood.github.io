## Networkx的学习

### Graph分类

```
G = nx.Graph() # 创建无向图

G = nx.DiGraph() # 创建有向图

G = nx.MultiGraph() # 创建多重无向图

G = nx.MultiDigraph() # 创建多重有向图

G.clear() #清空图

```
### 基本操作


+ 节点

```
#添加节点

import networkx as nx
import matplotlib.pyplot as plt
 
G = nx.Graph()                 #建立一个空的无向图G
G.add_node('a')                  #添加一个节点1
G.add_nodes_from(['b','c','d','e'])    #加点集合
G.add_cycle(['f','g','h','j'])         #加环
H = nx.path_graph(10)          #返回由10个节点挨个连接的无向图，所以有9条边
G.add_nodes_from(H)            #创建一个子图H加入G
G.add_node(H)                  #直接将图作为节点

nx.draw(G, with_labels=True)
plt.show()

#访问节点

print('图中所有的节点', G.nodes())

print('图中节点的个数', G.number_of_nodes())

#删除节点

G.remove_node(1)    #删除指定节点
G.remove_nodes_from(['b','c','d','e'])    #删除集合中的节点

nx.draw(G, with_labels=True)

plt.show()
```

+ 边
```
#添加边

F = nx.Graph() # 创建无向图
F.add_edge(11,12)   #一次添加一条边

#等价于
e=(13,14)        #e是一个元组
F.add_edge(*e) #这是python中解包裹的过程

F.add_edges_from([(1,2),(1,3)])     #通过添加list来添加多条边

#通过添加任何ebunch来添加边
F.add_edges_from(H.edges()) #不能写作F.add_edges_from(H)

nx.draw(F, with_labels=True)
plt.show()

#访问边

print('图中所有的边', F.edges())

print('图中边的个数', F.number_of_edges()) 

#快速遍历每一条边，可以使用邻接迭代器实现，对于无向图，每一条边相当于两条有向边
FG = nx.Graph()
FG.add_weighted_edges_from([(1,2,0.125), (1,3,0.75), (2,4,1.2), (3,4,0.275)])
for n, nbrs in FG.adjacency():
    for nbr, eattr in nbrs.items():
        data = eattr['weight']
        print('(%d, %d, %0.3f)' % (n,nbr,data))

print('***********************************')

#筛选weight小于0.5的边：
FG = nx.Graph()
FG.add_weighted_edges_from([(1,2,0.125), (1,3,0.75), (2,4,1.2), (3,4,0.275)])
for n, nbrs in FG.adjacency():
    for nbr, eattr in nbrs.items():
        data = eattr['weight']
        if data < 0.5:
            print('(%d, %d, %0.3f)' % (n,nbr,data))
print('***********************************')

#一种方便的访问所有边的方法:
for u,v,d in FG.edges(data = 'weight'):
    print((u,v,d))

#删除边

F.remove_edge(1,2)
F.remove_edges_from([(11,12), (13,14)])

nx.draw(F, with_labels=True)

plt.show()
```

+ 属性

属性如weight，labels，colors，或者任何对象，你都可以附加到图，节点或边上。
```
#图的属性

import networkx as nx
import matplotlib.pyplot as plt

G = nx.Graph(day='Monday')    #可以在创建图时分配图的属性
print(G.graph)

G.graph['day'] = 'Friday'     #也可以修改已有的属性
print(G.graph)

G.graph['name'] = 'time'      #可以随时添加新的属性到图中
print(G.graph)
```
```
#节点的属性

G = nx.Graph(day='Monday')
G.add_node(1, index='1th')             #在添加节点时分配节点属性
print(G.node(data=True))

G.node[1]['index'] = '0th'             #通过G.node[][]来添加或修改属性
print(G.node(data=True))

G.add_nodes_from([2,3], index='2/3th') #从集合中添加节点时分配属性
print(G.nodes(data=True))

print(G.node(data=True))
```
```
#边的属性

G = nx.Graph(day='manday')
G.add_edge(1,2,weight=10)                    #在添加边时分配属性
print(G.edges(data=True))

G.add_edges_from([(1,3), (4,5)], len=22)     #从集合中添加边时分配属性
print(G.edges(data='len'))

G.add_edges_from([(3,4,{'hight':10}),(1,4,{'high':'unknow'})])
print(G.edges(data=True))

G[1][2]['weight'] = 100000                   #通过G[][][]来添加或修改属性
print(G.edges(data=True))
```

+ 无向图和有向图之间的转化
```
#有向图转化成无向图

H=DG.to_undirected()
#或者
H=nx.Graph(DG)

#无向图转化成有向图

F = H.to_directed()
#或者
F = nx.DiGraph(H)
```
+ 一些函数

*图* 

degree(G[, nbunch, weight])：返回单个节点或nbunch节点的度数视图。 <br>
degree_histogram(G)：返回每个度值的频率列表。<br>
density(G)：返回图的密度。<br>
info(G[, n])：打印图G或节点n的简短信息摘要。<br>
create_empty_copy(G[, with_data])：返回图G删除所有的边的拷贝。<br>
is_directed(G)：如果图是有向的，返回true。<br>
add_star(G_to_add_to, nodes_for_star, **attr)：在图形G_to_add_to上添加一个星形。<br>
add_path(G_to_add_to, nodes_for_path, **attr)：在图G_to_add_to中添加一条路径。<br>
add_cycle(G_to_add_to, nodes_for_cycle, **attr)：向图形G_to_add_to添加一个循环。<br>
*节点*

nodes(G)：在图节点上返回一个迭代器。<br>
number_of_nodes(G)：返回图中节点的数量。<br>
all_neighbors(graph, node)：返回图中节点的所有邻居。<br>
non_neighbors(graph, node)：返回图中没有邻居的节点。<br>
common_neighbors(G, u, v)：返回图中两个节点的公共邻居。<br>

*边*

edges(G[, nbunch])：返回与nbunch中的节点相关的边的视图。<br>
number_of_edges(G)：返回图中边的数目。<br>
non_edges(graph)：返回图中不存在的边。<br>

*out_degee()函数*
1. 使用out_degree()函数查找所有带有子项的节点：
```
>>> [k for k,v in G.out_degree().iteritems() if v > 0]

['n13', 'n', 'n131', 'n1', 'n22', 'n2', 'n221', 'n4']
```
2. 所有没有孩子的节点
```
>>> [k for k,v in G.out_degree().iteritems() if v == 0]

['n12', 'n11', 'n3', 'n41', 'n21', 'n5']
```
3. 所有孤儿节点，即度数为0的节点
```
>>> [k for k,v in G.degree().iteritems() if v == 0]
['n5'] 
```
4. 度超过2的节点
```
>>> [k for k,v in G.out_degree().iteritems() if v > 2]
['n', 'n1']
```
+ 如何画复杂网络图

NetworkX主要不是一个图形绘制软件包，但它包含Matplotlib的基本绘图以及使用开源Graphviz软件包的界面。这些是networkx.drawing模块的一部分。首先引入matplotlib:
```
import matplotlib.pyplot as plt
```
最基础的一个函数是nx.draw(G,pos=None,ax=None,**kwds),其中pos即图中各点的位置信息，以下几个函数可以以某种算法生成各点的坐标：
1. circular_layout(G,scale=1,center=None,dim=2)    # 将点以圈的形状摆放

参数介绍：

G:networkx定义的图

scale：摆放图的比例因子，该参数是数值，默认为1

center：以布局为中心的坐标对

dim(int):布局尺寸，一般为2.

2. random_layout(G,center=None,dim=2,seed=None)    # 在单位正方形内均匀随机定位节点



