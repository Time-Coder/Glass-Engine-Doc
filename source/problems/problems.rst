常见问题
====================

1. 问题：渲染结果没有阴影，而且报如下警告：

::

	Extension GL_ARB_bindless_texture is not available.
	Shadows and dynamic environment mapping will be disabled.
	Try to change default graphics card of python.exe to high performance one.

原因：出现该警告的原因在于你的显卡不支持无绑定纹理 GL_ARB_bindless_texture 扩展，在 **Glass Engine** 中采用了无绑定纹理技术以渲染多光源阴影，因此，如果不支持该扩展，则无法渲染阴影，同样的，动态环境映射也无法渲染。计划在 0.1.* 的某个版本中将解决此问题：针对不同的显卡，采用不同的阴影和动态环境映射渲染方案。

2. 问题：无法出渲染结果，报如下错误：

::

	Current OpenGL version (your version) is lower than minimum version require (OpenGL 4.3)

原因：出现该警告的原因在于你的显卡所支持的 OpenGL 版本过低，**Glass Engine** 要求最低支持 OpenGL 4.3。并没有计划支持低于 OpenGL 4.3 的版本。

3. 问题：无法出渲染结果，报如下错误：

::

	glass.GPUProgram.LinkError: Error when linking following files:
	  glass_engine/glsl/Pipelines/forward_rendering/forward_rendering.vs
	  glass_engine/glsl/Pipelines/forward_rendering/forward_rendering.gs
	  glass_engine/glsl/Pipelines/forward_rendering/forward_rendering.fs
	Out of resource error.

原因：链接着色器程序时，由于着色器程序代码量较大，导致显存溢出。目前 **Glass Engine** 中将 10 种着色模型的代码放在了同一个着色器程序中，导致单个着色器程序代码臃肿，计划在 0.4.0 版本解决该问题：一个着色模型对应一个着色器程序，减少但着色器程序代码量，并使着色模型可用户扩展。

以上三个问题都可以通过更换显卡解决。如果你用的电脑含有多张显卡，请将 python.exe 程序指定使用高性能显卡，在笔记本电脑上往往为 Nvidia 独显。另外，更新显卡驱动程序也有可能会解决这些问题。