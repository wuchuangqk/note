# 添加pinia
安装
```shell
npm install pinia
```

集成到vue

```typescript
// main.ts
import { createApp } from 'vue'
import { createPinia } from 'pinia'
import App from './App.vue'

const pinia = createPinia() // 创建一个 pinia 实例(根 store)
const app = createApp(App)

app.use(pinia)
app.mount('#app')
```



# 创建store

option语法

```typescript
// stores/counter.js
import { defineStore } from 'pinia'

export const useCounterStore = defineStore('counter', {
  state: () => {
    return { count: 0 }
  },
  // 也可以这样定义
  // state: () => ({ count: 0 })
  actions: {
    increment() {
      this.count++
    },
  },
})
```
组合式语法

```typescript
// stores/counter.js
import { defineStore } from 'pinia'

export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  function increment() {
    count.value++
  }

  return { count, increment }
})
```



# 三种改变状态的方式

```typescript
// App.vue
import { useCounterStore } from '@/stores/counter'

export default {
  setup() {
    const counter = useCounterStore()

    counter.count++ // 第一种，直接调用
    
    counter.$patch({ count: counter.count + 1 }) // 第二种，调用$patch，传一个对象，可以同时更改多个状态
    
    counter.increment() // 第三种，使用action
  },
}
```

