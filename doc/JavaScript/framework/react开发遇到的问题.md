### 1. Module build failed: SyntaxError: Missing class properties transform.

在react中遇到报错信息：

```
Module build failed: SyntaxError: Missing class properties transform.
```

经过查找发现是webpack配置中的问题，

我之前在webpack中的配置：

```
 module: {
    rules: [
      {
        test: /\.js[x]?$/,
        exclude: /node_modules/,
        loader: 'babel',
        query: {
           presets: ['react', 'env']
        }
      },
 .........
```

修改解析jsx的配置：

```
 module: {
    rules: [
      {
        test: /\.js[x]?$/,
        exclude: /node_modules/,
        loader: 'babel',
        query: {presets: ['react', 'stage-0'], cacheDirectory: true}
      },
 .........
```

https://github.com/babel/babel/issues/2729