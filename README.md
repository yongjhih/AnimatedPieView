# AnimatedPieView

#### // 一个好吃的甜甜圈？请问客官要啥口味捏-V- 
#### // [English Ver](https://github.com/razerdp/AnimatedPieView/blob/master/README_EN.md)（ps:请别对我的英文有多大信心）

[![jcenter](https://api.bintray.com/packages/razerdp/maven/AnimatedPieView/images/download.svg)](https://bintray.com/razerdp/maven/AnimatedPieView/_latestVersion)
[![license](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](https://github.com/razerdp/AnimatedPieView/blob/master/LICENSE)
[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-AnimatedPieView-brightgreen.svg?style=flat)](https://android-arsenal.com/details/1/6507)
[![Api](https://img.shields.io/badge/Api-14%2B-green.svg)](https://img.shields.io/badge/Api-14%2B-green.svg)
[![Author](https://img.shields.io/badge/Author-razerdp-blue.svg)](https://github.com/razerdp) 

### 因为一些历史原因~~（撸代码时对于硬件加速的使用有点随意。。。）~~导致了重大性能问题，强烈建议更新到1.1.3或以上版本

--- 

### 开发进度 （更新日志->[日志](https://github.com/razerdp/AnimatedPieView/blob/master/UPDATE_LOG.md)）：
  > 如果您有别的需求，可以提交您的issue哦，当然，也可以直接修改源码-V-
  -~~允许alpha突出选中的甜甜圈~~-
  - ~~允许甜甜圈之间含有间隔~~
  - ~~文字自适应点击动画位置~~
  - ~~文字描述动画~~
  - ~~有文字描述的甜甜圈~~
  - ~~点击事件回调的甜甜圈~~
  - ~~点击动画的甜甜圈~~
  - ~~可以点击的甜甜圈~~
  - ~~可以变成大饼的甜甜圈~~
  - ~~动画长大的甜甜圈~~

### 主要功能：
| 描述        | 方法    |  预览  |
| --------   | :-----   | ---- |
| 动画生长        | --      |   ![pie_animation](https://github.com/razerdp/AnimatedPieView/blob/master/art/pie_animation.gif)    |
| 饼图/甜甜圈转换        | setDrawStrokeOnly(boolean)      |   ![pie_switch](https://github.com/razerdp/AnimatedPieView/blob/master/art/pie_switch.gif)    |
| 角度间隙       | setSplitAngle(float)      |   ![pie_split_angle](https://github.com/razerdp/AnimatedPieView/blob/master/art/pie_split_angle.gif)    |
| 绘制文字       | setDrawText(true)      |   ![pie_with_text](https://github.com/razerdp/AnimatedPieView/blob/master/art/pie_with_text.gif)    |
| 点击效果       | setCanTouch(true) / setOnPieSelectListener()    |   ![pie_click_effect](https://github.com/razerdp/AnimatedPieView/blob/master/art/pie_click_effect.gif)    |
| 焦点甜甜圈效果 (反向)      | setFocusAlphaType(<br>AnimatedPieViewConfig.FOCUS_WITH_ALPHA_REV,150<br>)    |   ![pie_click_with_focus_alpha_type_rev](https://github.com/razerdp/AnimatedPieView/blob/master/art/pie_click_with_focus_alpha_type_rev.gif)    |
| 焦点甜甜圈效果       | setFocusAlphaType(<br>AnimatedPieViewConfig.FOCUS_WITH_ALPHA,150<br>)    |   ![pie_click_with_focus_alpha_type](https://github.com/razerdp/AnimatedPieView/blob/master/art/pie_click_with_focus_alpha_type.gif)    |

### 依赖

添加依赖（请把{latestVersion}替换成上面的jcenter标签所示版本）
```xml
	dependencies {
	        compile 'com.github.razerdp:AnimatedPieView:{latestVersion}'
	}
```

#### 基本使用方式（简单的超乎想像）：

```java
        AnimatedPieView mAnimatedPieView = findViewById(R.id.animatedPieView);
        AnimatedPieViewConfig config = new AnimatedPieViewConfig();
        config.setStartAngle(-90)// 起始角度偏移
                .addData(new SimplePieInfo(30, getColor("FFC5FF8C"), "这是第一段"))//数据（实现IPieInfo接口的bean）
                .addData(new SimplePieInfo(18.0f, getColor("FFFFD28C"), "这是第二段"))
                ...(尽管addData吧)
                .setDuration(2000)// 持续时间
        mAnimatedPieView.applyConfig(config);
        mAnimatedPieView.start();
```

### 进阶用法（所有配置都在config，and...相信我，我提供大多数配置，但日常用到的，其实不多哈哈）：
```java
        AnimatedPieViewConfig mConfig=mAnimatedPieView.getConfig();
        mConfig.setTouchAnimation(true)// 点击事件是否播放浮现动画/回退动画（默认true）
                        .addData(IPieInfo info, boolean autoDesc)// 添加数据，autoDesc：是否自动补充描述？（百分比）
                        .setTouchExpandAngle(15f)// 点击后圆弧/扇形扩展的角度
                        .setTouchShadowRadius(18f)// 点击后的阴影扩散范围
                        .setTouchScaleUpDuration(500)// 点击浮现动画时间
                        .setTouchScaleDownDuration(500)// 上一个浮现的圆弧回退的动画时间
                        .setTouchScaleSize(15)// 点击后扇形放大数值,，只对饼图有效
                        .setDrawStrokeOnly(true)// 是否只画圆弧【甜甜圈哈哈】，否则画扇形（默认true）
                        .setStrokeWidth(15)// 圆弧（甜甜圈）宽度
                        .setDuration(2500)// 动画时间
                        .setStartAngle(-90f)// 开始的角度
                        .setOnPieSelectListener(new OnPieSelectListener<IPieInfo>())//点击事件
                        .setDrawText(true)// 是否绘制文字描述
                        .setTextSize(12)// 绘制的文字大小
                        .getTextMarginLine(8)// 绘制文字与描述线的距离
                        .setPieRadiusScale(0.8f)// 甜甜圈半径占比
                        .setTextPointRadius(2)// 设置描述文字的开始小点的大小
                        .setTextLineStrokeWidth(4)// 设置描述文字的指示线宽度
                        .setTextLineTransitionLength(8)// 设置描述文字的指示线折角处长度
                        .setTextLineStartMargin(8)// 设置描述文字的指示线开始距离外圆半径的大小
                        .setDirectText(true)// 设置描述文字是否统一方向 【
                            -true：文字将会在描述线上绘制
                            -false：文字在1、2象限部分绘制在线的上方，在3、4象限绘制在线的下方
                        】
                        .setCanTouch(true)// 是否允许甜甜圈点击放大
                        .setSplitAngle(1)// 甜甜圈间隙角度
                        .setFocusAlphaType(AnimatedPieViewConfig.FOCUS_WITH_ALPHA_REV,150)// 焦点甜甜圈的alpha表现形态及alpha削减值
                        .setStrokePaintCap(Paint.Cap.ROUND)// 笔刷的样式
                        .setConfig(new AnimatedPieViewConfig());// 配置（这里的new只是演示哦，可不要学我例子这里直接塞进一个新的config，否则上面的设置都浪费了）
```

---

### 打赏（您的支持是我维护的动力-V-愿意的话，金额随意）
![wechat](https://github.com/razerdp/AnimatedPieView/blob/master/art/wechat.jpg)

### 控件思路【按思路顺序更新】
 - [自定义控件——弄个甜甜圈吧（1）： 起源](http://www.jianshu.com/p/b2a2d82e107e)
 - [自定义控件——弄个甜甜圈吧（2）： 搭建](http://www.jianshu.com/p/562c525ff927)
 - [自定义控件——弄个甜甜圈吧（3）： 动画篇【生长动画】](http://www.jianshu.com/p/f7842a97cb3e)
 - 编写中...

### LICENSE
Apache-2.0
   
   

   



