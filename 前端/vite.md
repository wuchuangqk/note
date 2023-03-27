# 搭建项目环境

```sh
npm init vite@latest
```

```sh
pnpm create vite
```

# lib模式

```js
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";
import dts from 'vite-plugin-dts'

// https://vitejs.dev/config/
export default defineConfig({
  build: {
    // 原生es模块
    target: 'modules',
    outDir: 'es',
    // 代码压缩和混淆
    minify: false,
    rollupOptions: {
      //忽略打包vue文件
      external: ['vue'],
      // 入口文件，这个文件要转发（导出）所有模块
      input: ['src/index.ts'],
      output: [
        {
          format: 'es',
          //不用打包成.es.js,这里我们想把它打包成.js
          entryFileNames: '[name].js',
          //让打包目录和我们目录对应
          preserveModules: true,
          //配置打包根目录
          dir: 'es',
          preserveModulesRoot: 'src'
        },
      ]
    },
    lib: {
      entry: 'src/index.ts',
      formats: ['es']
    }
  },
  plugins: [
    vue(),
    dts()
  ]
});

```

