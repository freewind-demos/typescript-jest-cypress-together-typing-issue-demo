TypeScript Jest Cypress Together Typing Issue Demo
=========================================

由于jest和cypress都有global的`expect`，所以当一个项目中同时存在jest与cypress时，
哪怕它们分别在自己的目录，也会存在`expect`冲突的问题，即总是在某一方测里的`expect`类型不对。

由于typescript在编译时期对于typing的定位和选择很难调试，所以这个问题花费了我很多时间，
基本上靠各种示例调整各种参数。最后在这个示例的帮助下，终于成功：

https://github.com/cypress-io/cypress-and-jest-typescript-example

解决方法：
1. 在根目录下的`tsconfig.json`，主要设置的是jest需要的类型，所以其中有`"types": ["jest"]`
2. 根目录下`tsconfig.json`中的`"include": ["src/**/*"]`是为了让`tsc --noEmit`通过，否则typescript会同时编译cypress测试，会再次遇到`cypress`问题
3. 在`cypress`目录下的`tsconfig.json`需要重新指定`include`的文件
4. 其`"types": ["cypress"]`似乎可要可不要
5. `cypress/plugins/index.js`中使用的`@cypress/webpack-preprocessor`对于这个问题无影响

注意：
1. cypress中不能`import 'cypress'`（我曾尝试使用该方法来解决typing的问题），因为会导入一些额外的东西，导致cypress测试报错：
    ```
    Error: Can't resolve 'child_process' in ...
    ```

```
npm install
npm run test:open

npm run test:run
```
