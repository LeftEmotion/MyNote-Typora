UML全称为unified modeling language

- 构造块 基本UML建模元素、关系和图
- 公共机制 达到特定目标的公共UML方法
- 构架 系统架构的UML视图



构造块 building blocks

- 物件 things 建模元素本身
- 关系 relationships 把物件联系在一起，关系说明两个或多个物件时是如何语义相关的
- 图 diagrams 展现物体的集合



物件 things

- 结构物件 UML模型中的名词，如类，接口
- 行为物件 UML模型的动词，如交互，状态机
- 分组物件 用于把语义上相关的建模元素分组为内聚的单元
- 注解物件 附加到模型上以捕获特殊信息



公共机制 

- 规格说明 specifications
- 修饰 adornments
- 公共分类 common divisions
- 扩展机制 extensibility mechanisms





九种图 = 静态模型（系统结构）+ 动态模型（系统行为）

​	（静态模型）

- **类图** class 类以及类之间的相互关系

- 对象图 object 对象以及对象之间相互关系（类的具体实现）

- 构件图 component 构件以及相互依赖关系

- 部署图 deployment 构件在各节点上的部署

  

  （动态模型）

- **顺序图** sequence 强调时间顺序的交互图

- 通信图（协作图） collaboration 强调对象协作的交互图

- 状态图 statechart 类所经历的各种状态

- **活动图** activity 对工作流建模

- **用例图** use case 需求捕获，测试依据

  **顺序图和通信图可以相互转换**

类的属性

- 公有public + 所有可见

- 受限protected # 子类以及本身可见

- 私有private - 本身可见

- 包package ~ 包内可见




四种关系 relationships

- 关联 association 描述对象之间的一组链接
- 依赖 dependency 物件的改变引起依赖物件的语义改变
- 泛化 generalization 一个元素是另一个元素的特化，而且它可以取代更一般的元素（继承：孩子与双亲是泛化关系）
- 实现 realization 类元之间的关系

关联

- 连接 最弱的关联，表示两个类对象之间有导航关系

- 聚合 has a，对象A是对象B的一个组成部分

- 组合 强语义的聚合，部分跟着整体对象消失

  

UML structure

- 构造块 building blocks
- 公告机制 common mechanisms
- 构架 architecture



 构架 Architecture（4+1视图）

- 用例视图 use case view 描述项目干系人的需求
- 逻辑视图 logical view 展示对象和类是如何组合成系统、实现所需系统行为的
- 进程视图 process view 系统性能、可伸缩量和吞吐量；将系统中的可执行线程和进程作为活动类来建模
- 实现视图 implementation view 
- 部署视图 deployment view 



类的类型 the class type

- 实体类  entity class 表示客观实体，像学生，图书等
- 界面类 Boundary class 描述系统与外界之间交互的系统要素，并不表示交互的具体内容以及具体形式
- 控制类 control class 表示系统用来进行各种业务处理的系统要素，诸如登陆处理，会员管理器，售书处理



场景是用来描述用户和系统之间交互顺序的步骤

用例是为了达到某一用户目标而组合在一起的一组场景



- 用例图：用来显示在系统内的用例与系统参与者之间的关系
  - p

