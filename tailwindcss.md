# 安装

```shell
npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
```

创建配置文件

```shell
npx tailwindcss init -p
```

引入tailwind

```css
/* ./src/index.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```



# 自定义配置

```json
module.exports = {
  content: [],
  theme: {
    extend: {
      gap: {
        '15': '15px',
        '16': '16px',
        '20': '20px',
        '22': '22px',
        '26': '26px',
        '80': '80px',
      }
    },
    spacing: {
      2: '2px',
      3: '3px',
      4: '4px',
      5: '5px',
      6: '6px',
      8: '8px',
      10: '10px',
      11: '11px',
      12: '12px',
      14: '14px',
      16: '16px',
      18: '18px',
      20: '20px',
      22: '22px',
      24: '24px',
      25: '25px',
      26: '26px',
      27: '27px',
      28: '28px',
      30: '30px',
      32: '32px',
      34: '34px',
      36: '36px',
      38: '38px',
      40: '40px',
      42: '42px',
      44: '44px',
      46: '46px',
      48: '48px',
      50: '50px',
      60: '60px',
      70: '70px',
      80: '80px',
      90: '90px',
      100: '100px',
    }
  },
  plugins: [],
  purge: ['./index.html', './src/**/*.{vue,js,ts,jsx,tsx}'],
}

```

