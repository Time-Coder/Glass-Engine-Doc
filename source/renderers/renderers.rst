渲染器
====================

渲染器是 **Glass Engine** 完成渲染的核心模块，**Glass Engine** 内置两种渲染管线的渲染器，分别为

- ``ForwardRenderer``: 使用前向渲染管线的渲染器
- ``DeferredRenderer``: 使用延迟着色法管线的渲染器

这两种渲染器均定义在 ``glass_engine.Renderers`` 子模块中，可直接导入使用。**Glass Engine** 默认采用 ``ForwardRenderer`` 渲染器，你可以通过给 ``camera.screen`` 的 ``renderer`` 属性赋值来更改使用的渲染器。例如，你可以通过如下代码将渲染器修改为延迟着色渲染器：

::

	from glass_engine.Renderers import *
	camera.screen.renderer = DeferredRenderer()

另外，你还可以定义自己的渲染器在其中编写自己的渲染逻辑，只需继承自 ``Renderer`` 类并重写其中 ``render`` 方法即可。

.. _label_ForwardRenderer:

前向渲染
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Glass Engine** 默认采用前向渲染的渲染器，该渲染管线能够利用多重采样抗锯齿 (Multi-Sampling Anti-Aliasing, MSAA) 得到比较平滑的物体边缘。MSAA 默认已开启，你可通过设置 ``camera.screen.samples`` 属性设置多重采样数，默认为 4，将其设置为不大于 1 的数则为关闭多重采样抗锯齿。

其缺点为场景中光源较多时，帧率会大幅降低，你可以将其替换为延迟着色法渲染器以提高渲染效率。（前提是多光源都关闭阴影，否则延迟着色法也没法补救。）

.. _label_DeferredRenderer:

延迟着色法
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

当你通过 ``camera.screen.renderer = DeferredRenderer()`` 将渲染器切换为 ``DeferredRenderer`` 之后，其将采用延迟着色法进行渲染。延迟着色法能够很好地提高多光源渲染效率，但有两个较大的缺陷：

- MSAA 抗锯齿有一点效果但十分不明显，默认已关闭。默认采用快速近似抗锯齿 (Fast Approximate Anti-Aliasing, FXAA) 策略，但效果没有前向渲染的 MSAA 好；
- 使用 Toon 着色模型时，材质的 ``Toon_diffuse_softness`` 和 ``Toon_specular_softness`` 参数无法生效。原因在于渲染目标个数存在硬件上限，最多八个，每个渲染目标最多四个分量，已经尽可能的将材质参数压缩到这八个渲染目标中，上面提到的两个实在无法存储，只能选择抛弃。

自定义渲染器
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

如果你想实现自己的渲染管线，需要编写自定义渲染器继承自 ``Renderer``，并重写其中的 ``render`` 方法，这对普通用户来说难度较大，在此处不再展开讲解。真的希望重写 ``render`` 方法的用户，可以参考 ``ForwardRenderer.py`` 和 ``DeferredRenderer.py`` 的源码。