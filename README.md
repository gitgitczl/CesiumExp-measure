# Cesium气泡窗插件
## [在线体验](http://mapgl.com/shareCode/#/Measure)
ps：如果可以的话，希望大家能给我个star，好让我有更新下去的动力；
***
实现原理：
其中距离量算的原理是用了Cartesian3提供的distance方法进行了计算；  
面积计算是使用了开源的turf库来进行计算的，此处我只做了空间面积计算，并没有做贴地面积计算，贴地面积计算的原理和空间面积计算一样，只不过贴地时对面做了微分；  
方位角使用了矩阵计算了正北方向的夹角；  
坐标是一个普通的Cartesian3转经纬度；  

***
两种调用方法：  
此处调用和我另一个标绘组件的方法类型，一种是使用MeasureTool这个工具类进行统一控制（推荐使用），另一种是直接new 所需的标绘类。
1、直接通过Tool工具类进行控制：
```
 measureTool = new MeasureTool(viewer);
 // 通过on可以实现状态监听
 measureTool.on("endCreate",function(measureObj){
  // 标绘结束的回调
  ......
 });
```

2、直接new 具体标绘类型，如下进行贴地距离测量：
```
  let mg = new MeasureGroundDistance(viewer);
  mg.starte();
```

***
<iframe src="http://mapgl.com/introduce/" width="100%" height="100%" frameborder="no" style="padding:0"></iframe>

