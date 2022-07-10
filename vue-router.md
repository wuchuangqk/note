安装

```shell
npm install vue-router@4
```



导入新的api

```typescript
import {createRouter, createWebHistory} from 'vue-router'
```



创建router，createRouter的参数里，history和routes必传。

history支持两种类型：

- hash模式：createWebHashHistory
- history模式：createWebHistory

```typescript
export const router = createRouter({  
    history: createWebHistory(),  
    routes 
})
```



全局拦截器

```typescript
const interceptor = (to: RouteLocationNormalized, from: RouteLocationNormalized) => {
  // 取消导航
  // return false

  // 导航到指定路由(必须是RouteLocationRaw类型)
  /* const target: RouteLocationRaw = {
    path: '',
    replace: true, // 替换
  } */

  // 不返回或返回true:放行
  // return true
}

// 注册全局路由拦截器
router.beforeEach(interceptor)
```

