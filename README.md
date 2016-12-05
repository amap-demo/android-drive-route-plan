# android-drive-route-plan
驾车路径规划示例
## 前述 ##
- [高德官网申请Key](http://lbs.amap.com/dev/#/).
- 阅读
  [地图SDK参考手册](http://a.amap.com/lbs/static/unzip/Android_Map_Doc/index.html). 
- 工程基于高德3D地图实现

## 使用方法##
###1:配置搭建AndroidSDK工程###
- [Android Studio工程搭建方法](http://lbs.amap.com/api/android-sdk/guide/creat-project/android-studio-creat-project/#add-jars).
- [通过maven库引入SDK方法](http://lbsbbs.amap.com/forum.php?mod=viewthread&tid=18786).

## 扫一扫安装##

 ![Screenshot](https://github.com/amap-demo/android-drive-route-plan/blob/master/resource/download.png)

## 示例效果##

 - overlay效果展示
 
 ![Screenshot](https://github.com/amap-demo/android-drive-route-plan/blob/master/resource/Screenshot_overlay.png)

 - 列表效果展示
 
 ![Screenshot](https://github.com/amap-demo/android-drive-route-plan/blob/master/resource/Screenshot_list.png)
 
 ## 核心类/接口 ##
| 类    | 接口  | 说明   | 版本  |
| -----|:-----:|:-----:|:-----:|
|RouteSearch|	calculateDriveRouteAsyn()|根据指定的参数计算驾车路径、异步方法|V2.1.0|
|RouteSearch|onDriveRouteSearched()|驾车路径规划结果的回调方法|V2.1.0|
 
  ## 核心难点 ##
  - 构造路径规划类
  
  ```java
        mRouteSearch = new RouteSearch(this);
        mRouteSearch.setRouteSearchListener(this);
  ```
  
  -发起路径规划异步请求
   
  ```java
    mRouteSearch.calculateDriveRouteAsyn(query)
  ```
  
  - 将驾车路径规划结果用overlay在地图展现
  
  ```java
        DrivingRouteOverlay drivingRouteOverlay = new DrivingRouteOverlay(
                mContext, aMap, drivePath,
                mDriveRouteResult.getStartPos(),
                mDriveRouteResult.getTargetPos(), null);
        drivingRouteOverlay.setNodeIconVisibility(false);//设置节点marker是否显示
        drivingRouteOverlay.setIsColorfulline(true);//是否用颜色展示交通拥堵情况，默认true
        drivingRouteOverlay.removeFromMap();
        drivingRouteOverlay.addToMap();
        drivingRouteOverlay.zoomToSpan();
  ```
