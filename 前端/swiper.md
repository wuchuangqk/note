# 安装

```shell
npm i swiper
```



# 导入样式文件

`index.scss`

核心样式文件

```typescript
@import "swiper/css";
```

可选组件样式文件

- 分页

```typescript
@import "swiper/css/pagination";
```



# 安装组件

全局安装

导入要安装的组件，传入到`use`方法的数组参数里，`Swiper.use`必须要在main.ts里执行

```typescript
import Swiper, { Pagination } from "swiper";
Swiper.use([Pagination]);
```

