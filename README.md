#mapv分析：(API解读)
##一、Common ##1 util 工具类 
###1.1 isPlainObject: 参数：obj 功能：判断一个对象是否是常规的对象，即不是dom,或者含有构造函数的对象，一般是我们new 出来的或者是通过{}造出来的对象 
###1.2 extend: 参数：destination,source 功能：可以实现一个对象的浅复制或拓展目标对象 
###1.3 copy： 参数：obj
功能：浅copy一个对象 
###1.4 inherits： 参数：subClass,supperClass
功能：原型链继承 
###1.5 addCssByStyle： 参数：cssString--css样式代码
功能：向页面动态写入css样式 
###1.6 getGeoCenter: 参数：geo--带地理信息(经纬度)的数组如：[[120.34324,29.2342],[121.41432,29.342]...]
功能：获取地理位置的几何中心点 
###1.7 getPixelRatio： 参数：context
功能：获取(设置)设备浏览器的window.devicePixelRatio(目标设备选择几个像素点去渲染图片的一个像素点) 
##2 MVCObject类：

MVCObject类是mapv的核心类，它实现了mapv数据(对象)绑定，动态获取(设置属性)等特性。

###2.1 set: 参数：key,value
功能：动态设置属性并更新到页面上 
###2.2 get: 参数:key
功能:从依赖链中获取对应key的值 
###2.3 notify: 参数:key
功能:手动触发对应key的事件传播 
###2.4 setValues: 参数:values
功能:为对象动态设置多个属性 
###2.5 setOptions: 同2.4 
###2.6 bindTo: 参数:key(当前对象上的key),target(目标对象),targetKey(目标对象上的key),noNotify(是否触发)
功能:将当前对象上的一个key与目标对象的targetKey建立监听和广播关系 
###2.7 unbind: 参数:key
功能:解除当前对象上key与目标对象的监听 
###2.8 unbindAll: 功能:解除当前对象上所有与目标对象的监听 ###2.9 initOptions: 参数:options
功能:初始化options选项 ##3 Class类:
该类主要定义了事件的事件的监听器,移除事件和派发事件

###3.1 addEventListener: 参数:type(事件类型),handler(事件处理器)
功能:添加自定义事件和对应的处理函数 

###3.2 removeEventListener: 参数:type,handler(同3.1)
功能:移除自定义事件和对应的处理函数 

###3.3 dispatchEvent: 参数:type,handler(同3.1)
功能:派发自定义事件,使绑定到事件上的函数都触发 

##4 DataRange 类: 构造函数参数:layer,mapv主件对象
DataRange 和 layer的 'data' 绑定 该类的主要作用是作为图例项确定值的显示范围和显示方式与类型 
##5 Animation 类: 定义动画类 

##6 Mapv:主类 
###6.1 构造函数: 参数:{ map:map, //当前地图对象 drawTypeControl:false, drawTypeControlOptions:{} } 

##7 CanvasLayer类:
说明:该类构建了一个一直覆盖在当前视野的canvas对象,并且该类继承自BMap.Overlay类,当地图缩放或移动时就会触发draw方法重绘当前canvas.这也是mapv根据地图变化而实时渲染而不加监听的魅力所在。

##8 Layer 类:
说明:这是跟绘制图形最为接近的控制类了,该类向用户提供,接受配置

构造参数说明:
mapv:当前的mapv对象
map:当前地图对象
data:当前要展示的数据,数据格式为[{lng:lng,lat:lat,count:count}...]
dataType:数据类型,为point或polygon
animationOptions:动画配置
coordType:地图坐标类型,取值为bd09ll、bd09mc、gcj02、wgs84
drawType:绘制类型,为mapv所提供的类型
animation:是否显示动画
dataRangeControl:是否显示图例项 
##9 DataRangeControl:
图例项类
###9.1 Drawer 类: 
该类是所有绘制类的父类，承担了绘制的责任
