# (Vitest)

这是我第一次接触单元测试,了解到前端还有单元测试

## 1 常见的单元测试工具

- **Jest：** Jest 是一个 Facebook 公司开发的流行的 JavaScript 测试框架。它提供了
  自动化测试、模拟和覆盖率报告等功能。Jest 的主要特点是易于使用、速度快、自动运
  行测试用例和提供详细报告。
- **Mocha：** Mocha 是一个流行的 JavaScript 测试框架，可以用于编写前端和后端测试
  用例。它提供不同的测试运行器、测试框架、覆盖率报告等工具。Mocha 可以与其他库（
  如 Chai、Sinon 等）结合使用，以提供更好的测试功能。
- **Enzyme：** Enzyme 是一个 React 组件测试工具，它提供了一个简单的 API 来模拟
  React 组件的行为。Enzyme 可以帮助开发人员测试组件的渲染和逻辑，以确保其正确性
  。它还提供了丰富的匹配器和渲染引擎，以进行功能和性能测试。

不过我习惯了用 vite 来构建,最好的选择还是 vitest 了

## 2 本次项目中测试框架和工具选择：

- 测试基础框架
  ：[Vitest](https://link.juejin.cn/?target=https%3A%2F%2Fcn.vitest.dev%2F 'https://cn.vitest.dev/') ，
  它是基于 vite 驱动，如果项目中使用了 vite，它是最好的选择
- DOM 环境：jsdom、happy-dom
