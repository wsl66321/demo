## 文件结构 及 Json结构说明
### 文件结构：
1. audios 音效文件夹

```	
题目播报语音 audio_question_km3_{index}.mp3
```
	
2. image 界面所用的图片
3. json 配置文件
```

+ control	控制-冲突处理文件夹
+ render	渲染文件夹
- practice.json	练习json
- guide.json	基础步骤与提示json
- region.json	各区域布局json
```

4. 跟包 json (与外层灯光考试、灯光视频共用) 		

```
- exam.json	考试列表json
- practice.json	练习json
```


### Json结构：
control：
```
  {
    "condition": [
      {
        "region": "透视区域-重置",
        "slot": 1
      }
    ],
    "reset": [
      {
        "region": "透视区域-右转灯",
        "slot": 0
      },
      {
        "region": "透视区域-远光灯",
        "slot": 0
      },
      {
        "region": "透视区域-左转灯",
        "slot": 0
      },
      {
        "region": "透视区域-闪光灯",
        "slot": 0
      }
    ]
  }
```

解释：
> 当满足condition中所有条件时，把reset中所有region字段的状态改为slot


render 区域：
```
  {
    "condition": [
      {
        "region": "仪表盘区域-左转灯",
        "slot": 1
      }
    ],
    "resourceList": [
      {
        "region": "仪表盘区域-左转灯",
        "resource": "仪表盘-转向灯-左.png"
      }
    ]
  }
```

解释：
> 当满足condition中所有条件时，把resourceList中所有region字段的区域图片改为resource

render 动画/声音：
```
  {
    "condition": [
      {
        "region": "透视区域-右转灯",
        "slot": 1
      },
      {
        "region": "应急按钮区域",
        "slot": 0
      }
    ],
    "resourceList": [
      {
        "region": "仪表盘区域-右转灯",
        "resource": "type=alpha,pivotX=1,pivotY=1,fromValue=0,toValue=1,duration=700,repeat=-1",
        "resourceType": "animation"
      }
    ]
  }
```

解释：
> 当满足condition中所有条件时，把resourceList中所有region字段的区域执行动画/声音

> type : alpha透明度、rotate旋转、scale缩放； 

> pivotX、pivotY : 动画中心点坐标

> fromValue、toValue :变量初始值与结束值

> duration : 动画持续时间 ms

> repeat : 1:仅一次， -1:循环播放，-2:停止循环

> name : 文件名

> resourceType : audio: 音效，animation : 动画


exam.json
```
  {
    "name": "灯光模拟1",
    "data": "1,2,11,18,16,12,21"
  }
```
解释：
> name : 模拟考试标题

> data : 所包含的题目，根据索引去practoce.json中查找题目


practoce.json
```
  {
    "index": 3,
    "question": "夜间通过没有交通信号灯控制的路口",
    "answer": "近光灯、远近光交替两次。(部分城市三次)",
    "video": "https://sp.mnks.cn/km3/yjdgmn/jieda_14.mp4",
    "guide": "2,8,8"
  }
```

解释：
> index 题目索引

> question 题目

> answer 答案

> video 视频解析链接

> guide 基础操作索引，根据索引去guide.json中查找操作

guide.json
```
  {
    "index": 1,
    "tip": "点击转动至此处，开启示廓灯",
    "region": "旋钮区域-示廓灯",
    "slot": 1
  }

```
解释：
> index 题目索引

> tip 提示内容

> region 区域状态

> slot 区域目标状态

region.json

```

 {
    "name": "出风口区域",
    "width": "274",
    "height": "139",
    "left": "460",
    "top": "213",
    "subRegion": [
      {
        "name": "应急按钮区域",
        "width": "50",
        "height": "40",
        "alignment": "center",
        "left": "0",
        "top": "0",
        "action": {
          "type": "click"
        }
      }
      ]
  }

```
解释：
> name 区域名

> width 区域宽度

> height 区域高度

> left 距屏幕左边距离

> top 距屏幕顶部距离

> subRegion 子区域

>> name 子区域名

>> slot 初始状态

>> slotSize 状态个数

>> alignment 对齐方式  如果有次字段且字段值为“center”时 区域在父区域居中，否则根据left、top定位

>> width 子区域宽度

>> height 子区域高度

>> left 距父区域左边距离

>> top 距父区域顶部距离

>> action 活动 type：stuck：点击时把该区域状态置为1、touch：手指按下时把该区域状态置为1，松开时置为0、click：点击时切换该区域状态、slide：滑动。   deltaX、deltaY：触发滑动时XY的增量


车型接口：https://rapi.mnks.cn/data/banner/app_json_com.runbey.ybjk_car_light_config.json

```
{
  "carId": "1",
  "title": "新捷达灯光操作",
  "desc": "本套灯光操作适用于2013-2019年款大众捷达。",
  "cover": "https://sucimg.itc.cn/sblog/j25a277c8e121ff6478577cf9e56f82e6",
  "tryTime": "20",
  "time": "05:33",
  "url": "https://sp.mnks.cn/km3/yjdgmn/xinjieda.mp4",
  "train": {
    "icon": "https://sucimg.itc.cn/sblog/j8a7193610b6688c94e13ab41e3327611",
    "zip": "https://wycbd.mnks.cn/ybjk/light/car/newjieda.zip",
    "carName": "新捷达",
    "version": ""
  }
}
```
解释：
> carId 外部使用

> title 外部使用

> desc 外部使用

> cover 外部使用

> tryTime 外部使用

> time 外部使用

> url 视频讲解链接

> train

>> icon 车型列表icon图标url

>> zip 车型素材下载链接 zip密码： com.runbey   取包名截出密码，不能用明文

>> carName 车型名

>> version 版本号，纯数字，当该字段为空时，所有版本均展示，当该字段有值，则>= 该版本展示 ，仅配置一个版本号即可 exp: "70"


## UI界面规则

以375×667为基准，其余屏幕尺寸手机进行适配：


适配规则

①背景图：等比填充背景，左右居中显示

②车架：拉伸铺满背景

③内饰：以基准图摆放，其它屏幕尺寸不动元素大小，横向纵向间距按真实尺寸等比调整（以某一元素为基准的元素，如仪表盘内的表盘、灯光等，整体跟着仪表盘走，内部间距不要动）

375* / 基础图纵向间距 = 真实纵向尺寸 / 真实间距

> *纵向取375，横向取667

## 区域
根据region.json按需展示区域，区域图层排序、所需json如下
1. 背景区域

```
图片：json/render/渲染-背景区域.json
```

2. 车架区域

```
图片：json/render/渲染-背景区域.json
```

3. 拨杆区域

```
图片：json/render/渲染-拨杆区域.json
声音：json/render/渲染-声音.json
```

4. 出风口区域

```
图片：json/render/渲染-应急按钮区域.json
声音：json/render/渲染-声音-应急按钮.json
```

5. 后雾灯区域

```
图片：json/render/渲染-后雾灯.json
```

6. 仪表盘区域

```
图片：json/render/渲染-仪表盘区域.json
控制：
	json/control/控制-仪表盘-远光灯.json
	json/control/控制-仪表盘-转向灯.json
	json/control/控制-仪表盘-近光灯+雾灯光+示宽灯.json
	json/control/控制-拨杆区域.json
```

7. 透视区域

```
图片：json/render/渲染-透视区域.json
声音：json/render/渲染-声音-透视区域.json
冲突处理：json/control/控制-透视区域-冲突处理.json
```

8. 旋钮区域

```
图片：json/render/控制-旋钮区域.json
声音：json/render/渲染-声音-旋钮区域.json
```

解释：
> 图片 根据json内容查找要展示的图片

> 声音 按键音效

> 冲突处理、控制 根据某些状态去设置其他状态

> 仪表盘控制json数量不固定，存在几个读几个

### 部分算法
#### 检查答案
view.LightingView.checkAnswer(PracticeBean practiceBean)


```
//关闭所有灯光
if(guide == ""){
  if(透视区域-重置 == 1 && 旋钮区域-关闭 == 1 && 应急按钮区域 == 0 && 拨杆区域-上 == 0 && 拨杆区域-下 == 0){
    return true;
  }else{
    return false;
  }
}

//1.需要的打开的均已打开
if(guide中需要打开的状态都已打开){
  if(guide包含"远近光灯切换"){
    if(透视区域-闪光灯操作次数!=4){		//开-关-开-关 共四次
      return false;
    }
  }
}else{
  return false;
}

//2.没有要求的均处于关闭状态
for(所有的状态名s){
  if(s是题目中要操作的 || s == "透视区域-重置" || s == "旋钮区域-关闭"){
    continue;
  }else{
    if(s的状态处于开){
      return false;
    }
  }
}

//3.没进行多余操作
for(本题过程中所做的操作b){
  if(b是题目中要操作的 || b == "透视区域-重置" || b == "旋钮区域-关闭" || b包含 "拨杆区域"){
    continue;
  }else{
    if(b的操作时打开操作){
      return false;
    }
  }
}

return true;
```
#### 冲突处理
view.WidgetView.reset(String name)
```
for(本区域中所有冲突处理 b){
  boolean 包含 = false, 相等 = true;
  for(b中所有条件s){
    if(状态 != 条件s){
      相等 = false;
      break;
    }
    if(name == 条件s.region){
      包含 = false;
    }
  }
  if(包含 && 相等){
    for(b中所要重置的状态 r){
      r.region状态 = r.slot;
      发送通知;
    }
  }
}
```

#### 图片查找
共包含2中图片查找 1:单状态就可确定图片 例如雾灯；2.多状态确定图片：例如透视区域和旋钮区域

##### 图片查找1
算法同上方冲突处理，发送通知所出的代码块改为设置图片操作

##### 图片查找2
初始化时用k-v的方式保存在聚合中，k是生成的code，v是图片
查找是根据code查找图片
生成code举例：
view.TsView.getCode(Map<String, Integer> map)

```
long slot = 0;
slot = 状态1;
slot = slot * 10;
slot = slot + 状态2;
slot = slot * 10;
slot = slot + 状态3;
slot = slot * 10;
slot = slot + 状态4;
slot = slot * 10;
slot = slot + 状态5;
return slot;
```

如下json保存为：k：10100 v：透视开关-闪光-右转.png

保存时 状态1为 透视区域-右转灯 的slot：1

查找时 状态1为当前 透视区域-右转灯 的状态
```
  {
    "condition": [
      {
        "region": "透视区域-右转灯",
        "slot": 1
      },
      {
        "region": "透视区域-左转灯",
        "slot": 0
      },
      {
        "region": "透视区域-闪光灯",
        "slot": 1
      },
      {
        "region": "透视区域-远光灯",
        "slot": 0
      },
      {
        "region": "透视区域-重置",
        "slot": 0
      }
    ],
    "resourceList": [
      {
        "region": "透视区域",
        "resource": "透视开关-闪光-右转.png"
      }
    ]
  }
```



## Android 

### manager.AudioManager
音效管理类

- +playShortAudio(Context context, String path)	播放单次音效
- +playQuestionAudio(Context context, String path, final MediaPlayer.OnCompletionListener completionListener)	播放题目音效
- +playLongAudio(Context context, String path)	播放循环音效
- -initAudio(Context context, String path, MediaPlayer mediaPlayer)	初始化音效MediaPlayer对象
- +stopQuestionAudio()	停止播放题目音效
- +playRightAudio(Context context)	播放操作正确音效
- +playErrorAudio(Context context)	播放操作错误音效
- +pauseAudio() 	暂停循环播放音效
- +restartAudio()	重新开始播放循环音效
- +stopLongAudio() 停止播放循环音效
- +playAudio(Context context, List<RenderBean.ResourceList> resourceList)	根据resourceList播放音效
- +destroy()	停止所有音效的播放并释放资源

### manager.MediaPlayerManager
视频管理类
- +playMediaPlayer(String url) 播放视频
- -initMediaPlayer()	初始化
- +restart()	继续播放
- +pause()	暂停播放
- +stop()	停止播放
- +destroy()	释放资源

### view.WidgetView	
各区域组件的父类
- init(RegionBean data)	设置区域大小与位置
- setImg(String path)	设置区域的图片
- initAudio()	初始化音效json为 "json/render/渲染-声音-" + widgetName + ".json"
- initAudio(String file)	根据file读取音效json
- playAudio(String name)	播放音效 name:区域名
- reset(String name)	冲突处理
- callBack(String name, int slot)	Tip提示回调
- showTip(String name, String tip, int slot, TipCallBack callBack) 展示提示tip

### view.LightingView
模拟灯光区域
- -initView() 根据region.json解析需要展示的区域并初始化
- -checkAnswer(PracticeBean practiceBean):boolean 检查答案
- -showTime(final int time, final PracticeBean practiceBean)	显示做题倒计时与其他做题信息
- -doGuide(final List<Integer> list, final int index) 	指引教程 list：指引列表 ，index：当前指引下标
- -showTip()	展示提示

### view.TsView
透视区域
- +init(RegionBean data, LightingView parent) 根据data初始化、绘制区域、添加subRegion中的区域并添加点击监听
- -getCode(Map<String, Integer> map):long: 根据状态map生成key映射ResourceList对象查找要显示的图片

