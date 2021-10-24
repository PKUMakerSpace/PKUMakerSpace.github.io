# Unity X课程 第一次课



## 第一次课程大纲

Unity的界面结构

Unity的游戏元素

Unity的游戏逻辑

场景布置

基本游戏功能（碰撞，运动控制，玩家输入等）

基本资源功能



## Unity的界面结构

Scene面板

Hierarchy面板

Game面板

Project面板

Inspector面板

Console面板



## Unity的游戏元素

Unity的一个工程（Project）的游戏元素大致可以分为Asset、GameObject、Compoent三大类

### Asset

Asset是一个Project的静态元素，它们存储了所有游戏需要的资源，以文件的形式保存在你的磁盘里，如果做一个比喻，将游戏作为一个车辆，则Asset就是车辆的图纸

Asset有很多种类型，重要的包括包括：

Scene

Prefab

Mesh

Material

Script

### GameObject

GameObject是一个Scene内部的动态元素，它们被布置在一个Scene中，组成了整个游戏场景，Unity拥有一系列预设的GameObject，包括：

Cube

Sphere

Empty

Canvas

UI element

Particle System

Light

Camera

### Component

Component依附于GameObject，它为GameObject提供修饰，最基本的Component是transform，它规定了该GameObject的位置，所有GameObject都有transform组件

如果一个GameObject只有transform组件，那它和Empty没有区别，它只有一个位置，但是它不会渲染出任何东西，也不能和其他游戏物体相互作用（除非其他物体的脚本操纵了它）

常用的Component包括：

Script

Collider

Renderer

Rigidbody

Animator



## Unity的游戏逻辑

一个Project由一系列Scene组成，一般来说，一个Scene作为一个整体被打开和关闭，当开始一个游戏时，Unity会打开该游戏的默认Scene，之后开始整个游戏的游戏循环

Unity中每一个物体都会有其独立的游戏循环，通过其Script中继承Monobehavior类进行操纵，包括如下逻辑：

Start：该物体被创建

Update：每一次循环（渲染）进行一次

FixedUpdate：每固定时间进行一次

一个物体被创建时，会执行其Start以初始化，之后，每经过一定时长，会对该物体进行渲染（render），并执行其逻辑（Update，FixedUpdate），如果该物体有多个Component，那么每个Component都会执行其Start，Update等逻辑



## 场景布置

### 物体布置

在Hierarchy面板和Scene面板中可以对场景进行布置，通过拖拽的方法可以简单地进行控制

Unity的场景是树状结构，除了直接在场景之下的根物体，每一个物体都有一个父物体

在布置场景时，最重要的Component是transform，它可以通过Script（运行时）或者手动设置（编辑时）进行设置

在Inspector面板上，可以看到一个物体的transform，transform上的值显示了其相对于父物体的位置偏移、角度偏移、缩放偏移。transform的值本质上是相对值，也就是说，如果在Inspector上，改变子物体的transform，那么是改变了其相对于父亲的transform的位置，角度，缩放，而如果改变了父亲的transform，那么孩子会保持和父亲的相对关系，因此，如果父亲发生了位置，角度，缩放的改变，则孩子也会跟着改变

在使用脚本时，情况会相对复杂一些，transform组件支持相对于父亲进行改变，但是它也可以通过指定绝对世界坐标来确定位置。但是，不管使用绝对坐标还是相对坐标，本质上，transform都是相对于父亲的，使用世界坐标时，只是通过计算将其转化为对应的相对坐标而已

创建物体不仅仅可以在编辑时手动完成，也可以在运行时完成，使用GameObject.Instantiate可以在运行时动态地创建一个游戏物体

### Camera布置

之前的物体布置只是我们在浏览Scene的呈现，但实际上，我们需要一个Camera才能真正在游戏运行时看到这些物体

Camera有两种模式，平视模式和透视模式，后者是默认，会形成点状的透视视角，具有立体感，而前者并没有透视效果，常用于2D场景



## 基本游戏功能

### 碰撞

物体之间的碰撞由Collider组件实现，Collider可以指定物体的形状，并自动地管理碰撞行为，需要注意的是，Collider给出的是碰撞的形状，而非物体渲染的形状，二者可以是不同的，比如，一个物体可能长得像一个巨型的球体，但实际上碰撞体积只是一个微小的立方体，甚至没有碰撞体积

Collider的IsTrigger属性可以指定该物体为Trigger，如果是一个Trigger，那它不会和其他物体发生碰撞，但是，它可以检测到其他物体的进入，并触发相应的Script的响应函数

可以通过物体的layer以及Physics面板来决定哪些物体之间会发生碰撞

### 运动控制

有三种方式可以进行运动控制：无RigidBody或kinematic rigidbody，运动学RigidBody，动力学RigidBody

在无RigidBody或kinematic rigidbody的情况下，物体的位置完全由脚本控制，物体不存在所谓速度、质量等属性，都需要通过脚本来模拟

在运动学RigidBody的情况下，物体由其RigidBody上的速度属性控制，通过速度来控制物体

在动力学RigidBody的情况下，物体不仅仅有速度，还有质量以及受力，在这种情况下，可以通过给物体施加力的方式改变物体的运动，而物体也会在与其他物体的相互作用中（比如碰撞）受力

### 玩家输入

玩家输入需要写脚本，大多数的输入由Input静态类获取

### 渲染

renderer组件负责进行物体的渲染，它主要需要指定形状和材质：

形状：可以是预设形状，也可以是自己建模产生的形状，决定了物体呈现的形状

材质：物体的材质可以通过Shader或者Material来指定，决定了物体呈现的光学特性，如透明度，金属度，颜色，贴图，光滑度

### 其他功能

Tag：可以有许多的Tag，它们适合于给物体分类

Disable：禁用物体的所有功能

不显示：不渲染一个物体，以达到隐藏的目的

Documentation按钮：方便学习不懂的东西



## 基本资源功能

Unity的资源管理就是一个文件系统，因此，可以像你操作Windows或Mac的文件和文件夹一样方便地操作

### 常见预设资源

可以直接在Project面板中添加Scene，Material，Animator，Script等预设资源

### Prefab

GameObject只是Scene中的一个物体，但是，它依附于Scene，不是一个独立的资源。但是，我们依旧可以将这个物体的图纸放在Asset中，方便对其的创建和修改，这就是Prefab

Prefab很好创建，可以直接将Scene中（通过Hierarchy界面）的物体拖拽到Projec面板中，就会创建该物体的Prefab

之后，可以以该Prefab为模板创建任意多的物体，一旦改变了Prefab，这些物体也会跟着改变

由Prefab创建的GameObject可以有相对于Prefab不同的Component的属性，可以有多余的Component，可以有新的子物体，但是不可以删除其包含的子物体（但是可以Disable）

### 外部资源

只要是Unity可以识别的外部资源，就可以直接将文件拖拽到Project面板中，比如：3D模型，不同格式的文件，视频等

注意，不要在Unity之外直接通过文件系统进行拖拽，因为这样不会创建元文件

### Unity Asset Store

可以在这里发布自己创建的Asset，或者下载别人，包括官方发布的Asset包，其中有不少是免费的，而且质量还不错，不过凑齐一套画风一样的也不太容易



## Demo

这是第一次课的教学工程

Github repository：

[PKUMakerSpace/UnityCourse1 (github.com)](https://github.com/PKUMakerSpace/UnityCourse1)

