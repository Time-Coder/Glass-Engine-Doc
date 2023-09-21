键鼠交互
=================

**Glass Engine** 所创建出的视口的键盘鼠标交互方式由相机屏幕 ``camera.screen`` 的 ``manipulator`` 属性决定。可通过给 ``camera.screen.manipulator`` 设置不同的值来实现不同的鼠标交互方式，该属性其只接受继承自 ``Manipulator`` 类的对象。**glass_engnine** 提供两种内置的 ``Manipulator`` 分别为：

- ``SceneRoamManipulator``: 场景漫游交互模式
- ``ModelViewManipulator``: 模型预览交互模式

这两种交互模式的类都定义在子模块 ``glass_engine.Manipulators`` 中，可直接导入使用。**Glass Engine** 默认的交互模式为 **场景漫游交互模式**，若想切换为 **模型预览交互模式** 则可以使用如下代码：

::

	from glass_engine.Manipulators import *
	camera.screen.manipulator = ModelViewManipulator()

如果你不想要任何的键盘鼠标响应，只想要一个静态场景，只需设置 ``camera.screen.manipulator = None`` 即可。

另外，通过 ``glass_engine`` 中定义的简化函数 ``SceneRoam`` 创建出的基本场景的交互模式为场景漫游交互模式；通过 ``ModelView`` 创建出的基本场景的交互模式为模型预览交互模式。最后，你还可以编写自己的 ``Manipulator`` 来实现自定义鼠标键盘交互模式。

场景漫游模式
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Glass Engine** 默认为场景漫游交互模式，在该模式下，你可以通过 :kbd:`W` :kbd:`A` :kbd:`S` :kbd:`D` :kbd:`E` :kbd:`C` 在场景中进行漫游，并通过鼠标控制视角。具体地，

- :kbd:`A` 相机向左移动，:kbd:`D` 相机向右移动；
- :kbd:`W` 相机向前移动，:kbd:`S` 相机向后移动；
- :kbd:`E` 相机向上移动，:kbd:`C` 相机向下移动；
- 鼠标右键拖拽：改变相机视角；
- 鼠标左键拖拽：在垂直与观察方向的平面内平移相机；
- 鼠标滚轮推动：向前推则放大视口，向后拉则缩小视口
- 鼠标左侧前进键：提高键盘移动速度；
- 鼠标左侧后退键：降低键盘移动速度；
- :kbd:`R`：在实体模式、网格模式、点模式这三种显示模式下切换；
- :kbd:`F`：打印帧率和渲染调用次数；
- :kbd:`P`：截图并保存到当前文件夹；
- :kbd:`Enter`：进入游戏模式；
- :kbd:`Esc`：退出游戏模式。

按下回车键你可以进入游戏模式，在游戏模式中，鼠标光标是隐藏的，左右键拖拽则不再适用，鼠标移动即为改变视角。按下退出键就可以退出游戏模式。

模型浏览模式
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

通过 ``camera.screen.manipulator = ModelViewManipulator()`` 可将交互模式切换为模型预览模式。该模式更加适合查看单个模型，因为随着鼠标的拖动，视角只会围绕模型旋转。具体地，

- :kbd:`A`：相机向左移动，:kbd:`D`：相机向右移动；
- :kbd:`W`：相机靠近物体，:kbd:`S`：相机远离物体；
- :kbd:`E`：相机向上移动，:kbd:`C`：相机向下移动；
- 鼠标左键拖拽：相机围绕物体旋转；
- 鼠标右键拖拽：在垂直与观察方向的平面内平移相机；
- 鼠标滚轮推动：向前推则放大视口，向后拉则缩小视口；
- 鼠标左侧前进键：提高围绕物体旋转灵敏度；
- 鼠标左侧后退键：降低围绕物体旋转灵敏度；
- :kbd:`R`：在实体模式、网格模式、点模式这三种显示模式下切换；
- :kbd:`F`：打印帧率；
- :kbd:`P`：截图并保存到当前文件夹。

``ModelViewManipulator`` 类在创建的时候还接受 ``distance, azimuth, elevation`` 三个参数，同时它还具有同名的三个属性。它们分别表示：

- ``distance``: 相机距离世界坐标 (0, 0, 0) 的距离；
- ``azimuth``: 相机位置的方位角，单位为度；
- ``elevation``: 相机位置的仰角，单位为度。

如图 1 所示，图中所示的坐标系恒为场景根节点坐标系。

.. figure:: images/azimuth_elevation_distance.png
    :align: center
    :scale: 30%

    图 1. distance, azimuth, elevation 的含义

自定义交互模式
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

你还可以创建自定义鼠标键盘交互模式，只需编写一个类继承自 ``Manipulator`` 并选择性的编写以下方法来实现鼠标键盘响应时所要执行的操作后，将该类创建的对象赋值给 ``camera.screen`` 的 ``manipulator`` 属性即可。

::

    from glass_engine.Manipulators import Manipulator

    class MyManipulator(Manipulator):

        def __init__(self):
            Manipulator.__init__(self)

        def startup(self)->bool:
        # 刚执行 camera.screen.manipulator = MyManipulator() 时要执行的操作

            return False

        def on_mouse_pressed(self, button:Manipulator.MouseButton, screen_pos:glm.vec2, global_pos:glm.vec2)->bool:
        # 鼠标按钮按下时要执行的操作
        # button: 鼠标按钮的枚举值
        # screen_pos: 鼠标按下的屏幕位置，当前视口左上角为 (0, 0)，右下为正方向，单位为像素
        # global_pos: 鼠标按下的全局位置，电脑显示器左上角为 (0, 0)，右下为正方向，单位为像素
        
            return False

        def on_mouse_released(self, button:Manipulator.MouseButton, screen_pos:glm.vec2, global_pos:glm.vec2)->bool:
        # 鼠标按钮松开时要执行的操作
        # button: 鼠标按钮的枚举值
        # screen_pos: 鼠标松开的屏幕位置，当前视口左上角为 (0, 0)，右下为正方向，单位为像素
        # global_pos: 鼠标松开的全局位置，电脑显示器左上角为 (0, 0)，右下为正方向，单位为像素

            return False
        
        def on_mouse_double_clicked(self, button:Manipulator.MouseButton, screen_pos:glm.vec2, global_pos:glm.vec2)->bool:
        # 鼠标按钮双击时要执行的操作
        # button: 鼠标按钮的枚举值
        # screen_pos: 鼠标双击的屏幕位置，当前视口左上角为 (0, 0)，右下为正方向，单位为像素
        # global_pos: 鼠标双击的全局位置，电脑显示器左上角为 (0, 0)，右下为正方向，单位为像素

            return False

        def on_mouse_moved(self, screen_pos:glm.vec2, global_pos:glm.vec2)->bool:
        # 鼠标移动时要执行的操作
        # screen_pos: 鼠标当前的屏幕位置，当前视口左上角为 (0, 0)，右下为正方向，单位为像素
        # global_pos: 鼠标当前的全局位置，电脑显示器左上角为 (0, 0)，右下为正方向，单位为像素

            return False

        def on_wheel_scrolled(self, angle:glm.vec2, screen_pos:glm.vec2, global_pos:glm.vec2)->bool:
        # 鼠标滚轮滚动时要执行的操作
        # angle: 鼠标滚轮滚动的角度，angle.y 为常规滚轮滚动的角度，angle.x 为横向滚轮滚动的角度
        # screen_pos: 鼠标滚轮滚动时的屏幕位置，当前视口左上角为 (0, 0)，右下为正方向，单位为像素
        # global_pos: 鼠标滚轮滚动时的全局位置，电脑显示器左上角为 (0, 0)，右下为正方向，单位为像素

            return False

        def on_key_pressed(self, key:Manipulator.Key)->bool:
        # 键盘按键按下时要执行的操作
        # key: 按下的按键枚举值

            return False

        def on_key_released(self, key:Manipulator.Key)->bool:
        # 键盘按键松开时要执行的操作
        # key: 松开的按键枚举值

            return False

        def on_key_repeated(self, keys:set[Manipulator.Key])->bool:
        # 键盘按键一直按着时要执行的操作
        # keys: 当前所有按着的按键集合

            return False

在每个方法编写时，你可以访问到 ``self.camera`` 属性，表示当前操作的相机，可通过 ``self.camera`` 的 ``position, orientation, yaw, pitch, roll`` 等属性直接更改相机的空间变换。如果你想更改场景内容的话，可以通过 ``self.camera.scene`` 获取到该相机所在的场景并进行更改。

你会注意到，每个方法都需要返回一个 ``bool`` 值，返回 ``True`` 意味着需要更新视口，否则不更新，不更新意味着即使你改变了相机位置，显示内容也不会发生改变。所以记得在适当的时候 ``return True``。

如果你觉得继承自 ``Manipulator`` 工作量太大，你只是想更改默认的操作器的一些行为，则可以直接继承自 ``SceneRoamManipulator`` 或 ``ModelViewManipulator`` 并重载里面对应的方法。

Qt 系统的额外功能
>>>>>>>>>>>>>>>>>>>>>>>>>>>

如果你使用的是 PyQt 或 PySide 界面系统（当前仅支持 PyQt），还可以在不编写 Manipulator 子类的情况下直接编写一些简单的鼠标键盘响应。每当有键盘鼠标事件发生时，``camera.screen`` 都会有相应的信号发出，这些信号包括：

- ``mouse_pressed(button:Manipulator.MouseButton, screen_pos:glm.vec2, global_pos:glm.vec2)``: 鼠标按钮按下信号
- ``mouse_released(button:Manipulator.MouseButton, screen_pos:glm.vec2, global_pos:glm.vec2)``: 鼠标按钮松开信号
- ``mouse_double_clicked(button:Manipulator.MouseButton, screen_pos:glm.vec2, global_pos:glm.vec2)``: 鼠标双击信号
- ``mouse_moved(screen_pos:glm.vec2, global_pos:glm.vec2)``: 鼠标移动信号
- ``wheel_scrolled(angle:glm.vec2, screen_pos:glm.vec2, global_pos:glm.vec2)``: 滚轮滚动信号
- ``key_pressed(key:Manipulator.Key)``: 键盘按键按下信号
- ``key_released(key:Manipulator.Key)``: 键盘按键松开信号
- ``key_repeated(keys:set[Manipulator.Key])``: 键盘按键一直按着的信号
- ``frame_started()``: 每一帧开始时的信号
- ``frame_ended()``: 每一帧结束时的信号

将它们连接到你要执行操作的槽函数即可。如果想要屏蔽掉默认的响应，只需设置 ``camera.screen.manipulator = None`` 即可。