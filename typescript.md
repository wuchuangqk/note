# 配置文件

```json
{
  "compilerOptions": {
    "target": "ESNext",
    "useDefineForClassFields": true,
    "lib": ["DOM", "DOM.Iterable", "ESNext"],
    "allowJs": false,
    "skipLibCheck": true,
    "esModuleInterop": false,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "module": "ESNext",
    "moduleResolution": "Node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx"
  },
  "include": ["src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

- `include`: Array
  - 指定哪些目录下的文件需要编译
- `exclude`: Array
  - 不需要编译的目录，默认值：["node_modules"]

# compilerOptions

- `target`: string 
  - 编译的es版本
- `module`: string 
  - 指定要使用的模块化规范，"commonjs", "amd", "esnext"等
- `lib`: string[] 
  - 指定要使用的库，"dom", "esnext"等
- `allowJs`: boolean 
  - 是否对`.js`文件编译，默认false，只对`.ts`文件编译
- `removeComments`: boolean
  - 是否在编译时移除注释
- `noEmit`: boolean
  - 不生成编译文件（只做检查），默认false
- `strict`: boolean
  - 严格模式



# 泛型

泛型工具类型，TS内置了一些常用的工具类型，来简化TS中的一些常见操作。

## Partial

将所有属性设置为可选

```tsx
interface Props {
    id: string
    children: number[]
}
```

```ts
type PartialProps = Partial<Props>
```

`Partial<Type>`返回属性设置为可选后的类型