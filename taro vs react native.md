# Taro vs React Native 八大差异

## API风格
Taro 与 RN 的一些组件及字段并不完全一致，以 RN 为主 vs 以 Taro 为主，
如 RN 的 Touchable* 为 onPress 而 Taro 的 View 为 onClick

## 技术栈约束
1. 选用轻量第三方库，按需引入，按需加载
2. RN 和 Taro 版本在开发阶段应尽早启用新版本


## 样式
1. 行内 vs 外联：style={styles.abc} 与 className="abc"
2. 外联时，像素乘以 2，RN 不需要单位
3. 内联时，h5 需要 px 单位，RN 不需要单位， Taro 默认以 750px 作为换算尺寸标准
4. box-sizing: RN全是 container-box, Taro 默认为 content-box
5. position 在 RN 默认为 relative， 不支持 fixed， 而 Taro 需要手动配置，才能让子组件的绝对定位和 zIndex 生效
6. View 和 Text 的默认行高 与 RN 默认行高并不一致， RN 行高未配置
7. Text 在 RN 默认为 display-block 而 Taro 为 inline，导致 padding、margin、width、height 行为不一致，间接导致 text-align: center 不起作用
8. display: grid 在 RN 并不支持
9. RN 安卓对 zIndex 支持不好，需要 elevation
10. RN 安卓的阴影不平滑，不支持 box-shadow
11. RN 不支持伪类 :before :after
12. RN 不支持类层叠样式
13. Taro 动画 Api 与 RN 动画 Api 不一致
14. RN 仅支持 flex 不支持 grid
15. RN 的 background 仅支持 backgroundColor, 不支持 background-image,
渐变色的实现需要借助 react-native 的第三方包 react-native-linear-gradient
16. RN 不用指定 borderStyle, Taro 需要指定 borderStyle
17. RN 的 font-weight样式只支持400、700、bold、normal这几个值


## 图片
1. 图标方案：svg vs base64+png vs sprite
2. 图标考虑深色与浅色、不可用状态的颜色变化
3. RN.svg 不支持，需要引入第三方库（也不能完美支持）, Taro 支持 svg 格式的图片

## 组件
1. 是否二次包装 Taro 的 Text、Image，以及 ScrollView，FlatList
2. Taro.ScrollView 的 height 需要手动指定
3. Taro 不支持 React.Fregment 
4. Taro.View 有 onClick，而 RN.Touchable* 有 onPress
5. Taro 不支持全局组件，如 Alert 和 Loading，且 Loading 在页面切换时会丢失
6. RN 允许全局组件，Taro 因小程序是由页面为单位，故没有全局组件，如 Loading
7. 两个页面级别组件不能 import (不包含子组件)，否则 Please do not register multiple Pages

## Header / Footer
1. RN 有 statusBar，有深色与浅色主题两个区别，图标也应考虑两个主题
2. RN 的 footer 得考虑 IPhone 的全面屏影响
3. 影响到右上角的按钮和状态类图标及动画设计(如抛物线动画)

## Webview
1. Taro.Webview 只有 src 属性，js 通讯只能同源（第三方支付有问题），而 RN.WebView 有 source 支持 html 属性，js 通讯允许不同源
2. Taro.Webview 事件勾子只有 onLoad，RN.WebView 可以监听 url 的变化和 method，用于第三方支付完成的回调特别友好

## Hooks
1. Taro 使用 Promise.finally 代码块中用 setState 等 hooks 可能不起作用，尽量在 then 和 catch 里使用 hooks
2. Taro 的一些全局 API 脱离 React 的更新机制，如徽标数字的更新
