动画
==========================

目前 **Glass Engine** 暂不支持骨骼动画，现有的动画有两种形式：变化的各种参数和 Shadertoy 纹理。其中变化的参数可通过 ``QTimer`` 推动，并在回调函数中改变任意参数；Shadertoy 纹理可以通过编写 `Shadertoy <https://shadertoy.com/>`_ 格式的 Shader 将任意纹理设置为动态效果。

变化的参数
~~~~~~~~~~~~~~~~~~~~

你可以在 ``QTimer`` 的回调函数中改变前面章节介绍过的任何参数，以此来达到动画的效果。例如我们可以改变 :ref:`label_transform` 参数来实现地球自转，月球绕地球旋转的动画效果（从 `这里 <https://www.solarsystemscope.com/textures/>`_ 下载地球，月球，星空的纹理图片）：

::

	from glass_engine import *
	from glass_engine.Geometries import *

	from PyQt6.QtCore import QTimer

	scene, camera, _, _ = SceneRoam(add_floor=False)
	scene.skydome = "stars_milky_way.jpg"

	earth = Sphere()
	earth.material.diffuse_map = "earth.jpg"
	scene.add(earth)

	moon = Sphere(radius=0.3)
	moon.position.x = 3
	moon.material.diffuse_map = "moon.jpg"

	moon_node = SceneNode()
	moon_node.add_child(moon)

	scene.add(moon_node)

	def timer_event():
	    earth.yaw += 3
	    moon_node.yaw += 1
	    camera.screen.update()

	timer = QTimer()
	timer.timeout.connect(timer_event)
	timer.start(20)

	camera.screen.show()

则能得到如图 1 所示的效果：

.. figure:: images/earth.gif
   :align: center
   :scale: 50%

   图 1. 地月系动画效果

.. _label_shadertory:

Shadertoy 动态纹理
~~~~~~~~~~~~~~~~~~~~

在 **Glass Engine** 中，所有纹理除了可以设置为静态图片，还可设置为 `Shadertoy <https://shadertoy.com/>`_ 格式的动态纹理。该类型纹理可从 `Shadertoy <https://shadertoy.com/>`_ 网站直接下载代码，方法为：

1. 打开 `Shadertoy <https://shadertoy.com/>`_ 网站，找到你喜欢的动态 Shader，打开并复制右侧红框中的代码，如图 2 所示：

.. figure:: images/shadertoy.png
   :align: center
   :scale: 40%

   图 2. 打开 Shadertoy 复制代码
   
2. 将代码粘贴到任意一个文本文件中，保存并重命名为你想要的名字，例如 test.glsl
3. 将你保存的文件路径赋值给任意一处接受静态图片的参数，例如：material.emission_map

下面代码将一个 `Shadertoy <https://shadertoy.com/>`_ 纹理设置为 Box 的自发光贴图：

::

	from glass_engine import *
	from glass_engine.Geometries import *

	scene, camera, _, _ = SceneRoam()

	box = Box(Lx=2, Ly=2, Lz=2)
	box.position.z = 1
	box.material.emission_map = "test.glsl"
	box.material.shading_model = Material.ShadingModel.Unlit

	scene.add(box)

	camera.screen.show()

能够得到如图 3 所示结果：

.. figure:: images/box.gif
   :align: center
   :scale: 50%

   图 3. 将 Shadertoy 动态纹理设置为 Box 的自发光贴图

除了从 Shadertoy 网站下载已有的 Shader，你也可以按照 Shadertoy 的 `编写规则 <https://www.shadertoy.com/howto>`_ 编写自己的动态 Shader 并设置为任意的纹理。