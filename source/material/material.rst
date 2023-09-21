材质
=========================

材质对象作为网格 ``Mesh`` 对象的一个属性存在，可以改变网格的视觉效果。任何 ``Mesh`` 都可通过 ``material`` 属性获取到自身的材质。本章主要讲解如何通过材质来改变 ``Mesh`` 的视觉效果。

材质对象含有一个 ``shading_model`` 属性表示材质的着色模型。着色模型决定了材质反射入射光的方式，进而直接决定了物体的外观。**Glass Engine** 具有多种着色模型可供选择，包括：

- ``Material.ShadingModel.Flat``：平面光照模型，光照颜色逐面渲染，没有高光；
- ``Material.ShadingModel.Gouraud``：Gouraud 光照模型，光照颜色逐顶点渲染并在面内插值；
- ``Material.ShadingModel.Phong``：Phong 光照模型，光照颜色逐像素渲染，计算高光时参考视线与反射向量夹角的余弦值；
- ``Material.ShadingModel.PhongBlinn``：Phong-Blinn 光照模型，光照颜色逐像素渲染，计算高光时参考半程向量与表面法线夹角的余弦值；
- ``Material.ShadingModel.Toon``：卡通模式渲染，基于 Phong 模型，但任何颜色不再渐变而是突变，能够产生卡通效果；
- ``Material.ShadingModel.OrenNayar``：Oren-Nayar 光照模型[`1 <https://doi.org/10.1145/192161.192213>`_]，是一种比 Lambert 漫反射模型更物理的漫反射模型，不计算高光；
- ``Material.ShadingModel.Minnaert``：Minnaert 光照模型[`2 <https://www.researchgate.net/publication/247923568_The_Lambertian_Assumption_and_Landsat_Data>`_]，光照颜色逐像素渲染，没有高光；
- ``Material.ShadingModel.Unlit``：不受光照影响，物体直接表现为自发光颜色或漫反射颜色；
- ``Material.ShadingModel.Fresnel``：Fresnel 着色模型，仅在边缘处产生渐变光；
- ``Material.ShadingModel.PBR``：基于物理的渲染模型，采用金属度/粗糙度工作流。

依据着色模型的不同，可供设置的材质属性也不同，这些属性包括：

.. role:: raw-html(raw)
    :format: html

.. list-table:: 材质属性
   :widths: 20 20 20 20 20 20
   :align: center
   :header-rows: 1

   * - 材质属性
     - .. figure:: images/Unlit.png
		   :align: center
		   :scale: 25%

		   Unlit
     - .. figure:: images/Flat.png
		   :align: center
		   :scale: 25%

		   Flat
     - .. figure:: images/Gouraud.png
		   :align: center
		   :scale: 25%

		   Gouraud
     - .. figure:: images/Phong.png
		   :align: center
		   :scale: 25%

		   Phong
     - .. figure:: images/PhongBlinn.png
		   :align: center
		   :scale: 25%

		   Phong-Blinn
   * - ambient : glm.vec3 :raw-html:`<br />` 环境光颜色
     - 
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - diffuse : glm.vec3 :raw-html:`<br />` 漫反射颜色
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - specular : glm.vec3 :raw-html:`<br />` 高光颜色
     - 
     - 
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - shininess : float :raw-html:`<br />` 闪耀度
     - 
     - 
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - glossiness : float :raw-html:`<br />` 光泽度
     - 
     - 
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - shininess_strength : float :raw-html:`<br />` 高光强度
     - 
     - 
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - emission : glm.vec3 :raw-html:`<br />` 自发光颜色
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - rim_power : float :raw-html:`<br />` 边缘光强度
     - 
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - base_color : glm.vec3 :raw-html:`<br />` 基础颜色
     - 
     - 
     - 
     - 
     - 
   * - metallic : float :raw-html:`<br />` 金属度
     - 
     - 
     - 
     - 
     - 
   * - roughness : float :raw-html:`<br />` 粗糙度
     - 
     - 
     - 
     - 
     - 
   * - diffuse_bands : int :raw-html:`<br />` 漫反射条带数
     - 
     - 
     - 
     - 
     - 
   * - specular_bands : int :raw-html:`<br />` 高光条带数
     - 
     - 
     - 
     - 
     - 
   * - diffuse_softness : float :raw-html:`<br />` 漫反射过度软度
     - 
     - 
     - 
     - 
     - 
   * - specular_softness : float :raw-html:`<br />` 高光过度软度
     - 
     - 
     - 
     - 
     - 
   * - reflection : glm.vec4 :raw-html:`<br />` 环境映射层颜色
     - 
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - refractive_index : float :raw-html:`<br />` 折射率
     - 
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - env_mix_diffuse : bool :raw-html:`<br />` 环境映射与漫反射颜色是否混合
     - 
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - dynamic_env_mapping : bool :raw-html:`<br />` 是否开启动态环境映射
     - 
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - auto_update_env_map : bool :raw-html:`<br />` 自动更新环境映射贴图
     - 
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - opacity : float :raw-html:`<br />` 材质不透明度
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - height_scale : float :raw-html:`<br />` 凹凸夸张系数
     - 
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - fog : bool :raw-html:`<br />` 是否受雾影响
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - recv_shadows : bool :raw-html:`<br />` 是否接收阴影
     - 
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - cast_shadows : bool :raw-html:`<br />` 是否投射阴影
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`

.. list-table:: 材质属性（续）
   :widths: 20 20 20 20 20 20
   :align: center
   :header-rows: 1

   * - 材质属性
     - .. figure:: images/OrenNayar.png
		   :align: center
		   :scale: 25%

		   Oren-Nayar
     - .. figure:: images/Minnaert.png
		   :align: center
		   :scale: 25%

		   Minnaert
     - .. figure:: images/Toon.png
		   :align: center
		   :scale: 25%

		   Toon
     - .. figure:: images/Fresnel.png
		   :align: center
		   :scale: 25%

		   Fresnel
     - .. figure:: images/PBR.png
		   :align: center
		   :scale: 25%

		   PBR
   * - ambient : glm.vec3 :raw-html:`<br />` 环境光颜色
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - diffuse : glm.vec3 :raw-html:`<br />` 漫反射颜色
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - 
   * - specular : glm.vec3 :raw-html:`<br />` 高光颜色
     - 
     - 
     - :raw-html:`&check;`
     - 
     - 
   * - shininess : float :raw-html:`<br />` 闪耀度
     - 
     - 
     - :raw-html:`&check;`
     - 
     - 
   * - glossiness : float :raw-html:`<br />` 光泽度
     - 
     - 
     - :raw-html:`&check;`
     - 
     - 
   * - shininess_strength : float :raw-html:`<br />` 高光强度
     - 
     - 
     - :raw-html:`&check;`
     - 
     - 
   * - emission : glm.vec3 :raw-html:`<br />` 自发光颜色
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - rim_power : float :raw-html:`<br />` 边缘光强度
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - 
   * - base_color : glm.vec3 :raw-html:`<br />` 基础颜色
     - 
     - 
     - 
     - 
     - :raw-html:`&check;`
   * - metallic : float :raw-html:`<br />` 金属度
     - 
     - 
     - 
     - 
     - :raw-html:`&check;`
   * - roughness : float :raw-html:`<br />` 粗糙度
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - 
     - 
     - :raw-html:`&check;`
   * - diffuse_bands : int :raw-html:`<br />` 漫反射条带数
     - 
     - 
     - :raw-html:`&check;`
     - 
     - 
   * - specular_bands : int :raw-html:`<br />` 高光条带数
     - 
     - 
     - :raw-html:`&check;`
     - 
     - 
   * - diffuse_softness : float :raw-html:`<br />` 漫反射过度软度
     - 
     - 
     - :raw-html:`&check;`
     - 
     - 
   * - specular_softness : float :raw-html:`<br />` 高光过度软度
     - 
     - 
     - :raw-html:`&check;`
     - 
     - 
   * - reflection : glm.vec4 :raw-html:`<br />` 环境映射层颜色
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - refractive_index : float :raw-html:`<br />` 折射率
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - env_mix_diffuse : bool :raw-html:`<br />` 环境映射与漫反射颜色是否混合
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - dynamic_env_mapping : bool :raw-html:`<br />` 是否开启动态环境映射
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - auto_update_env_map : bool :raw-html:`<br />` 自动更新环境映射贴图
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - opacity : float :raw-html:`<br />` 材质不透明度
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - height_scale : float :raw-html:`<br />` 凹凸夸张系数
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - fog : bool :raw-html:`<br />` 是否受雾影响
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - recv_shadows : bool :raw-html:`<br />` 是否接收阴影
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
   * - cast_shadows : bool :raw-html:`<br />` 是否投射阴影
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`
     - :raw-html:`&check;`

下面我们从以下角度展开详细描述：

.. toctree::
   :maxdepth: 1

   common_props/common_props
   shading_models/shading_models
   internal_materials/internal_materials
