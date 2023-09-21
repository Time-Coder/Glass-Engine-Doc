内置材质
~~~~~~~~~~~~~~~~~~~~~~

**Glass Engine** 内置了一些材质可供使用，这些材质参数来自网站 `devernay.free.fr <http://devernay.free.fr/cours/opengl/materials.html>`_，这些材质仅针对传统着色模型，PBR 则不适用。这些内置材质在不同着色模型下的视觉效果见下面两表。我们可轻松的设置材质为某个内置材质，例如下面代码将某个球体的材质设置为翡翠：

::

    sphere.material.set_as(Material.Type.Emerald)

下表所列的所有内置材质的英文名称均可通过加上前缀 ``Material.Type.`` 访问到。

.. role:: raw-html(raw)
    :format: html

.. list-table:: 内置材质
   :widths: 20 20 20 20 20
   :align: center
   :header-rows: 1

   * - 内置材质名称
     - Flat
     - Gouraud
     - Phong
     - Phong-Blinn
   * - Emerald 翡翠
     - .. figure:: images/Emerald_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/Emerald_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/Emerald_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/Emerald_PhongBlinn.png
           :align: center
           :scale: 25%
   * - Jade 玉
     - .. figure:: images/Jade_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/Jade_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/Jade_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/Jade_PhongBlinn.png
           :align: center
           :scale: 25%
   * - Obsidian 黑曜石
     - .. figure:: images/Obsidian_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/Obsidian_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/Obsidian_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/Obsidian_PhongBlinn.png
           :align: center
           :scale: 25%
   * - Pearl 珍珠
     - .. figure:: images/Pearl_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/Pearl_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/Pearl_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/Pearl_PhongBlinn.png
           :align: center
           :scale: 25%
   * - Ruby 红宝石
     - .. figure:: images/Ruby_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/Ruby_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/Ruby_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/Ruby_PhongBlinn.png
           :align: center
           :scale: 25%
   * - Turquoise 绿松石
     - .. figure:: images/Turquoise_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/Turquoise_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/Turquoise_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/Turquoise_PhongBlinn.png
           :align: center
           :scale: 25%
   * - Brass 黄铜
     - .. figure:: images/Brass_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/Brass_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/Brass_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/Brass_PhongBlinn.png
           :align: center
           :scale: 25%
   * - Bronze 青铜
     - .. figure:: images/Bronze_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/Bronze_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/Bronze_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/Bronze_PhongBlinn.png
           :align: center
           :scale: 25%
   * - Chrome 铬合金
     - .. figure:: images/Chrome_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/Chrome_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/Chrome_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/Chrome_PhongBlinn.png
           :align: center
           :scale: 25%
   * - Copper 铜
     - .. figure:: images/Copper_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/Copper_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/Copper_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/Copper_PhongBlinn.png
           :align: center
           :scale: 25%
   * - Gold 金
     - .. figure:: images/Gold_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/Gold_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/Gold_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/Gold_PhongBlinn.png
           :align: center
           :scale: 25%
   * - Silver 银
     - .. figure:: images/Silver_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/Silver_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/Silver_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/Silver_PhongBlinn.png
           :align: center
           :scale: 25%
   * - BlackPlastic 黑色塑料
     - .. figure:: images/BlackPlastic_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/BlackPlastic_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/BlackPlastic_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/BlackPlastic_PhongBlinn.png
           :align: center
           :scale: 25%
   * - CyanPlastic 青色塑料
     - .. figure:: images/CyanPlastic_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/CyanPlastic_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/CyanPlastic_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/CyanPlastic_PhongBlinn.png
           :align: center
           :scale: 25%
   * - GreenPlastic 绿色塑料
     - .. figure:: images/GreenPlastic_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/GreenPlastic_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/GreenPlastic_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/GreenPlastic_PhongBlinn.png
           :align: center
           :scale: 25%
   * - RedPlastic 红色塑料
     - .. figure:: images/RedPlastic_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/RedPlastic_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/RedPlastic_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/RedPlastic_PhongBlinn.png
           :align: center
           :scale: 25%
   * - WhitePlastic 白色塑料
     - .. figure:: images/WhitePlastic_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/WhitePlastic_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/WhitePlastic_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/WhitePlastic_PhongBlinn.png
           :align: center
           :scale: 25%
   * - YellowPlastic 黄色塑料
     - .. figure:: images/YellowPlastic_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/YellowPlastic_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/YellowPlastic_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/YellowPlastic_PhongBlinn.png
           :align: center
           :scale: 25%
   * - BlackRubber 黑色橡胶
     - .. figure:: images/BlackRubber_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/BlackRubber_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/BlackRubber_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/BlackRubber_PhongBlinn.png
           :align: center
           :scale: 25%
   * - CyanRubber 青色橡胶
     - .. figure:: images/CyanRubber_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/CyanRubber_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/CyanRubber_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/CyanRubber_PhongBlinn.png
           :align: center
           :scale: 25%
   * - GreenRubber 绿色橡胶
     - .. figure:: images/GreenRubber_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/GreenRubber_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/GreenRubber_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/GreenRubber_PhongBlinn.png
           :align: center
           :scale: 25%
   * - RedRubber 红色橡胶
     - .. figure:: images/RedRubber_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/RedRubber_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/RedRubber_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/RedRubber_PhongBlinn.png
           :align: center
           :scale: 25%
   * - WhiteRubber 白色橡胶
     - .. figure:: images/WhiteRubber_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/WhiteRubber_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/WhiteRubber_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/WhiteRubber_PhongBlinn.png
           :align: center
           :scale: 25%
   * - YellowRubber 黄色橡胶
     - .. figure:: images/YellowRubber_Flat.png
           :align: center
           :scale: 25%
     - .. figure:: images/YellowRubber_Gouraud.png
           :align: center
           :scale: 25%
     - .. figure:: images/YellowRubber_Phong.png
           :align: center
           :scale: 25%
     - .. figure:: images/YellowRubber_PhongBlinn.png
           :align: center
           :scale: 25%


.. list-table:: 内置材质（续）
   :widths: 20 20 20 20 20
   :align: center
   :header-rows: 1

   * - 内置材质名称
     - Oren-Nayar
     - Minnaert
     - Toon
     - Fresnel
   * - Emerald 翡翠
     - .. figure:: images/Emerald_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/Emerald_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/Emerald_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/Emerald_Fresnel.png
           :align: center
           :scale: 25%
   * - Jade 玉
     - .. figure:: images/Jade_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/Jade_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/Jade_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/Jade_Fresnel.png
           :align: center
           :scale: 25%
   * - Obsidian 黑曜石
     - .. figure:: images/Obsidian_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/Obsidian_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/Obsidian_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/Obsidian_Fresnel.png
           :align: center
           :scale: 25%
   * - Pearl 珍珠
     - .. figure:: images/Pearl_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/Pearl_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/Pearl_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/Pearl_Fresnel.png
           :align: center
           :scale: 25%
   * - Ruby 红宝石
     - .. figure:: images/Ruby_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/Ruby_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/Ruby_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/Ruby_Fresnel.png
           :align: center
           :scale: 25%
   * - Turquoise 绿松石
     - .. figure:: images/Turquoise_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/Turquoise_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/Turquoise_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/Turquoise_Fresnel.png
           :align: center
           :scale: 25%
   * - Brass 黄铜
     - .. figure:: images/Brass_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/Brass_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/Brass_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/Brass_Fresnel.png
           :align: center
           :scale: 25%
   * - Bronze 青铜
     - .. figure:: images/Bronze_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/Bronze_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/Bronze_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/Bronze_Fresnel.png
           :align: center
           :scale: 25%
   * - Chrome 铬合金
     - .. figure:: images/Chrome_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/Chrome_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/Chrome_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/Chrome_Fresnel.png
           :align: center
           :scale: 25%
   * - Copper 铜
     - .. figure:: images/Copper_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/Copper_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/Copper_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/Copper_Fresnel.png
           :align: center
           :scale: 25%
   * - Gold 金
     - .. figure:: images/Gold_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/Gold_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/Gold_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/Gold_Fresnel.png
           :align: center
           :scale: 25%
   * - Silver 银
     - .. figure:: images/Silver_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/Silver_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/Silver_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/Silver_Fresnel.png
           :align: center
           :scale: 25%
   * - BlackPlastic 黑色塑料
     - .. figure:: images/BlackPlastic_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/BlackPlastic_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/BlackPlastic_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/BlackPlastic_Fresnel.png
           :align: center
           :scale: 25%
   * - CyanPlastic 青色塑料
     - .. figure:: images/CyanPlastic_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/CyanPlastic_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/CyanPlastic_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/CyanPlastic_Fresnel.png
           :align: center
           :scale: 25%
   * - GreenPlastic 绿色塑料
     - .. figure:: images/GreenPlastic_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/GreenPlastic_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/GreenPlastic_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/GreenPlastic_Fresnel.png
           :align: center
           :scale: 25%
   * - RedPlastic 红色塑料
     - .. figure:: images/RedPlastic_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/RedPlastic_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/RedPlastic_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/RedPlastic_Fresnel.png
           :align: center
           :scale: 25%
   * - WhitePlastic 白色塑料
     - .. figure:: images/WhitePlastic_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/WhitePlastic_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/WhitePlastic_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/WhitePlastic_Fresnel.png
           :align: center
           :scale: 25%
   * - YellowPlastic 黄色塑料
     - .. figure:: images/YellowPlastic_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/YellowPlastic_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/YellowPlastic_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/YellowPlastic_Fresnel.png
           :align: center
           :scale: 25%
   * - BlackRubber 黑色橡胶
     - .. figure:: images/BlackRubber_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/BlackRubber_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/BlackRubber_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/BlackRubber_Fresnel.png
           :align: center
           :scale: 25%
   * - CyanRubber 青色橡胶
     - .. figure:: images/CyanRubber_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/CyanRubber_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/CyanRubber_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/CyanRubber_Fresnel.png
           :align: center
           :scale: 25%
   * - GreenRubber 绿色橡胶
     - .. figure:: images/GreenRubber_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/GreenRubber_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/GreenRubber_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/GreenRubber_Fresnel.png
           :align: center
           :scale: 25%
   * - RedRubber 红色橡胶
     - .. figure:: images/RedRubber_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/RedRubber_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/RedRubber_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/RedRubber_Fresnel.png
           :align: center
           :scale: 25%
   * - WhiteRubber 白色橡胶
     - .. figure:: images/WhiteRubber_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/WhiteRubber_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/WhiteRubber_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/WhiteRubber_Fresnel.png
           :align: center
           :scale: 25%
   * - YellowRubber 黄色橡胶
     - .. figure:: images/YellowRubber_OrenNayar.png
           :align: center
           :scale: 25%
     - .. figure:: images/YellowRubber_Minnaert.png
           :align: center
           :scale: 25%
     - .. figure:: images/YellowRubber_Toon.png
           :align: center
           :scale: 25%
     - .. figure:: images/YellowRubber_Fresnel.png
           :align: center
           :scale: 25%