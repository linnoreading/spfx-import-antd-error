# spfx-import-antd-error

### summary
2021.7.29创建的spfx项目，import antd报错：TS1005: ';' 
expected.

此项目仅用于antd提交错误 [antd issue](https://github.com/ant-design/ant-design/issues/31573)，当前项目typescript版本还是3.7.7,未更新。

### 原因
spfx v1.12.1默认typescript版本为3.7.7

### 解决方案
spfx 升级typescript 到v4+

[Use Different Versions of TypeScript in SPFx projects](https://spblog.net/post/2021/07/28/spfx-fast-serve-new-features-native-serve-and-hot-module-replacement-aka-hmr)

1. re-install rush-stack-compiler 4+
```powershell
npm uninstall @microsoft/rush-stack-compiler-3.7 --save-dev
npm install @microsoft/rush-stack-compiler-4.2 --save-dev 
```
2. Then update tsconfig.json so that it extends the 4.2 version instead of 3.7

```js
"extends": "./node_modules/@microsoft/rush-stack-compiler-4.2/includes/tsconfig-web.json",
```
3. TypeScript 4+ doesn't support tslint (tslint is deprecated). Thus you should disable the tslint task in your gulpfile.js:
```js
build.tslintCmd.enabled = false;
```
Otherwise, the build will fail. As an alternative to tslint, you can use eslint.

4. delete node_modules folder、package-lock.json、yarn.lock，re-install all modules,and then gulp serve,run successfully.