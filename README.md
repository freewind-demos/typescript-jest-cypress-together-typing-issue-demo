TypeScript Cypress Test Demo
=========================================

注意点：

1. `cypress/plugins/index.js`不能使用`.ts`，所以`webpack.config.js`也不能使用`.ts`
2. 由于混用了`.js`与`.ts`，所以webpack中要设置`resolve`->`extensions`
3. `tsconfig.json`中一定要设置`"types": [ "cypress" ]`，否则`cy`等typing找不到

```
npm install
npm run test:open

npm run test:run
```
