.. _label_scene_graph:

场景图
====================

场景图
~~~~~~~~~~~~~~~~~~~~

**Glass Engine** 是按照 **场景图** 的理念对场景进行组织的。当我们需要构建复杂场景时，利用场景图的方式更容易描述场景中对象的位置姿态等变换。例如，想象一下，我们要创建这样一个场景：地面上坐落一个房子，房子里放着一张桌子，一把椅子，桌子上放着一个杯子，一个茶壶。很显然，从生活逻辑上讲，这个场景遵循图 1 所示的层次关系：

.. figure:: images/scene_graph.png
   :alt: 场景图
   :align: center
   :scale: 30%

   图 1. 房子、桌椅、杯子、茶壶所构成的场景图

从另一方面讲，当我们描述房子位置的时候，以世界坐标描述比较方便；当我们描述桌子位置的时候，是不是以房子为参考系描述比较方便？当我们描述杯子位置的时候，是不是以桌子为参考系描述比较方便？因此，以树状结构组织场景，能够更符合直觉的体现对象之间的从属关系，并且更加便于描述场景中对象的空间变换。再抽象一层，在上图所示的场景树状结构中，一个节点实际上是代表了一个局部坐标系，它的子节点的空间变换描述是相对于该父节点所代表的的局部坐标系的。按照局部坐标系的理念，则不难理解，如果父节点移动，其所有子节点会跟着移动，但会保持相对父节点的相对坐标不变，这也是将场景组织成树状结构的优势所在。

既然将场景组织成树状结构，为什么不叫场景树而叫场景图呢？是因为，在 **Glass Engine** 的设计中，一个场景节点可以有多个父节点，如图 2 所示。该图表示，桌子上和椅子上放了两个一模一样的茶壶。

.. figure:: images/scene_graph2.png
   :alt: 场景图2
   :align: center
   :scale: 30%

   图 2. 多父节点的场景图

当我们需要在不同位置绘制同一个物体时，推荐使用将该物体挂载到多个父节点上的方式。因为采取这种方式时，在 **Glass Engine** 内部处理时，既可以避免重复的相同物体顶点创建过程，还采用了 **实例化** 渲染方式，将物体在不同位置的绘制合并为一次渲染调用，加快了渲染速度。因此，在这种情况下，场景的组织方式是图而不是树了。更确切的说，这种组织方式是有向无环图。因此，称这种组织方式为 **场景图**。

在 **Glass Engine** 中，首先由 ``scene = Scene()`` 创建出一个场景，一个场景对应唯一一个场景图，一个场景图含有唯一一个根节点，可通过 ``scene.root`` 访问到。往场景中添加对象都应该直接或间接的挂载到根节点上。挂载节点的方式为：

.. highlight:: python3

::

	node = SceneNode()
	scene.root.add_child(node)

上述代码利用 ``SceneNode`` 创建了一个抽象场景节点 ``node``，并将该节点挂载到场景的根节点上。由于往根节点上挂载节点的操作会比较频繁，**Glass Engine** 将该操作进行了一个简化，使得上述代码与下面的代码等价：

::

	node = SceneNode()
	scene.add(node)

注意，这种简化写法只能用于往场景根节点上挂载节点。这里的抽象节点 ``node`` 并不是一个可绘制对象，仅仅代表一个局部坐标系（如果不好理解的话，你可以暂时理解为一个空间位置）。我们可以设置 ``node`` 的空间变换：

::

	node.position.x = -1
	node.yaw = 30 # 偏航角 30 度

随后 ``node`` 下直接和间接挂载的所有子节点将与该节点一起做了这个空间变换，但会保持与该节点的相对位置不变。

下面我们来看一个例子：

::

	from glass_engine import *
	from glass_engine.Geometries import *

	scene, camera, dir_light, floor = SceneRoam() # 创建基础场景

	node1 = SceneNode() # 创建一个场景节点
	node1.position.x = -1 # 设置节点位置的 x 坐标为 -1
	scene.add(node1) # 将其挂载到场景根节点上

	node2 = SceneNode() # 创建另一个场景节点
	node2.position.x = 1 # 设置节点位置的 x 坐标为 1
	scene.add(node2) # 将其挂载到场景根节点上

	cone = Cone(radius=0.5) # 创建一个圆锥模型
	cone.position.x = -0.5 # 设置圆锥位置的 x 坐标为 -0.5
	node1.add_child(cone) # 将圆锥挂载到 node1 上
	node2.add_child(cone) # 同时，将圆锥挂载到 node2 上

	cylinder = Cylinder(radius=0.5) # 创建一个圆柱模型
	cylinder.position.x = 1 # 设置圆柱位置的 x 坐标为 1
	node2.add_child(cylinder) # 将圆柱挂载到 node2 上

	camera.screen.show()

这段代码将产生如图 3 所示的结果：

.. figure:: images/cone_cylinder.png
   :alt: 圆锥圆柱
   :align: center
   :scale: 40%

   图 3. 圆锥圆柱所构成的场景

上述代码创建了一个如图 4 所示的场景图：

.. figure:: images/scene_graph3.png
   :alt: 圆锥圆柱场景图
   :align: center
   :scale: 30%

   图 4. 圆锥圆柱所构成的场景图

``cone`` 节点同时挂载到了两个节点 ``node1`` 和 ``node2`` 下，因此圆锥出现在了两个不同的位置。而我们设置 ``cylinder`` 节点的位置 x 坐标为 1，实则为相对 ``node2`` 的相对坐标，因此其不会和 ``node2`` 下的圆锥重合。这个例子是对场景图概念的一个很好的示意。

场景节点
~~~~~~~~~~~~~~~~~~~~

在上面的例子中，``Camera``、``DirLight``、``Floor``、``Sphere``、``Cone``、``Cylinder``、``SceneNode`` 均能作为场景节点并组织成场景图，原因是这些类均继承自 ``SceneNode``。以 ``SceneNode`` 为根类的所有类的继承关系如图 5 所示：

.. figure:: images/scenenode_class_graph.png
   :alt: 场景节点类图
   :scale: 30%
   :align: center

   图 5. 场景节点继承关系图

其中：

- ``SceneNode`` 为 **场景节点**，是所有场景节点类的基类。可将其想象为一个局部坐标系，可用 ``position, yaw, pitch, roll, orientation`` 等属性描述该局部坐标系相对于其父节点的空间变换关系。可用 ``add_child, remove_child`` 添加或删除子节点。
- ``SinglePathNode`` 为 **单路径节点**。单路径指的是从该节点出发向上追溯到根节点的路径是唯一的。**Glass Engine** 通过异常和其他机制保证了这种唯一性，一般情况下你不需要创建它，它只作为相机类的父类存在。
- ``Camera`` 为 :ref:`label_camera`，用于将场景投影为屏幕上显示的视图，其显示屏 ``screen`` 属性即为 3D 视口，可作为一个 GUI 控件（当前仅为 `QWidget`）布局到程序界面的任意位置，也可单独显示。在不设置姿态时，相机视线方向朝向其所在的局部坐标系 y 轴正方向。
- ``Light`` 为 :ref:`label_lights`，用于照亮场景。建议场景中至少添加一个光源，否则整个场景将一片漆黑。请不要用 ``Light`` 类直接创建实例，因为这将起不到任何光源的作用。而应该用其子类创建光源实例。
- ``DirLight`` 为 :ref:`label_DirLight`，范围无限大，能照亮全场。其有一个特定的光线方向，在不设置姿态时朝向其所在的局部坐标系 y 轴正方向。可用姿态属性 ``yaw, pitch, roll, orientaion`` 控制光线方向，而其位置属性 ``position`` 则没有意义。
- ``PointLight`` 为 :ref:`label_PointLight`，光线从一点发散射出，具有一定的照明范围。其发出的光线具有各向同性，所以其姿态属性无意义。
- ``SpotLight`` 为 :ref:`label_SpotLight`，类似于舞台聚光灯。聚光仅射出一个光锥，光锥内表现为点光源，光锥外不被照亮。
- ``Mesh`` 为 **网格**，“网格”这个名字不太直观，事实上就是场景中可见的实体，并且不可再分。之所以起名为网格是因为这是计算机图形学中的通用术语。所有的基本几何体都继承自 ``Mesh``。
- ``Floor`` 为 **地板**，基本几何体之一，可直接作为场景的地面使用。
- ``Sphere, Cone, Cylinder, ...`` 为各种 :ref:`label_geometries`，**Glass Engine** 提供 40 多种基本几何体，详情见 :ref:`label_geometries`，不在此一一介绍。
- ``Model`` 为 :ref:`label_model`，单指从外部模型文件加载上来的模型。可直接通过 ``Model("file_name")`` 的方式直接从文件加载模型。**Glass Engine** 支持 40 多种格式的模型文件加载，详情见 :ref:`label_model`，不在此一一介绍。

一个基类场景节点 ``SceneNode`` 对象是可以被独立创建的，场景节点基类对象仅代表一个局部坐标系，并维持树状结构关系。在上面的描述中，我们经常提到局部坐标系的概念，而所有的空间变换描述都依赖于局部坐标系的定义，在下一节中我们将给出定义并详细讲解空间变换的概念。