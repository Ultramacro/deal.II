<center><font size=6 color=blue>deal.II learning note</font></center>

[toc]

# 1.deal.II介绍

deal.II是一个开放源代码的有限元程序库，是一个C++软件库，支持创建有限元代码以及开放的用户和开发人员社区。

deal.II 是一个开源的有限元法求解器，支持大规模并行计算，自适应网格。采用C++编写，实现优雅。其文档完整丰富，文档共有三个级别，由浅入深：

- tutorial：一系列的教学程序，共有64步教学步骤，通过tutorial的学习可以对dealii有整体的认识。
- manual：对每个类以及相应的函数的介绍。适合用于查询类与函数的具体用法。
- Modules：介绍了实现某一个功能需要用到的一系列类与函数，比如 Sparsity patterns 介绍了存储稀疏矩阵相关的内容。

本deal.II学习笔记基于[deal.II官方文档](https://www.dealii.org/developer/doxygen/deal.II/index.html)，学长的[学习笔记](https://ghostvalley.top/categories/dealii/)和[Wolfgang Bangerth's lectures](https://www.bilibili.com/video/BV12x411d7Uv?from=search&seid=9519040821080786689)。

# 2.deal.II安装

# 3.deal.II示例学习

## 3.1.Step-1

相关链接：[deal.II step-1 tutorial program](https://www.dealii.org/developer/doxygen/deal.II/step_1.html)

step-1的源码位于**examples/step-1**目录，进入该目录并输入如下命令进行编译（对于其它的step项目同样需要进行如下的编译）：

```
cmake .			# 生成makefile，会查找deal.II库
make			# 生成可执行文件
make run		# 执行可执行文件，也会编译代码，所以第二句代码可忽略
```

如`cmake .`报错，如果此命令无法找到deal.II库，则需要使用以下命令提供安装路径：

```
cmake -DDEAL_II_DIR=/path/to/installed/deal.II .
```

<font size=5>**内容说明**</font>

step-1的主要内容是网格生成。网格有两种，一是方形网格，二是环形网格，并展示了网格迭代细化的过程。

有限元程序的三个过程：网格的Triangulation类型的对象；调用GridGenerator函数以生成网格；并在相关迭代器的所有单元上循环；

<font size=5>**示例程序**</font>

**加载头文件**

首先需要加载头文件，最为重要的是 Triangulation 类，其用于生成单元，Triangulation<1>表示一维单元，以此类推，可以表示二维单元和三维单元，对于边界单元，Triangulation<1,2>表示面边界上的曲线单元，Triangulation<2,3>表示体边界上的曲面单元。

```C++
#include <deal.II/grid/tria.h>
```

加载以下两个与在单元格和（或）面上的循环的头文件，实现单元存取和迭代：

```C++
#include <deal.II/grid/tria_accessor.h>
#include <deal.II/grid/tria_iterator.h>
```

生成具有一点过标准形状的网格：

```C++
#include <deal.II/grid/grid_generator.h>
```

网格的格式化输出：

```C++
#include <deal.II/grid/grid_out.h>
```

C++输入输出：

```C++
#include <iostream>
#include <fstream>
```

载入库cmath（数学运算库）：

```C++
#include <cmath>	// for std::sqrt and std::fabs
```

最后加上命名空间dealii，确保调用的函数来自dealii库。

```C++
using namespace dealii;
```

**创建第一个网格（正方形网格）**

首先申明二维单元triangulation，然后设置单元为立方体形状，并对单元进行四次全局细化，每次细化一分为四，总共将产生$4^4=256$个单位网格。最终将网格绘制成eps图像输出（或其它图像格式，如*.svg）。

```C++
void first_grid()
{
  Triangulation<2> triangulation;
  GridGenerator::hyper_cube(triangulation);
  triangulation.refine_global(4);
  std::ofstream out("grid-1.eps");
  GridOut       grid_out;
  grid_out.write_eps(triangulation, out);
  std::cout << "Grid written to grid-1.eps" << std::endl;
}
```

**创建第二个网格（环形网格）**

同样首先申明二维单元triangulation，然后设置中心点，内外圆的半径，并用hyper_shell函数生成网格，可以通过此函数自动调整圆周单元的数量，最后一个参数显式设置为10，即内外圈分为10个环带网格。

```C++
void second_grid()
{
  Triangulation<2> triangulation;
  const Point<2> center(1, 0);
  const double   inner_radius = 0.5, outer_radius = 1.0;
  GridGenerator::hyper_shell(
    triangulation, center, inner_radius, outer_radius, 10);
```

> 默认情况下，triangulation假定所有边界均为直线，为保证区域边界是弯曲的，引入一个manifold indicator，如果没有manifold描述与特定的manifold indicator关联，则表示产生笔直边缘的manifold。

然后通过五次（自定义）循环细化网格：

```C++
for (unsigned int step = 0; step < 5; ++step)
  {
```

>triangulation的单元格并不是数组方式储存，而是以迭代器（[iterator](https://en.wikipedia.org/wiki/Iterator#C.2B.2B)）的方式进行储存，包含指针，迭代器的基本操作见C++学习笔记。
>
>active cell是未进一步细化的单元，并且是可以标记为进一步细化的单元，即已激活的网格，所以遍历的是最细的网格。

遍历所有active cell：

```C++
for (auto it = triangulation.active_cell_iterators().begin();
     it != triangulation.active_cell_iterators().end();
     ++it)
  {
    auto cell = *it;
    // Then a miracle occurs...
  }
```

上面的写法需要声明循环的初始与结束条件，在此还可以采用更为简便的方式：

```C++
for (auto &cell : triangulation.active_cell_iterators())
  {
```

获取单元的维度：

```C++
   for (const auto v : cell->vertex_indices())
  	{
```

在此细化的策略为：如果网格是靠近圆环内边沿的网格，即有节点在圆环内径上，那么就加密这个网格。由于计算机机内小数表示有误差，因此不能直接判断等于，而是差值绝对值小于一个极小数，该极小数设置为等于环的内半径的$10^{-6}$倍。

```C++
      const double distance_from_center =
        center.distance(cell->vertex(v));  // 网格节点
      if (std::fabs(distance_from_center - inner_radius) <=
          1e-6 * inner_radius)
        {
          cell->set_refine_flag();  // 标记为active cell
          break;
        }
    }
}
```

已经标记了所有要细化的单元，接下来执行网格的稀疏和细化函数即可：

```C++
  triangulation.execute_coarsening_and_refinement();
}
```

最后输出网格的图像：

```C++
  std::ofstream out("grid-2.eps");
  GridOut       grid_out;
  grid_out.write_eps(triangulation, out);
  std::cout << "Grid written to grid-2.eps" << std::endl;
}
```

**main函数**

在main()调用之前生成两个网格的函数即可。

```C++
int main()
{
  first_grid();
  second_grid();
}
```

---

## 3.2.Step-2

相关链接：[deal.II step-2 tutorial program](https://www.dealii.org/developer/doxygen/deal.II/step_2.html)

<font size=5>**内容说明**</font>

在Step-1中创建了网格之后，Step-2将介绍如何在此网格上定义自由度。 在此示例中，我们将使用最低阶（$Q_1$）有限元，其自由度与网格的顶点相关。 在后面的示例将介绍高阶单元，在高阶有限元中，自由度不必再与顶点关联，而是可以与边缘，面或体相关联。

在有限元方法中，自由度（degree of freedom）有两个存在略微差异的意思：

* 将有限元解表示为形状函数的线性组合，即**$u_h(x)=\Sigma^{N-1}_{j=0}U_j\varphi_j(x)$**。式中，$U_j$是展开系数向量，其值未知，所以称之为未知量或自由度。
* 有限元问题的数学解释为，寻找一个满足某些方程组的有限维函数**$u_h\in V_h$**，如对所有的测试函数$\varphi_h\in V_h$均满足**$a(u_h,\varphi_h)=(f,\varphi_h)$**。首先需要选择空间$V_h$的一组基，是一组形状函数，特别选择由有限元函数描述的基元，这些函数通常是定义在网格和单元上的。所以，自由度即计算出的空间$V_h$的基函数数目，在deal.II中，类`DoFHandler`提供$V_h$基数目的计算，提供了自由度相关的功能。

  基于类`DoFHandler`，所以在deal.II中定义自由度变得很简单，需要做的即创建一个有限元对象，使用`DoFHandler::disturbute_dofs`函数进行有限元对象的自由度定义，能够从中获取局部的自由度和形状函数的下标等等，这些是确定系统矩阵的大小以及将单个单元的组成矩阵复制到全局矩阵时需要的信息。

**稀疏性**

稀疏性是有限元方法的显着特征之一，稀疏性有助于求解有数以万计自由度的矩阵问题。

在定义了自由度之后，便需要根据微分方程，计算相应的线性方程组，在Step-3中会讲解相应的过程。有限元法中非常重要的一点：有限元法线性方程组中的矩阵是稀疏的，即大多数系数为0。

更精确地说，如果矩阵中每行/列非零项的数量由一个与总自由度数量无关的数字所限制，则矩阵是**稀疏**的。例如，求解拉普拉斯方程的有限差分近似的简单5点法得到的解为稀疏矩阵，因为每行非零项的数量为5，与矩阵的总大小无关。对于更复杂的问题（例如，Step-22的斯托克斯问题），尤其是在三维中，每行的数字数目可能为数百。 但是重要的一点是，该数目与问题的整体大小无关：如果优化（精细）网格，则每行非零数的最大数目保持不变。

假设一个有N行的矩阵，其每行具有特定的非零数目上限，需要$O(N)$个存储位置进行存储（空间复杂度），而矩阵向量乘法也仅需要$O(N)$个操作（时间复杂度）。显然，如果矩阵不是稀疏的，通过$O(N)$个操作求解完成是不可能的，因为非稀疏矩阵中的项数必须为$O(N^s)$，且其中$s>1$，会进行$O(N^s)$次运算，这还是使用了多重网格法这种非常专业的求解器情况下。

在有限元方法中，稀疏性源于有限元形状函数是在单个单元上局部定义的，而不是全局定义的，并且局部微分算子仅与相邻的单元的形状函数有关，体现在矩阵中就是非零项，而非相邻项则为零，从而导致了矩阵的稀疏，即，未知量$i$，$j$所在的单元如果没有毗邻，则在最终的矩阵中$A_{ij}=A_{ji}=0$。

**自由度计算**

默认情况下，`DoFHandler`类随机处理网格上的自由度。 因此，稀疏矩阵也没有针对任何特定目的进行优化，即不是最优的。

对于大多数算法，对自由度进行编号的确切方式并不重要。如CG算法。但是也有一些算法对自由度的排布较为敏感，如SSOR、LU分解、Cholesky分解等。因此，deal.II中也包含了可以重新排列未知量的工具：`FRenumbering`。这个函数相比与随机排布有一定的优化。

<font size=5>**示例程序**</font>

**加载头文件**

同Step-1一样，首先导入相应的头文件：

```C++
#include <deal.II/grid/tria.h>
#include <deal.II/grid/tria_accessor.h>
#include <deal.II/grid/tria_iterator.h>
#include <deal.II/grid/grid_generator.h>
```

引入处理自由度的库：

```C++
#include <deal.II/dofs/dof_handler.h>
```

接下来引入与单元有关的库，在这个库种，包含了各种维度，各种阶次的拉格朗日单元的实现：

```C++
#include <deal.II/fe/fe_q.h>
```

引入处理自由度的工具：

```C++
#include <deal.II/dofs/dof_tools.h>
```

引入稀疏矩阵可视化网格的类：

```C++
#include <deal.II/lac/sparse_matrix.h>
```

引入中间稀疏模式结构：

```C++
#include <deal.II/lac/dynamic_sparsity_pattern.h>
```

对自由度进行重新排列：

```C++
#include <deal.II/dofs/dof_renumbering.h>
```

文件输出：

```C++
#include <fstream>
```

导入deal.II名字空间：

```C++
using namespace dealii;
```

**网格生成**

使用的是Step-1程序生成环形网格，并已经过数步网格优化,可以返回根据参数生成的网格。

```C++
void make_grid(Triangulation<2> &triangulation)
{
  const Point<2> center(1, 0);
  const double   inner_radius = 0.5, outer_radius = 1.0;
  GridGenerator::hyper_shell(
    triangulation, center, inner_radius, outer_radius, 5);
  for (unsigned int step = 0; step < 3; ++step)
    {
      for (auto &cell : triangulation.active_cell_iterators())
        for (const auto v : cell->vertex_indices())
          {
            const double distance_from_center =
              center.distance(cell->vertex(v));
            if (std::fabs(distance_from_center - inner_radius) <=
                1e-6 * inner_radius)
              {
                cell->set_refine_flag();
                break;
              }
          }
      triangulation.execute_coarsening_and_refinement();
    }
}
```

**自由度处理DoFHandler**

至此，已创建了一个网格，且节点和单元的几何信息和拓扑信息已基本明确。为了使用数值算法，我们需要将节点（或线，单元）的信息与自由度相关联，以便后续生成有限元的矩阵和向量。deal.II中`DoFHandler`类就是来完成这部分工作的。但是，在执行此操作之前，首先需要建立有限元单元来描述与对象相关联的自由度。衍生类`FE_Q`能够描述拉格朗日有限单元，它的构造函数采用一个参数来说明元素的多项式，如参数1表示形状函数为1阶多项式，假设参数为3，则将创建一盒有限单元，每个顶点具有一个自由度，每条线具有两个自由度，并且在单元内具有四个自由度。

首先需要建立一个有限单元，并用`DoFHandler`进行自由度处理：

```C++
void distribute_dofs(DoFHandler<2> &dof_handler)
{
  const FE_Q<2> finite_element(1);
  dof_handler.distribute_dofs(finite_element);
```

网格的每一个节点都有一个形状函数。求解拉普拉斯方程时，得到的矩阵中非零元素$a_{ij}$为每对相邻$(i,j)$形状函数梯度的积分（求和）。`DoFHandler :: distribute\_dofs()​`对顶点进行了或多或少的随机编号，因此矩阵中非零项的模式有些参差不齐，需要进一步的处理。

1. 首先需要一个数据结构来储存非零元素的位置，那么便可以根据这个存储下来的“稀疏模式”来存储矩阵中的值。`SparsityPattern`类可以完成位置的储存，其缺点在于当我们直接使用时，需要预估每一行（列）的最大非零项数目（预估值）。对于二维空间，可信的预估值可通过函数

   `DoFHandler::max\_couplings\_between\_dofs()`获得；
   对于三维空间，预估值一般都偏大，会造成储存空间的浪费，为防止这种浪费，引入`DynamicSparsityPattern`类型来创建内部数据空间便于无过载地转换成`SparsityPattern`类，其初始化需要给出矩阵的大小。

   ```C++
   DynamicSparsityPattern dynamic_sparsity_pattern(dof_handler.n_dofs(),
   										dof_handler.n_dofs());
   ```

2. 随后得到非零元素的位置：

   ```C++
   DoFTools::make_sparsity_pattern(dof_handler,dynamic_sparsity_pattern;
   ```

3. 创建实际的稀疏模式，以后可以将其用于矩阵:

   ```C++
   SparsityPattern sparsity_pattern;
   sparsity_pattern.copy_from(dynamic_sparsity_pattern);
   ```

4. 将结果写入.svg文件中，其中矩阵中的每个非零项都与图像中的红色正方形相对应。

   ```C++
   std::ofstream out("sparsity_pattern1.svg");
   sparsity_pattern.print_svg(out);
   }
   ```

>查看.svg文件，可以注意到稀疏模式是对称的。 这不足为奇，因为我们没有给`DoFTools :: make_sparsity_pattern`任何非对称矩阵信息；
>
>还将注意到，它具有几个不同的区域，这是由于编号从最稀疏的单元网格开始，然后移动到更精细的单元网格。

**自由度重新排布**

在之前程序生成的稀疏模式中，非零项离对角线很远，这对某些算法（如LU分解或者GS迭代）的使用是不利的，所以需要通过重新排布非零项来进行优化。

$(i,j)$为矩阵中的非零项，只有单元$i$和$j$相邻时，其值不为0，为了使非零项聚集在对角线附近，所以需要调整相邻的形状函数的索引号相差不大。（最优化问题）

这可以通过简单的前行算法来实现：从给定的顶点开始，并为其指定索引0。 然后，对其邻点进行连续编号，使其索引接近原始索引（1，2，3，...）。 然后，对邻点的邻点（如果尚未编号）进行编号，以此类推。

示例中采用的是由Cuthill和McKee提出的算法，在代码中调用`DoFRenumbering::Cuthill_McKee​`即可:

```C++
void renumber_dofs(DoFHandler<2> &dof_handler)
{
  DoFRenumbering::Cuthill_McKee(dof_handler);
  DynamicSparsityPattern dynamic_sparsity_pattern(dof_handler.n_dofs(),
                                                  dof_handler.n_dofs());
  DoFTools::make_sparsity_pattern(dof_handler, dynamic_sparsity_pattern);
  SparsityPattern sparsity_pattern;
  sparsity_pattern.copy_from(dynamic_sparsity_pattern);
  std::ofstream out("sparsity_pattern2.svg");
  sparsity_pattern.print_svg(out);
}
```

值得注意的是，`DoFRenumbering`类还提供了许多其他算法来对自由度进行重新编号。 例如，所有非零项都在矩阵的下三角或上三角中，但对于对称稀疏模式，这当然是无法实现的，但是在某些涉及输运方程的特殊情况下是可行的，如从流入边界沿流线到流出边界。

**主函数**

最后，用主函数来调用各函数，形成最终的程序：

```C++
int main()
{
  Triangulation<2> triangulation;
  make_grid(triangulation);
  DoFHandler<2> dof_handler(triangulation);
  distribute_dofs(dof_handler);
  renumber_dofs(dof_handler);
}
```

<font size=5>**结果**</font>

该程序运行后产生了两种稀疏模式。可以通过在Web浏览器中打开.svg文件来可视化它们。

![image-20201021144656115](C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20201021144656115.png)

左侧图片中的不同区域（左上角和其他部分网格区域）表示网格的不同细化级别上的自由度。 右侧图片的稀疏模式在重新编号后非零项离对角线更近了。

<font size=5>**拓展**</font>

首先，可以尝试更改单元的阶数，比如改成3或5，即`distribute_dofs`函数的参数设置为3或5。

或者，如果想要观察网格细化对矩阵的影响，将局部加密的步数（细化次数）改为4。

最后，还可以尝试`DoFRenumbering`名字空间中的其他的排布算法。

在可视化的方式上，可以采用`gnuplot`，在源代码函数 `distribute_dofs()` 和`renumber_dofs()`中将`print_svg()`改为`print_gnuplot()`。

```
examples/step-2> gnuplot
        G N U P L O T
        Version 3.7 patchlevel 3
        last modified Thu Dec 12 13:00:00 GMT 2002
        System: Linux 2.6.11.4-21.10-default
        Copyright(C) 1986 - 1993, 1998 - 2002
        Thomas Williams, Colin Kelley and many others
        Type `help` to access the on-line reference manual
        The gnuplot FAQ is available from
        http://www.gnuplot.info/gnuplot-faq.html
        Send comments and requests for help to <info-gnuplot@dartmouth.edu>
        Send bugs, suggestions and mods to <bug-gnuplot@dartmouth.edu>
Terminal type set to 'x11'
gnuplot> set style data points
gnuplot> plot "sparsity_pattern.1"
```

另一种基于GNUPLOT的做法是尝试打印出节点的位置和编号的网格。需要包括GridOut和MappingQ1的头文件。此代码是：

```C++
std::ofstream out("gnuplot.gpl");
out << "plot '-' using 1:2 with lines, "
    << "'-' with labels point pt 2 offset 1,1"
    << std::endl;
GridOut().write_gnuplot (triangulation, out);
out << "e" << std::endl;
const int dim = 2;
std::map<types::global_dof_index, Point<dim> > support_points;
DoFTools::map_dofs_to_support_points (MappingQ1<dim>(),
                                      dof_handler,
                                      support_points);
DoFTools::write_gnuplot_dof_support_point_info(out,
                                               support_points);
out << "e" << std::endl;
```

为了查看.gpl文件，需要在命令行输入

```
gnuplot -p gnuplot.gpl
```

