## 加载谷歌地图

### 示例功能

本示例对接谷歌地图服务，实现在三维场景中加载谷歌地图，具体类型包括矢量、影像、栅格、道路。

### 示例实现

本示例需要使用【include-cesium-local.js】开发库实现，关键接口为`WebSceneControl`类提供的`appendGoogleMapExt()`方法，以此来加载谷歌地图。

> 开发库使用请参见*首页-概述-原生JS调用*内容。

> 使用谷歌地图请注意`藏南`与`南海九段线`问题，建议使用天地图。

### 实现步骤

1. 引用开发库：本示例引用local本地【include-cesium-local.js】开发库；

2. 创建布局：创建`id='GlobeView'`的div作为三维视图的容器，并设置其样式；

3. 构造三维场景控件：实例化WebSceneControl对象；

    ``` javascript
    //构造三维视图类（视图容器div的id，三维视图设置参数）
    var webGlobe = new Cesium.WebSceneControl('GlobeView', {
        terrainExaggeration: 1,
    });
    ```

4. 加载数据：调用`appendGoogleMapExt()`方法加载Google地图，为`ptype`属性配置不同参数可加载不同类型地图，如加载矢量可传入：‘m@207000000’、影像：‘s@130’、栅格：‘t@130’、道路：‘h@207000000’；

    ``` javascript
    //添加Google地图
    webGlobe.appendGoogleMapExt({
        ptype: 'm@207000000'
    });
    ```

5. 鼠标位置显示控件：创建`id="coordinate_location"`的div作为容器，用于显示鼠标当前位置的经纬度、高程、视角高度信息；然后调用`showPosition()`方法为三维场景控件设置鼠标位置显示控件。

    ``` javascript
    //显示鼠标位置控件
    webGlobe.showPosition('coordinate_location');
    ```

### 关键接口

#### 1.【三维场景控件】WebSceneControl

##### （1）`new WebSceneControl(elementId, options)`：三维场景控件构造函数

> `WebSceneControl`构造函数主要参数

|参数名|类 型|说 明|
|-|-|-|
|elementId|Element \| String|放置视图的div的id|
|options|Object|（可选）附加属性|

> `options`属性主要参数

|参数名|类 型|默认值|说 明|
|-|-|-|-|
|viewerMode|String|‘3D’|（可选）初始视图模式默认为三维球视图 '2D'表示二维视图 'COLUMBUS_VIEW' 表示三维平面视图|
|showInfo|Boolean|false|（可选）是否显示默认的属性信息框|
|animation|Boolean|true|（可选）默认动画控制不显示|
|baseLayerPicker|Boolean|true|（可选）是否创建图层控制显示小组件|
|fullscreenButton|Boolean|true|（可选）是否创建全屏控制按钮|
|vrButton|Boolean|false|（可选）是否创建VR按钮|

##### （2）`appendGoogleMapExt(options)`：添加Google地图服务

> `appendGoogleMapExt`方法主要参数

|参数名|类 型|说 明|
|-|-|-|
|options|Object|{ptype:'s'}|

##### （3）`showPosition(elementId, options)`：显示经纬度 高程 视角高度

> `showPosition`方法主要参数

|参数名|类 型|说 明|
|-|-|-|
|elementId|Element \| String|要显示的div的id|
|options|Object|附加属性|

> `options`属性主要参数

|参数名|类 型|默认值|说 明|
|-|-|-|-|
|showHpr|Boolean|false|（可选） |
|showSelectTileInfo|Boolean|false|（可选）显示当前鼠标所在位置拾取到的级别|
|showViewLevelInfo|Boolean|false|（可选）显示视图级别|
