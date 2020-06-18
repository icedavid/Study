cocos-2dx 3.17 学习笔记

### Director（导演）

+ 作用

  + 控制场景切换
  + cocos2dx中的导航器，指挥每一个元素的操作及作用

+ 使用方法

  ​	使用getInstance()来获取

### Scheduler（调度器）

+ 类别

  + 默认调度器：scheduleUpdate()
  + 自定义调度器：schedule(SEL_SCHEDULE selector, float interval, unsigned int repeat, float delay)
  + 单词调度器：scheduleOnce(SEL_SCHEDULE selector, float delay)

+ 默认调度器

  + 作用：对游戏过程中的逻辑进行判断
  + 使用方法
    + 重载Node的刷新时间update方法，使其在每一帧绘制前都会调用一次
    + 需要停止使用，方法unschedulerUpdate()

+ 自定义调度器

  + 作用：减少逻辑检测次数，自定义检测周期（自定义时间至少为2帧间隔，也就是大于0.1s）

  + 使用方法

    + ```
      schedule(SEL_SCHEDULE selector, float interval, unsigned int repeat, float delay)
      ```

      + 第一个参数selector即为你要添加的事件函数
      + 第二个参数interval为事件触发时间间隔
      + 第三个参数repeat为触发一次事件后还会触发的次数，默认值为kRepeatForever，表示无限触发次数
      + 第四个参数delay表示第一次触发之前的延时

    + 取消调度器：unschedule(SEL_SCHEDULE selector, float delay)

+ 单次调度器

  + 作用：只触发一次逻辑检测
  + 使用方法
    + scheduleOnce(SEL_SCHEDULE selector, float interval);
    + 取消调度器：unschedule(SEL_SCHEDULE selector, float delay)

### FileUtils（文件管理）

+ 作用：统一文件CRUD操作

+ 使用方法

  + 检查文件是否存在

  ```
  cc.FileUtils:getInstance():isFileExist(path)
  ```

  + 读取文件

  ```
  cc.FileUtils:getInstance():getStringFromFile(path)
  ```

### Scene（场景）

+ 作用：作为游戏制作中的舞台场地

+ 使用方法

  + cc.Scene

  + 创建普通场景

    ```
    display.newScene(name)
    ```

  + 创建带物理引擎的场景

    ```
    display.newPhysicsScene(name)
    ```

  + 与导演相关的几个方法

    ```
    shareDirector:runWithScene(newScene)
    ```

    + 运行第一个场景，主程序第一次启动主场景时调用

    ```
    shareDirector:pushScene(scene)
    ```

    + 将当前运行的场景压入场景栈中，再将传入的scene场景设置为当前运行场景

    ```
    shareDirector:replaceScene(newScene)
    ```

    + 传入的newScene替换当前场景，当前场景被释放

    ```
    shareDirector:popScene()
    ```

    场景栈弹出栈顶场景并释放，运行新的栈顶场景。如果栈顶为空，结束应用。与PushScene结对使用。

### Node（节点）

+ 作用：cocos2dx中使用层级管理各个节点对象，Node是其根类

+ 使用方法

  + 创建节点

    ```
    cc.Node:create()
    ```

  + 增加新子节点

    ```
    node:->addChild(childNode, 0, 123)
    ```

    + 第二个参数Z轴绘制顺序

    + 第三个参数是标签

  + 通过标签删除子节点，并停止所有该节点上的一切动作。

    ```
    node:removeChildByTag(123, true) 
    ```

  + 删除childNode节点。并停止所有该子节点上的一切动作。

    ```
    node:removeChild(childNode, true)
    ```

  + 删除node节点的所有子节点，并停止这些子节点上的一切动作。

    ```
    node:removeAllChildrenWithCleanup(true)
    ```

  + 从父节点删除node节点，并停止所有该节点上的一切动作。

    ```
    node:removeFromParentAndCleanup(true)
    ```

+ 属性

  + position

    ​		position(位置)属性是Node对象的实际位置。position属性往往还要配合使用anchorPoint（锚点）属性。

  + anchorPoint

    ​		为了将一个Node对象（标准矩形图形）精准的放置在屏幕某一个位置上，需要设置该矩形的锚点，anchorPoint是相对于position的比例，默认是(0.5,0.5)。

### Sprite（精灵）

+ 作用：游戏中的操作对象以及节点对象

+ 使用方法

  + 创建精灵对象

    ```
    cc.Sprite:create ()
    ```

  + 指定图片创建精灵

    ```
    cc.Sprite:create (filename)
    ```

  + 指定图片和裁剪的矩形区域来创建精灵

    ```
    cc.Sprite:create (filename, rect)
    ```

  + 指定纹理创建精灵

    ```
    cc.Sprite:createWithTexture (texture)
    ```

  + 指定纹理和裁剪的矩形区域来创建精灵，第三个参数是否旋转纹理，默认不旋转

    ```
    cc.Sprite:createWithTexture (texture, rect, rotated=false)
    ```

  + 通过一个精灵帧对象创建另一个精灵对象

    ```
    cc.Sprite:createWithSpriteFrame (pSpriteFrame)
    ```

  + 通过指定帧缓存中精灵帧名创建精灵对象

    ```
    cc.Sprite:createWithSpriteFrameName (spriteFrameName)
    ```

### *Layer（层）

+ 作用： 将场景中的不同组成部分分层化管理，各组件之间互不干扰

+ 使用方法：

   

### Action

+ 作用：制作动作

+ 使用方法

  