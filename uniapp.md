- 不支持`*`通配符
- body的元素选择器用page，div、ul、li改为view，span改为text，a改为navigator，img改为image
- app端单文件组件style标签默认不加scoped，需要手动添加，pc端自带scoped
- 小程序和app的js运行在jscore而不是浏览器，所以不支持dom和bom，如：document、xhr、cookie、window、location、localstorage等
- 不要在引用组件的地方在组件属性上直接写 style="xx"，要在组件内部写样式
- 小程序不支持v-html
- 小程序要求连接的网址都要配白名单
- uniapp默认css单位是`rpx`
- `--window-top`，`--window-bottom`，```bottom: var(--window-bottom)```



# 页面栈

生命周期执行顺序：

`onLoad(一次，拿路由参数)` => `onShow(多次，下级页面返回)` => `onReday(一次，操作dom)`

onLoad和onReday只执行一次，onShow会执行多次。

每个页面是一个节点

节点1 -> 节点2 -> 节点3 -> 节点4 -> 节点5

- navigateTo

  - 将to的url对应的页面，创建出一个新的节点，追加到当前节点后
  - 比如列表 -> 详情，详情用navigateTo跳列表，此时会生成三个节点
    - 列表 -> 详情 -> 列表
    - 新创建的列表会触发onLoad事件，这个列表和之前的列表不是同一个
  - 特性：创建(create)
- navigateBack

  - 不指定返回层级时，默认返回层级为1级，即回到上个节点
  - 指针会从当前节点移动到要返回的节点，然后将这个节点之后的所有节点销毁
  - 也就是说，调用了navigateBack，就表示这个页面要出栈
  - 特性：移除(remove)
- redirectTo
  - 特性：替换(replace)
  - 创建新节点追加到末尾，同时移动指针到这个新节点
  - 当前节点会被销毁，等于是把当前节点替换成了新节点
  - 同时具有：
    - navigateTo创建新节点的特性
    - navigateBack销毁自身的特性

- reLaunch
  - 把现存的所有节点全部清空，然后指向创建的新节点
  - 新来的把所有人都赶跑，只留下自己一个人。


## 页面栈例子

现有三个页面：首页，列表页，详情页

- 首页 navigateTo 列表页 navigateTo 详情页
  - 页面生命周期调用顺序：
  - 首页(onHide) -> 列表页(onLoad) -> 列表页(onShow) -> 详情页(onLoad) -> 详情页(onShow)
- 详情页 navigateBack 列表页
  - 页面生命周期调用顺序：
  - 详情页(onUnload) -> 列表页(onShow)
- 详情页 navigateTo  列表页
  - navigateTo 会为列表页创建出一个副本，而不是重复使用。
  - 页面生命周期调用顺序：
  - 详情页(onHide) -> 列表页(新)(onLoad) -> 列表页(新)(onShow) 
- 列表页(新) navigateBack 详情页
  - 页面生命周期调用顺序：
  - 列表页(新)(onUnload) -> 详情页(onShow)
- 列表页 navigateTo  列表页 navigateTo  列表页
  - navigateTo  会以自身为副本创建出新的副本



# 页面传值

## 下级页面向上级页面传值

### 发布订阅

`uni.$on` `uni.$emit`

发布订阅的注意事项

比如页面层级是：页面A -> 页面B -> 页面C

在页面A和页面B的onLoad里都监听了'test'事件

```
// 页面A和页面B都监听test事件
onLoad() {
    uni.$on("test", (value) => {
      console.log("页面A", value); // 页面A
      // console.log("页面B", value); // 页面B
    });
  },
```

那么，当页面C触发'test'事件时，页面A、B都会监听到

```
// 页面C
uni.$emit('test', 'dfsdfsdf')
```

控制台，页面A和B都打印了

```
页面A dfsdfsdf
页面B dfsdfsdf
```

解决办法：上级页面生成唯一的eventName（随机数，时间戳等），作为参数传给下级页面。
