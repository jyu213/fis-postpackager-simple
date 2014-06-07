# fis-postpackager-simple

用于自动打包页面零散资源和应用打包资源的[FIS](https://github.com/fex-team/fis/)插件

## 功能

 - 自动将页面中声明的资源引用替换为pack中设置的资源
 - 自动将未打包的零散资源按照引用顺序打包

## 静态资源处理策略

 - ```<script src='path'></script>``` 引用的脚本默认会在打包后移动到body底部
 - ```<script data-single='true' src='path'></script>``` 引用的脚本不会进行自动打包
 - ```<link rel='stylesheet' href='path'>``` 引用的样式表默认会在打包后移动到head底部
 - ```<link rel='stylesheet' href='path'>``` 引用的样式表默认会在打包后移动到head底部
 - ```<script>console.log('hello world')</script>``` 编写的内嵌脚本将会移动到body底部
 - ```<script|link data-fixed='true'>``` 声明的标签不会被处理
 - ```<style></style>``` 不会进行任何处理

## 用法

    $ npm install -g fis-postpackager-simple
    $ vi path/to/project/fis-conf.js

```javascript
//file : path/to/project/fis-conf.js
fis.config.set('modules.postpackager', 'simple');
//关闭autoCombine可以设置是否将零散资源进行打包
//fis.config.set('settings.postpackager.simple.autoCombine', false);
```

## 配置项

### autoCombine

设置是否自动将零散资源进行打包，默认为 `true`，关闭后仅会替换设置了pack的资源

### fullPackHit

设置是否资源需要全部命中pack设置才会将整个资源包引用

#### fullPackHit.js

默认为 `false`，使js资源尽量使用pack后的资源包，加强缓存能力。

#### fullPackHit.css

默认为 `true`，仅当pack设置中某个包所有的样式资源均被页面依赖的情况下，才会加载资源包，这是为了避免引入了错误的样式内容导致网页显示异常。

## 适应范围

用于简单的Web前端项目自动打包减少页面请求连接数，同时可以通过[pack](https://github.com/fex-team/fis/wiki/%E9%85%8D%E7%BD%AEAPI#pack)设置来对公共资源进行独立打包

## DEMO

https://github.com/hefangshi/fis-quickstart-demo
