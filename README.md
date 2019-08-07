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

### 三、解决办法

安装如下两个npm库
* [uni-app-polyfills-presets](https://www.npmjs.com/package/uni-app-polyfills-presets)
* [uni-app-core-js](https://www.npmjs.com/package/uni-app-core-js)

__重要__ :在上面两个依赖的github里 __点一下star__ 有利于解决bug :)

```bash
npm install uni-app-polyfills-presets@1.0.0
npm install uni-app-core-js@1.0.0
```

然后在`./babel.config.js`里写

```javascript
module.exports = {
  presets: [
    // 上面的代码略...
    [
      'module:uni-app-polyfills-presets',
      {
        // 如果写usage那么将是按实际使用情况引入兼容库
        // 参数具体解释请前往https://babeljs.io/docs/en/babel-preset-env查看
        useBuiltIns: 'usage'
      }
    ]
    // 下面面的代码略...
  ],
  plugins
}
```
最终打包&上传到小程序平台之后
![已解决](https://user-images.githubusercontent.com/27074730/62610193-c02b9e00-b935-11e9-824b-5bbb688cf1de.png)
