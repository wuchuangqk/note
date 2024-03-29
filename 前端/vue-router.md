# 安装

```shell
npm install vue-router@4
```

# 导入依赖

```typescript
import { createRouter, createWebHistory, RouteRecordRaw } from 'vue-router'
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

```typescript
const routes: RouteRecordRaw[] = [
    { path: '/', component: () => import('@/views/index/index.vue') },
    { path: '/detail/:id', component: () => import('@/views/search/detail.vue')},
    {
        path: '/user',
        component: () => import('@/views/user/index.vue'),
        children: [
          { path: 'profile', component: () => import('@/views/user/profile/index.vue') },
        ],
        meta: { authentication: true },
  	},
];
```

# 在vue中安装

```ty
import { router } from '@/router'
const app = createApp(App)
app.use(router)
app.mount('#app')
```

# path和fullPath的区别

path只匹配route数组里定义的path，fullPath还包含查询字符串。例如http://192.168.3.20:8080/#/pages/pickup/pickup?scanType=2，path是/pages/pickup/pickup，fullPath是/pages/pickup/pickup?scanType=2







![image-20230106152225179](./assets/vue-router/image-20230106152225179.png)
