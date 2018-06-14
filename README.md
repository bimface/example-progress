# 功能介绍

基于BIMFACE JS-SDK灵活使用进度模拟应用场景

# 效果图
![view](resources/img/view.png)

# 前端实现

## 引用BIMFACE的JavaScript显示组件库
```javascript
<script src="https://static.bimface.com/api/BimfaceSDKLoader/BimfaceSDKLoader@latest-release.js" charset="utf-8"></script>
```
## 定义DOM元素，用于在该DOM元素中显示模型或图纸
```javascript
<div id="view3d"></div>
```
## 模型初始化
```javascript
var options = new BimfaceSDKLoaderConfig();
options.viewToken = viewToken;
BimfaceSDKLoader.load(options, successCallback, failureCallback);

function successCallback() {
// 获取DOM元素
var dom4Show = document.getElementById('view3d');
var webAppConfig = new Glodon.Bimface.Application.WebApplication3DConfig();
webAppConfig.domElement = dom4Show;

// 创建WebApplication
window.app = new Glodon.Bimface.Application.WebApplication3D(webAppConfig);

// 添加待显示的模型
app.addView(viewToken);

// 监听添加view完成的事件
app.addEventListener(Glodon.Bimface.Application.WebApplication3DEvent.ViewAdded, function () {

  // 渲染3D模型
  app.render();

  // 从WebApplication获取viewer3D对象
  window.viewer3D = app.getViewer();
});

};
function failureCallback(error) {
console.log(error);
};

```
## 用到的JSSDK方法
  * 隔离构建
```javascript
viewer3D.isolateComponentsById(arr, Glodon.Bimface.Viewer.IsolateOption.MakeOthersTranslucent);
```

## 注

ps. 该Demo基于react+webpack进行开发打包，如用jquery/Vue实现同上。

参考API：[http://doc.bimface.com/book/js/articles/basic/index.html](http://doc.bimface.com/book/js/articles/basic/index.html)

# 查看示例

[http://bimface.com/example/progress](http://bimface.com/example/progress)
