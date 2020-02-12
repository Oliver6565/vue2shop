# vue_shop

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).



1.导入mydb.sql文件，路径不能有中文

2.导入mydb.sql文件时多等几分钟

3.在Vue ui中出现编译错误，看输出

4.tabs太严格，在.eslintric.js中的rules下面加一个'no-tabs': 'off'

5.坑人的eslint，缩进只能用空格缩进（规范）代码最后需要留一行即回车一下，不必要的分号；要去掉，对象方法后面需要空一格,
单引号来表示字符串

6.對5部分問題的解決:'space-before-function-paren':0 ，方法後面可以不加空格了。