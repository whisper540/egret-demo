改项目为白鹭官方案例，是egret的eui项目，白鹭进行游戏开发为三种模式，
一，直接代码编辑所有游戏场景；
二，代码+eui样式控件；
三，lakeshore方式，这种方式很类似flash的直接拖拽功能实现游戏开发，比较简单容易上手。

## EUI游戏应用示例

示例展示了EUI在游戏开发中的使用方法。

本示例包含玩家、英雄、物品、关于等多个页面，每个页面有独立的exml皮肤。所有游戏涉及的exml皮肤均处于项目的 "resource/custom_skins" 目录下。

在资源加载上，采用分页加载机制，保证最快速度呈现主界面。不同的界面也是在需要时方才启动对应资源的加载，力求保护移动设备玩家的流量消耗。最开始的基本资源加载完成后，每个页面的加载过程，均有通用的百分比loading界面。英雄和物品列表UI由于共用资源较多，资源上作为一个整体，但各自还是作为独立页面处理。具体的处理方式请参看Main.ts代码中的loadPage和pageLoadedHandler方法以及相关的代码。

在涉及组件类别上，不仅包含基本的Image、Button、ToggleButton组件，也包含了较为复杂的List以及控制器滚动的Scroller组件。共包含三个List组件，涵盖了横向滚动和纵向滚动，并且示范了滚动条自定义皮肤以及全程隐藏滚动条等高级技巧，具体做法请自行探索项目源码。每个List的项渲染均准备了单独对应的exml皮肤，同样处于项目的 "resource/custom_skins" 目录下，这些皮肤名称包含IR表示ItemRenderer。

在List内部使用组件时，请注意管理List项中的数据状态。请关注英雄列表界面(HerosUI.ts)列表项中的CheckBox用法，为记录选中状态，专门准备了HerosListIRSkin类，细节请自行研究源码。

在页面切换管理上，4个主要的界面切换按钮加入了严格的锁定逻辑。只有非当前页面对应的按钮才可以相应用户触摸，并且在资源加载过程中，这些按钮都已经锁定。这也是在复杂开发游戏过程中一些需要注意的细节，这些细节往往潜在提升用户体验，并且也很大程度上避免了切换过程中用户操作可能触发的bug。这些按钮的锁定及状态管理均在HomeUI.ts中。

另外，为增强用户体验，还准备了一个Toast类，用于动态呈现文字提示消息。该类完全独立，大家可以摘出来用到自己的项目中。
