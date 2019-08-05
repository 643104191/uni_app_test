# test_polyfill

## 在项目中使用了es6新方法

> 如, `./src/pages/index/index.vue`中使用了es6的`Array.prototype.flatMap`

### 一、尝试过在`./src/main.js`中写

```javascript
import "core-js/fn/array/flat-map"
```

这种方式最终打包出来的代码 __有__ `flatMap`相关兼容代码
__上传到体验版__ 却没有`flatMap`方法
(见下图)
![体验版本使用flatMap报错1](https://user-images.githubusercontent.com/27074730/62449761-760fb480-b79d-11e9-82cf-7bb487b8d21b.png)


### 二、尝试过在`./babel.config.js`中的`@vue/app`配置中写polyfills
```javascript
module.exports = {
  presets: [
    [
      '@vue/app',
      {
        modules: 'commonjs',
        useBuiltIns: 'entry',
        polyfills: [
          'es7.array.flat-map'
        ]
      }
    ]
  ],
  plugins
}
```
但是最终打包出来的代码 __没有__ `flatMap`相关兼容代码
(见下图)
![体验版本使用flatMap报错2](https://user-images.githubusercontent.com/27074730/62450187-6cd31780-b79e-11e9-9c48-03fcc1e42092.png)