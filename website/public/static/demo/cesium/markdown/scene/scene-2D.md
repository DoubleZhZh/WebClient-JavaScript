## 二维模式

### 示例功能

此功能用于将三维球展开，变成二维地图模式。

### 示例实现：

本示例需要使用include-cesium-local.js开发库实现，通过Cesium三维球控件 `Cesium.WebSceneControl()` 的 `changeSceneMode()` 方法切换地图显示模式。

### 实现步骤：

1. <font color=red>引用开发库</font>：本示例引用local本地【include-cesium-local.js】开发库, 完成此步后方可正常使用所有三维WebGL的功能；

2. <font color=red>创建三维地图容器并加载三维球控件</font>：创建 `id='GlobeView'` 的div作为三维视图的容器，并设置其样式，初始化Cesium三维球控件 `Cesium.WebSceneControl()` ，完成此步后可在三维场景中加载三维球控件；

``` Javascript
//构造三维视图类（视图容器div的id，三维视图设置参数）
var webGlobe = new Cesium.WebSceneControl('GlobeView', {
    terrainExaggeration: 1,
});
```

``` html
<div id='GlobeView'></div>
```

3.<font color=red>模式切换</font>：调用Cesium三维球控件 `Cesium.WebSceneControl()` 的 `changeSceneMode()` 方法切换地图显示模式；

``` Javascript
//模式切换
webGlobe.changeSceneMode('2D', 1)
```

### 关键接口

#### 1. `Cesium.WebSceneControl(elementId, options)` : 三维视图的主要类

##### (1) `changeSceneMode(sceneMode, duration)` 切换场景模式

> `changeSceneMode` 方法主要参数

|参数名|类型|说明|
|-|-|-|
|sceneMode|String|场景模式'3D', '2D', 'COLUMBUS_VIEW'(平面三维)|
|duration|Number|动画持续时间，<=0时，保持场景范围不变|
