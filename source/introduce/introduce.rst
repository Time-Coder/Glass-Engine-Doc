介绍
==================

说明
~~~~~~~~~~~~~~~~~~~~

**Glass Engine** 是一个 Python 原生的 3D 实时渲染引擎，免费开源。你可以使用它在你的 Python 程序界面的任何位置嵌入可交互的 3D 画面。与同类产品 Unreal Engine、Unity 3D、OSG、OGRE、Panda3D 等相比，**Glass Engine** 具有如下优势：

- 不引入新的界面系统，可直接在你熟悉的 Python 界面系统中嵌入 3D 视口（目前支持 PySide6/PySide2/PyQt6/PyQt5，计划支持 Tkinter/wxPython/PyGTK/PyGame），能够更方便的与渲染之外的逻辑进行交互；
- 更加直观易用，开发逻辑和编程接口更加符合人类直觉；
- Python 原生，并不是对 C++ 程序的 Python 绑定，行为更加 Pythonic。

在渲染方面，**Glass Engine** 具有以下特色：

- 采用 :ref:`label_scene_graph` (Scene Graph) 形式组织场景，对场景进行逻辑分组、固结运动、设置相对坐标等操作更加方便；
- 用户可控的实例化渲染 (Instanced Rendering)，极大程度的合并渲染批次，减少渲染调用；
- 用户透明的顶点共享机制，使得相同参数几何体共用同一组顶点和索引，提高渲染效率；
- 支持 :ref:`label_self_geo` 的动态构建，无需模型文件也能创建丰富场景；
- 内置三十多种 :ref:`label_geometries`，对一些简单几何体的创建无需从模型加载也不需要自定义顶点索引；
- 支持超过四十种模型文件格式的 :ref:`label_model` 加载；
- 支持多种 :ref:`label_shading_models`，包括 :ref:`label_Flat`、:ref:`label_Gouraud`、:ref:`label_Phong`、:ref:`label_PhongBlinn`、:ref:`label_Toon`、:ref:`label_OrenNayar`、:ref:`label_Minnaert`、:ref:`label_Fresnel`、:ref:`label_PBR` 等；
- 支持 :ref:`label_multi_cameras` 多视口，多视口共享场景资源；
- 用户透明的 Shader 预编译和增量编译过程，可极大程度提高程序启动速度；
- 支持 :ref:`label_ForwardRenderer` (Forward Rendering) 和 :ref:`label_DeferredRenderer` (Deferred Rendering) 管线，可由用户自由选择；
- 使用基于物理的 :ref:`label_bloom` 技术 (Physical based Bloom)，提升泛光真实感；
- 支持基于弥散圆 (Circle of Confusion， CoC) 理论的 :ref:`label_DOF` 效果，并可根据点击自动渐变对焦；
- 使用顺序无关的半透明 (Order Independent Transparent, OIT) 技术渲染半透明物体，用户不再需要关心渲染顺序；
- 采用级联阴影映射 (Casecading Shadow Map, CSM) 技术渲染阴影，极大程度上提高了阴影清晰度；
- 支持动态环境映射，更逼真的反射和折射效果，倒影中仍能呈现半透明、阴影等效果；
- 提供可叠加的 :ref:`label_PPEs` 机制，内置多种后处理效果，并可轻松 :ref:`label_self_defined_PPE`；
- 支持 :ref:`label_shadertory`，`Shadertoy <https://shadertoy.com/>`_ 代码可直接转化为纹理贴图使用；

开发路线
~~~~~~~~~~~~~~~~~~~~~~

.. |checkbox-unchecked| unicode:: U+2610
.. |checkbox-checked| unicode:: U+2611

**Glass Engine** 当前为 0.1.* 版本，后续将不断迭代升版，后续 10 个版本的开发计划为：

- 0.1.* 版本：基本渲染架构（已完成）
	- |checkbox-checked| 渲染基本要素：场景图、光源、阴影、相机、网格、简单材质系统、模型加载
	- |checkbox-checked| 场景环境：天空盒、天空穹顶、雾
	- |checkbox-checked| 后处理效果：SSAO、HDR、LUT、FXAA、景深、泛光、自定义后效
	- |checkbox-checked| 常见渲染管线：前向渲染、延迟着色法、自定义管线
	- |checkbox-checked| 键鼠交互模式：场景漫游、模型浏览、自定义模式
- 0.2.* 版本：完善渲染要素
	- |checkbox-unchecked| 基于有符号距离场的文字渲染
	- |checkbox-unchecked| 任意多边形三角网构建
	- |checkbox-unchecked| 点云数据三角化
	- |checkbox-unchecked| 网格布尔运算
	- |checkbox-unchecked| 鼠标点选拾取功能
	- |checkbox-unchecked| USD 格式保存
- 0.3.* 版本：完善渲染要素
	- |checkbox-unchecked| 高级软阴影算法：CSM、VSM、ESM、MSM、VSSM、EVSM
	- |checkbox-unchecked| 半透明物体阴影、折射体阴影
	- |checkbox-unchecked| 平面镜反射效果
	- |checkbox-unchecked| SSR 屏幕空间反射后处理效果
	- |checkbox-unchecked| IBL 以及 Specular/Glossiness 工作流的 PBR
	- |checkbox-unchecked| BVH 树、视锥体剔除以及自动 Lod 等提高渲染效率的算法
- 0.4.* 版本：完善渲染要素
	- |checkbox-unchecked| 更多高级着色模型：清漆、次表面、皮肤、毛发、布料等，向 Unreal Engine 看齐
	- |checkbox-unchecked| 自定义着色模型
	- |checkbox-unchecked| 面光源
	- |checkbox-unchecked| 粒子特效
	- |checkbox-unchecked| 骨骼动画、顶点动画
- 0.5.* 版本：完善空间环境渲染
	- |checkbox-unchecked| 随机地形、tif 地形
	- |checkbox-unchecked| 体积光/丁达尔效应
	- |checkbox-unchecked| 体积雾
	- |checkbox-unchecked| 体积云
	- |checkbox-unchecked| 雨、雪
	- |checkbox-unchecked| 大气散射模型
- 0.6.* 版本：跨 Python 端 GUI 框架
	- |checkbox-unchecked| 支持 Tkinter
	- |checkbox-unchecked| 支持 PyGame
	- |checkbox-unchecked| 支持 PyGTK
	- |checkbox-unchecked| 支持 wxPython
- 0.7.* 版本：跨图形编程接口
	- |checkbox-unchecked| 支持 Vulkan
	- |checkbox-unchecked| 支持 Direct 3D
	- |checkbox-unchecked| 支持 Metal
- 0.8.* 版本：|checkbox-unchecked| 支持音效
- 0.9.* 版本：|checkbox-unchecked| 支持物理
- 0.10.* 版本：|checkbox-unchecked| 支持网络
- 1.0.* 版本：|checkbox-unchecked| Glass Engine Editor 编辑器


第三方库引用情况
~~~~~~~~~~~~~~~~~~~~

**Glass Engine** 基本上完全基于 PyOpenGL 开发，在一些细节方面还引用了一些其他第三方库，重要的库包括：

- `PyOpenGL <https://pyopengl.sourceforge.net/>`_：提供渲染的底层接口；
- `PySide <https://wiki.qt.io/Qt_for_Python>`_/`PyQt <https://www.riverbankcomputing.com/software/pyqt/>`_：用作 OpenGL 的窗口系统。目前仅支持 PySide2/PySide6/PyQt5/PyQt6 窗口系统，对其他 GUI 系统（Tkinter/wxPython/PyGTK/PyGame）的支持则在进一步的开发计划当中；
- `qt-material <https://pypi.org/project/qt-material/>`_：用于美化示例程序的界面；
- `PyGLM <https://pypi.org/project/PyGLM/>`_：用于存储向量、四元数；
- `Numpy <https://numpy.org/>`_：用于管理连续内存、做矩阵运算等；
- `OpenCV <https://pypi.org/project/opencv-python/>`_：用于加载纹理图像、转换图片格式；
- `Pillow <https://python-pillow.org/>`_：用于加载一些特殊格式纹理图像；
- `pyroexr <https://pypi.org/project/pyroexr/>`_：用于加载 exr 格式的 HDR 图像；
- `Assimp <https://github.com/assimp/assimp>`_：用于加载模型。

联系方式
~~~~~~~~~~~~~~~~

**Glass Engine** 目前仅有一人维护，如果有任何 bug、新需求或想要参与开发，可在以下项目主页提交 issue 或 pull request：

- Github 项目主页：https://github.com/Time-Coder/Glass-Engine
- Gitee 项目主页：https://gitee.com/time-coder/Glass-Engine

如有任何关于本文档的问题，可在以下文档项目主页提交 issue 或 pull request：

- Github 项目主页：https://github.com/Time-Coder/Glass-Engine-Doc
- Gitee 项目主页：https://gitee.com/time-coder/Glass-Engine-Doc

或者，你还可以通过邮箱 binghui.wang@foxmail.com 直接联系到作者本人。

开源许可证
~~~~~~~~~~~~~~~~~

**Glass Engine** 完全使用 `MIT 开源许可证 <https://mit-license.org/>`_，没有任何附加条款，该许可指出：任何人可在不受限制的情况下处理本软件，包括但不限于使用、复制、修改、合并、发布、分发、分许可和出售。只有一点需要遵守的条件，就是在你使用 **Glass Engine** 开发并发布的软件目录下，必须放置一份 **Glass Engine** 的许可文件，除此之外，别无任何限制。

	| The MIT License (MIT)
	| Copyright © 2023 王炳辉 (Bing-Hui WANG)
	| 
	| Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

	| The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

	| THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.