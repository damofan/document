### vue2.0 + ant design 优化

#### 1、按需引入

- [ ] Echart升级为5.0（ps: 同步升级其他package），并修改为按需引入，**2.54MB → 1.9MB**

- [ ] 配合webpack的**IgnorePlugin**/**ContextReplacementPlugin**，将Moment的locale改为按需引入，**669KB → 169KB**

  ```js
  // 1、IgnorePlugin -- 配置
  const webpack = require('webpack');
  chainWebpack: config => {
      // load `moment/locale/ko.js` and `moment/locale/zh-cn.js`
      config
          .plugin("ignore")
          .use(
          new webpack.IgnorePlugin(/^\.\/locale$/, /moment$/)
      );
      // ...
  }
  // 引用时
  const moment = require('moment');
  require('moment/locale/zh-cn');
  require('moment/locale/ko');
  // moment.locale('zh-cn');
  
  // 2、ContextReplacementPlugin -- 不需要再次引入
  const webpack = require('webpack');
  chainWebpack: config => {
      // load `moment/locale/ko.js` and `moment/locale/zh-cn.js`
      config
          .use(
          new webpack.ContextReplacementPlugin(/moment[/\\]locale$/, /zh-cn|ko/)
      );
      // ...
  }
  ```


- [ ] 手动按需引入 **@ant-design/icons**，体积减小 **530KB**

  ```js
  // 新建 icons.js
  export { default as DeleteOutline } from "@ant-design/icons/lib/outline/DeleteOutline";
  export { default as DribbbleOutline } from "@ant-design/icons/lib/outline/DribbbleOutline";
  export { default as DownOutline } from "@ant-design/icons/lib/outline/DownOutline";
  
  // ant 组件用到 -- 也需要手动引入
  export { default as CloseOutline } from "@ant-design/icons/lib/outline/CloseOutline";
  export { default as LeftOutline } from "@ant-design/icons/lib/outline/LeftOutline";
  export { default as RightOutline } from "@ant-design/icons/lib/outline/RightOutline";
  export { default as UpOutline } from "@ant-design/icons/lib/outline/UpOutline";
  export { default as CloseCircleFill } from "@ant-design/icons/lib/fill/CloseCircleFill";
  export { default as LoadingOutline } from "@ant-design/icons/lib/outline/LoadingOutline";
  
  // 配置别名
  resolve: {
      alias: {
        '@ant-design/icons/lib/dist$': path.resolve(__dirname, 'src/utils/icons.js')
      },
    }
  ```

  