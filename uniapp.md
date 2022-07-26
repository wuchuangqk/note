- 不支持`*`通配符
- body的元素选择器用page，div、ul、li改为view，span改为text，a改为navigator，img改为image
- app端单文件组件style标签默认不加scoped，需要手动添加，pc端自带scoped
- 小程序和app的js运行在jscore而不是浏览器，所以不支持dom和bom，如：document、xhr、cookie、window、location、localstorage等
- 不要在引用组件的地方在组件属性上直接写 style="xx"，要在组件内部写样式
- 小程序不支持v-html
- 小程序要求连接的网址都要配白名单
- uniapp默认css单位是`rpx`
- `--window-top`，`--window-bottom`，```bottom: var(--window-bottom)```