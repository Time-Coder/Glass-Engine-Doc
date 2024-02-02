安装
========================================

操作系统要求
~~~~~~~~~~~~~~~~~~~~~~~~~~~
目前 **Glass Engine** 支持以下平台：

- AMD64 架构的 Windows 64bit 与 32bit
- x86_64 架构的 Linux 64bit
- aarch64 架构的 Linux 64bit
- x86_64 架构的 macOS 14 64bit

如需要支持其他平台，请通过 `Github <https://github.com/Time-Coder/Glass-Engine>`_ 或 `Gitee <https://gitee.com/time-coder/Glass-Engine>` 平台提 issue，或直接通过邮箱 binghui.wang@foxmail.com 联系作者本人进行支持。

Python 版本要求
~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Glass Engine** 要求 Python 版本大于等于 3.7，并不打算支持更低版本的 Python 。

显卡要求
~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Glass Engine** 要求显卡最低支持 OpenGL 4.3，Nvidia/AMD/Intel 显卡均可，集显/核显/独显均可。当显卡不支持 OpenGL 4.3 时，运行时会给出提示并直接退出。

另外，显卡最好支持 OpenGL 扩展 GL_ARB_bindless_texture，否则阴影和动态环境映射不会生效并会报出如下警告：

::

    Extension GL_ARB_bindless_texture is not available.
    Shadows and dynamic environment mapping will be disabled.
    Try to change default graphics card of python.exe to high performance one.

安装
~~~~~~~~~~~~~~~~~~~~~~~~~~~

安装 **Glass Engine** 非常简单，在命令行使用如下命令即可完成对 **Glass Engine** 的安装：

::

    pip install glass-engine --upgrade

如果你是中国区用户，则可以使用如下命令加速其安装：

::

    pip install glass-engine --upgrade -i https://pypi.tuna.tsinghua.edu.cn/simple

如果你已经安装 0.1.30 及以下版本的 Glass-Engine，并需要往更高版本更新，请先使用如下命令删除老版本的 Glass-Engine

::

    pip uninstall glass-engine

随后再进行新版本的安装。否则将会在导入 glass_engine 时报出如下错误：

::

    ModuleNotFoundError: No module named 'glass'
