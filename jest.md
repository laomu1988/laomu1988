# jest

1. jest case执行失败时，执行指定代码
```js
// 参考 https://stackoverflow.com/questions/48388206/how-to-run-function-when-any-test-fails-jest
jasmine.getEnv().addReporter( {
     specStarted: result => jasmine.currentTest = result
});

afterEach(async () => {
    if (jasmine.currentTest.failedExpectations.length > 0) {
        // 执行失败时才执行后续代码
        const testPath = jasmine.currentTest.testPath;
        const desc = jasmine.currentTest.fullName;
        const testFileName = testPath.replace(process.cwd() + '/cases/', '').replace(/\.js$/, '');
        const shotPathName = (testFileName + '_'+ desc).replace(/[^\w]/g, '_')
            + '.png';
        const errorPath = config.errorFolder + shotPathName;
        console.error('ExecErrorShot:', testPath, ' case:[' + desc + ']', errorPath);
        await page.screenshot({path: errorPath});
    }
});

```
