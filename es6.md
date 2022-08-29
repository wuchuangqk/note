# Module模块

## export导出

### 基本导出

单个导出，导出变量、函数、类

```javascript
export const name = 'tom'
export function sai() {}
export class Person {}
```

批量导出，注意这里的大括号`{}`不是对象的意思

```javascript
export { name, sai, Person }
```

给批量导出的变量重命名，使用`as`关键字，变量可以重命名多次（指向的都是同一个变量）

```js
export { name as catName, sai as say, name as dogName }
```

批量导出可以有多个，这意味着可以将多个模块暴露的变量汇总到一个模块里

```js
// db.js
export const db1 = 10
export const db2 = 10
// user.js
export const user = []

// index.js
export {db1,db2} from './db.js'
export {user} from './user.js'

// 使用时
import {db1,db2,user} from './index.js'
```



错误写法

```js
// 直接输出值
export 1

// 虽然输出val，实际还是输出的值1
const val = 1
export val
```



### 默认导出 export default

添加一个默认导出，使用者无需知道变量名是什么

```js
export default a = 10

// 使用时，不知道变量名也可用使用模块里的属性
import example from './example.js'
console.log(example) // 10
```

默认导出函数

```js
export default function test() {}

// 这时候，example就是函数了
import example from './example.js'
example()
```

export default 作为默认输出，一个模块里只能有一个

export default 可以和普通export 共同使用，这里的`_`是默认导出

```js
import _, { each, forEach } from 'lodash';
```



因为`export default`命令其实只是输出一个叫做`default`的变量，所以它后面不能跟变量声明语句。

```js
// 正确
export var a = 1;

// 正确
var a = 1;
export default a;

// 错误
export default var a = 1;
```

上面代码中，`export default a`的含义是将变量`a`的值赋给变量`default`。所以，最后一种写法会报错。

同样地，因为`export default`命令的本质是将后面的值，赋给`default`变量，所以可以直接将一个值写在`export default`之后。

```js
// 正确
export default 42;

// 报错
export 42;
```



### export default 和 export的转换

本质上，`export default`就是输出一个叫做`default`的变量或方法，然后系统允许你为它取任意名字。

```js
const add = () => {}

// 写法一
export default add

// 写法二，等同写法，把变量作为default变量导出
export { add as default }
```

在使用时，也支持两种方式

```js
// 对应写法一
import example from './example.js'
example() // example 指向 add函数

// 对应写法二，导入default变量，起自定义别名（default变量是不能使用的，必须起别名）
import { default as example } './example.js'
example() // 两者相同
```



## import导入

### 基本导入

注意这里的大括号`{}`既不是对象，也是解构

```js
import { name, sai, Person } from './example.js'
```

导入同样也可以用`as`关键字重命名

```js
import { name as catName } from './example.js'
```

加载的模块只会执行一次

```js
// lodash.js
console.log('loaded')
export const a = 10
export const b = 10

// 多次加载，只会执行一次console.log
import './lodash.js'
import './lodash.js'

// 下面的同理
import { a } from './lodash.js'
import { b } from './lodash.js'
```

### 整体导入 *

相当于把所有变量合并到一个对象上

```js
import { name, sai, Person } from './example.js'
import * as all from './example.js'

console.log(all.name)
console.log(all.sai)
console.log(all.Person)
```



## export 和 import 的复合写法

注意，复合写法只能起到转发的作用，当前模块是不能使用导入的变量的，因为变量实际上没有被导入到当前模块。

```js
export { foo, bar } from 'my_module';

// 可以简单理解为
import { foo, bar } from 'my_module';
export { foo, bar };
// 在当前模块里，foo和bar不可用
```

导出时起别名

```js
export { foo as myFoo } from 'my_module';
```

整体导出

```js
export * from 'my_module';
```

导出默认

```js
export { default } from 'foo';
```

具名改默认

```js
export { es6 as default } from './someModule';

// 等同于
import { es6 } from './someModule';
export default es6;
```

默认改具名

```js
// someModule.js
export { default as es6 } from './someModule';

// middle.js
// 等同于，导入默认的foo变量，然后将其导出，并且起别名
import foo from './someModule'
export { foo as es6 }

// use.js
// 使用时，这个es6就是someModule的默认输出
import { es6 } from 'middle.js'
```

