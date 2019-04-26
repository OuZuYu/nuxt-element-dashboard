# nuxt2 + element dashboard
使用了nuxt-element-dashboard 与 el-data-table ，增删查改都能向接口正确发送参数的，使用yapi时出现了403的问题，搜索了一番，试过改header，改mock等等仍然403，后来按照 https://github.com/FEMessage/el-data-table/issues/61 这个issue 中 levy9527 所说的改成私有也不行，最终使用levy9527 所说的使用 easy-mock解决了。

## 运行

```bash
# 安装依赖
yarn

# 使用mock接口进行开发，且不会有登录拦截
yarn mock:nologin

```

## 预览
![img](https://raw.githubusercontent.com/OuZuYu/images/master/images/deepexi-img.png)