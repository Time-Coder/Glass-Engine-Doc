安装
========================================

操作系统要求
~~~~~~~~~~~~~~~~~~~~~~~~~~~
目前 **Glass Engine** 仅支持 Windows，对支持 Linux 和 Mac OS 的支持在开发计划当中。如果您需要 Linux 和 Mac OS 版，请在 `github <https://github.com/Time-Coder/Glass-Engine>`_ 或 `gitee <https://gitee.com/time-coder/Glass-Engine>`_ 上提交 issue，我看到后会将支持 Linux 和 Mac OS 的工作优先处理。

对操作系统位数而言，**Glass Engine** 对 win32 和 x64 均支持。

Python 版本要求
~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Glass Engine** 要求 Python 版本大于等于 3.7，并不打算支持低版本的 Python 。

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

如果在安装依赖 PyOpenGL-accelerate 时报出如下错误：

::

    Building wheel for PyOpenGL-accelerate (pyproject.toml) ... error
      error: subprocess-exited-with-error

      × Building wheel for PyOpenGL-accelerate (pyproject.toml) did not run successfully.
      │ exit code: 1
      ╰─> [14 lines of output]
          running bdist_wheel
          running build
          running build_py
          creating build
          creating build\lib.win-amd64-cpython-312
          creating build\lib.win-amd64-cpython-312\OpenGL_accelerate
          copying OpenGL_accelerate\__init__.py -> build\lib.win-amd64-cpython-312\OpenGL_accelerate
          running build_ext
          C:\Users\wenzhan\AppData\Local\Temp\pip-build-env-rbsildcn\overlay\Lib\site-packages\Cython\Compiler\Main.py:381: FutureWarning: Cython directive 'language_level' not set, using '3str' for now (Py3). This has changed from earlier releases! File: C:\Users\wenzhan\AppData\Local\Temp\pip-install-damfrb3k\pyopengl-accelerate_03c836a626714ba48530f392b41f41a5\OpenGL_accelerate\wrapper.pxd
            tree = Parsing.p_module(s, pxd, full_module_name)
          Compiling src\wrapper.pyx because it changed.
          [1/1] Cythonizing src\wrapper.pyx
          building 'OpenGL_accelerate.wrapper' extension
          error: Microsoft Visual C++ 14.0 or greater is required. Get it with "Microsoft C++ Build Tools": https://visualstudio.microsoft.com/visual-cpp-build-tools/
          [end of output]

      note: This error originates from a subprocess, and is likely not a problem with pip.
      ERROR: Failed building wheel for PyOpenGL-accelerate
    Failed to build PyOpenGL-accelerate
    ERROR: Could not build wheels for PyOpenGL-accelerate, which is required to install pyproject.toml-based projects

这是因为 PyOpenGL-accelerate 还没有正式支持 Python 3.12，而你恰好在使用 Python 3.12 并且电脑里没有安装 Microsoft Visual Studio，无法通过源码编译 PyOpenGL-accelerate 进行安装。

解决办法为：到 `github <https://github.com/Time-Coder/Glass-Engine/tree/main/PyOpenGL-accelerate>`_ 或 `gitee <https://gitee.com/time-coder/Glass-Engine/tree/main/PyOpenGL-accelerate>`_ 手动下载 PyOpenGL-accelerate for Python 3.12 的 wheel 包并使用 pip install 进行安装。
