# Chap8. OCP: THE OPEN-CLOSED PRINCIPLE OCP：开闭原则

![](./un/CH-UN08.jpg)

The Open-Closed Principle (OCP) was coined in 1988 by Bertrand Meyer.[<sup>1</sup>](#footnote-1) It says:

> 开闭原则（OCP）是 Bertrand Meyer 在 1988 年提出的，该设计原则认为：

A software artifact should be open for extension but closed for modification.

> 设计良好的计算机软件应该易于扩展，同时抗拒修改。

In other words, the behavior of a software artifact ought to be extendible, without having to modify that artifact.

> 换句话说，一个设计良好的计算机系统应该在不需要修改的前提下就可以轻易被扩展。

This, of course, is the most fundamental reason that we study software architecture. Clearly, if simple extensions to the requirements force massive changes to the software, then the architects of that software system have engaged in a spectacular failure.

> 其实这也是我们研究软件架构的根本目的。如果对原始需求的小小延伸就需要对原有的软件系统进行大幅修改，那么这个系统的架构设计显然是失败的。

Most students of software design recognize the OCP as a principle that guides them in the design of classes and modules. But the principle takes on even greater significance when we consider the level of architectural components.

> 尽管大部分软件设计师都已经认可了 OCP 是设计类与模块时的重要原则，但是在软件架构层面，这项原则的意义则更为重大。

A thought experiment will make this clear.

> 下面，让我们用一个思想实验来做一些说明。

## A THOUGHT EXPERIMENT 思想实验

Imagine, for a moment, that we have a system that displays a financial summary on a web page. The data on the page is scrollable, and negative numbers are rendered in red.

> 假设我们现在要设计一个在 Web 页面上展示财务数据的系统，页面上的数据要可以滚动显示，其中负值应显示为红色。

Now imagine that the stakeholders ask that this same information be turned into a report to be printed on a black-and-white printer. The report should be properly paginated, with appropriate page headers, page footers, and column labels. Negative numbers should be surrounded by parentheses.

> 接下来，该系统的所有者又要求同样的数据需要形成一个报表，该报表要能用黑白打印机打印，并且其报表格式要得到合理分页，每页都要包含页头、页尾及栏目名。同时，负值应该以括号表示。

Clearly, some new code must be written. But how much old code will have to change?

> 显然，我们需要增加一些代码来完成这个要求。但在这里我们更关注的问题是，满足新的要求需要更改多少旧代码。

A good software architecture would reduce the amount of changed code to the barest minimum. Ideally, zero.

> 一个好的软件架构设计师会努力将旧代码的修改需求量降至最小，甚至为 0。

How? By properly separating the things that change for different reasons (the Single Responsibility Principle), and then organizing the dependencies between those things properly (the Dependency Inversion Principle).

> 但该如何实现这一点呢？我们可以先将满足不同需求的代码分组（即 SRP），然后再来调整这些分组之间的依赖关系（即 DIP）。

By applying the SRP, we might come up with the data-flow view shown in Figure 8.1. Some analysis procedure inspects the financial data and produces reportable data, which is then formatted appropriately by the two reporter processes.

> 利用 SRP，我们可以按图 8.1 中所展示的方式来处理数据流。即先用一段分析程序处理原始的财务数据，以形成报表的数据结构，最后再用两个不同的报表生成器来产生报表。

<Figures figure="8-1">Applying the SRP</Figures>

The essential insight here is that generating the report involves two separate responsibilities: the calculation of the reported data, and the presentation of that data into a web- and printer-friendly form.

> 这里的核心就是将应用生成报表的过程拆成两个不同的操作。即先计算出报表数据，再生成具体的展示报表（分别以网页及纸质的形式展示）。

Having made this separation, we need to organize the _source code_ dependencies to ensure that changes to one of those responsibilities do not cause changes in the other. Also, the new organization should ensure that the behavior can be extended without undo modification.

> 接下来，我们就该修改其 _源代码_ 之间的依赖关系了。这样做的目的是保证其中一个操作被修改之后不会影响到另外一个操作。同时，我们所构建的新的组织形式应该保证该程序后续在行为上的扩展都无须修改现有代码。

We accomplish this by partitioning the processes into classes, and separating those classes into components, as shown by the double lines in the diagram in Figure 8.2. In this figure, the component at the upper left is the _Controller_. At the upper right, we have the _Interactor_. At the lower right, there is the _Database_. Finally, at the lower left, there are four components that represent the _Presenters_ and the _Views_.

> 在具体实现上，我们会将整个程序进程划分成一系列的类，然后再将这些类分割成不同的组件。下面，我们用图 8.2 中的那些双线框来具体描述一下整个实现。在这个图中，左上角的组件是 _Controller_，右上角是 _Interactor_，右下角是 _Database_，左下角则有四个组件分别用于代表不同的 _Presenter_ 和 _View_。

<Figures figure="8-2">Partitioning the processes into classes and separating the classes into components</Figures>

Classes marked with `<I>` are interfaces; those marked with `<DS>` are data structures. Open arrowheads are _using_ relationships. Closed arrowheads are _implements_ or _inheritance_ relationships.

> 在图 8.2 中，用 `<I>` 标记的类代表接口，用 `<DS>` 标记的则代表数据结构；开放箭头指代的是 _使用_ 关系，闭合箭头则指代了 _实现_ 与 _继承_ 关系。

The first thing to notice is that all the dependencies are source code dependencies. An arrow pointing from class A to class B means that the source code of class A mentions the name of class B, but class B mentions nothing about class A. Thus, in Figure 8.2, `FinancialDataMapper` knows about `FinancialDataGateway` through an implements relationship, but `FinancialDataGateway` knows nothing at all about `FinancialDataMapper`.

> 首先，我们在图 8.2 中看到的所有依赖关系都是其源代码中存在的依赖关系。这里，从类 A 指向类 B 的箭头意味着 A 的源代码中涉及了 B，但是 B 的源代码中并不涉及 A。因此在图 8.2 中，`FinancialDataMapper` 在实现接口时需要知道 `FinancialDataGateway` 的实现，而 `FinancialDataGateway` 则完全不必知道 `FinancialDataMapper` 的实现。

The next thing to notice is that each double line is crossed _in one direction only_. This means that all component relationships are unidirectional, as shown in the component graph in Figure 8.3. These arrows point toward the components that we want to protect from change.

> 其次，这里很重要的一点是这些双线框的边界都是 _单向_ 跨越的。也就是说，上图中所有组件之间的关系都是单向依赖的，如图 8.3 所示，图中的箭头都指向那些我们不想经常更改的组件。

<Figures figure="8-3">The component relationships are unidirectional</Figures>

Let me say that again: If component A should be protected from changes in component B, then component B should depend on component A.

> 让我们再来复述一下这里的设计原则：如果 A 组件不想被 B 组件上发生的修改所影响，那么就应该让 B 组件依赖于 A 组件。

We want to protect the _Controller_ from changes in the _Presenters_. We want to protect the _Presenters_ from changes in the _Views_. We want to protect the _Interactor_ from changes in—well, _anything_.

> 所以现在的情况是，我们不想让发生在 _Presenter_ 上的修改影响到 _Controller_，也不想让发生在 _View_ 上的修改影响到 _Presenter_。而最关键的是，我们不想让 _任何_ 修改影响到 _Interactor_。

The _Interactor_ is in the position that best conforms to the OCP. Changes to the _Database_, or the _Controller_, or the _Presenters_, or the _Views_, will have no impact on the _Interactor_.

> 其中，_Interactor_ 组件是整个系统中最符合 OCP 的。发生在 _Database_、_Controller_、_Presenter_ 甚至 _View_ 上的修改都不会影响到 _Interactor_。

Why should the _Interactor_ hold such a privileged position? Because it contains the business rules. The _Interactor_ contains the highest-level policies of the application. All the other components are dealing with peripheral concerns. The _Interactor_ deals with the central concern.

> 为什么 _Interactor_ 会被放在这么重要的位置上呢？因为它是该程序的业务逻辑所在之处，_Interactor_ 中包含了其最高层次的应用策略。其他组件都只是负责处理周边的辅助逻辑，只有 _Interactor_ 才是核心组件。

Even though the _Controller_ is peripheral to the _Interactor_, it is nevertheless central to the _Presenters_ and _Views_. And while the _Presenters_ might be peripheral to the _Controller_, they are central to the _Views_.

> 虽然 _Controller_ 组件只是 _Interactor_ 的附属品，但它却是 _Presenter_ 和 _View_ 所服务的核心。同样的，虽然 _Presenter_ 组件是 _Controller_ 的附属品，但它却是 _View_ 所服务的核心。

Notice how this creates a hierarchy of protection based on the notion of “level.” _Interactors_ are the highest-level concept, so they are the most protected. _Views_ are among the lowest-level concepts, so they are the least protected. _Presenters_ are higher level than _Views_, but lower level than the _Controller_ or the _Interactor_.

> 另外需要注意的是，这里利用“层级”这个概念创造了一系列不同的保护层级。譬如，_Interactor_ 是最高层的抽象，所以它被保护得最严密，而 _Presenter_ 比 _View_ 时层级高，但比 _Controller_ 和 _Interactor_ 的层级低。

This is how the OCP works at the architectural level. Architects separate functionality based on how, why, and when it changes, and then organize that separated functionality into a hierarchy of components. Higher-level components in that hierarchy are protected from the changes made to lower-level components.

> 以上就是我们在软件架构层次上对 OCP 这一设计原则的应用。软件架构师可以根据相关函数被修改的原因、修改的方式及修改的时间来对其进行分组隔离，并将这些互相隔离的函数分组整理成组件结构，使得高阶组件不会因低阶组件被修改而受到影响。

## DIRECTIONAL CONTROL 依赖方向的控制

If you recoiled in horror from the class design shown earlier, look again. Much of the complexity in that diagram was intended to make sure that the dependencies between the components pointed in the correct direction.

> 如果刚刚的类设计把你吓着了，别害怕！你刚刚在图表中所看到的复杂度是我们想要对组件之间的依赖方向进行控制而产生的。

For example, the `FinancialDataGateway` interface between the `FinancialReportGenerator` and the `FinancialDataMapper` exists to invert the dependency that would otherwise have pointed from the _Interactor_ component to the _Database_ component. The same is true of the `FinancialReportPresenter` interface, and the two _View_ interfaces.

> 例如，`FinanciaIReportGenerator` 和 `FinancialDataMapper` 之间的 `FinancialDataGateway` 接口是为了反转 _Interactor_ 与 _Database_ 之间的依赖关系而产生的。同样的，`FinancialReportPresenter` 接口与两个 _View_ 接口之间也类似于这种情况。

## INFORMATION HIDING 信息隐藏

The `FinancialReportRequester` interface serves a different purpose. It is there to protect the `FinancialReportController` from knowing too much about the internals of the _Interactor_. If that interface were not there, then the _Controller_ would have transitive dependencies on the `FinancialEntities`.

> 当然，`FinancialReportRequester` 接口的作用则完全不同，它的作用是保护 `FinancialReportController` 不过度依赖于 _Interactor_ 的内部细节。如果没有这个接口，则 _Controller_ 将会传递性地依赖于 `FinancialEntities`。

Transitive dependencies are a violation of the general principle that software entities should not depend on things they don’t directly use. We’ll encounter that principle again when we talk about the Interface Segregation Principle and the Common Reuse Principle.

> 这种传递性依赖违反了“软件系统不应该依赖其不直接使用的组件”这一基本原则。之后，我们会在讨论接口隔离原则和共同复用原则的时候再次提到这一点。

So, even though our first priority is to protect the _Interactor_ from changes to the _Controller_, we also want to protect the _Controller_ from changes to the _Interactor_ by hiding the internals of the _Interactor_.

> 所以，虽然我们的首要目的是为了让 _Interactor_ 屏蔽掉发生在 _Controller_ 上的修改，但也需要通过隐藏 _Interactor_ 内部细节的方法来让其屏蔽掉来自 _Controller_ 的依赖。

## CONCLUSION 本章小结
The OCP is one of the driving forces behind the architecture of systems. The goal is to make the system easy to extend without incurring a high impact of change. This goal is accomplished by partitioning the system into components, and arranging those components into a dependency hierarchy that protects higher-level components from changes in lower-level components.

> OCP 是我们进行系统架构设计的主导原则，其主要目标是让系统易于扩展，同时限制其每次被修改所影响的范围。实现方式是通过将系统划分为一系列组件，并且将这些组件间的依赖关系按层次结构进行组织，使得高阶组件不会因低阶组件被修改而受到影响。

<a name="footnote-1">&nbsp;</a>

<br />

---

#### <sup>1</sup> Bertrand Meyer. _Object Oriented Software Construction_, Prentice Hall, 1988, p23.
