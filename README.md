# Cesium量算插件
### [在线体验](http://mapgl.com/shareCode/#/Measure)
gitee：https://gitee.com/caozl1132/CesiumExp-measure
github：https://github.com/gitgitczl/CesiumExp-measure

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
其它： 
qq群：606645466（GIS之家共享交流群）

[更多案例地址](http://mapgl.com/shareCode/)&nbsp;&nbsp;&nbsp; [更多免费数据](http://mapgl.com/shareData/)&nbsp;&nbsp;&nbsp; [开发文档说明](http://mapgl.com/3dapi/)   

[其它源码下载（标绘、量算、动态材质、漫游、地图分析等）](http://mapgl.com/introduce/)



