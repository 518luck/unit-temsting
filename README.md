# 单元测试 (Vitest)

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

## 3 react 中的搭配

- [@testing-library/react](https://link.juejin.cn/?target=https%3A%2F%2Flink.zhihu.com%2F%3Ftarget%3Dhttps%253A%2F%2Fgithub.com%2Ftesting-library%2Freact-testing-library 'https://link.zhihu.com/?target=https%3A//github.com/testing-library/react-testing-library')：
  作为 React DOM 和 UI 组件
- @testing-library/jest-dom：用于扩展 Vitest 的 expect 方法

# 3.1 **测试规范**

## 1 命名约定 it or test?

1. it 是 BDD（行为驱动开发）风格中常用的命名约定。它强调描述被测试行为的自然语言
   描述，以便更好地阐述测试的用例。
2. test 是传统的命名约定，被广泛使用在各种单元测试框架中。它更加直接和简洁，通常
   以测试的目标作为开头，然后描述被测试的函数或特性。

无论使用 it 还是 test 作为测试函数的命名约定，最重要的是保持一致性和可读性。根据
你的团队或项目的偏好，选择一个适合的命名约定并始终如一地使用它。

## 2 判断相等 toBe or toEqual?

1. toBe 它使用===检查严格的平等，通常用于比较基础类型。
2. toEqual 用于检查两个对象具有相同的值。这个匹配器递归地检查所有字段的相等性，
   而不是检查对象身份 - 这也被称为“深度平等”。

使用 toBe 进行比较时要注意，它比较的是两个对象的引用，而不是对象的属性是否相同。

## 3 测试文件写在哪？

1. 把测试文件统一写在 src/**test**/，这样保持项目和测试代码分离，保持工程目录整
   洁。
2. 和组件写在同一级目录，即 src/components/下，xx.jsx、xx.test.jsx, 这样对开发人
   员友好，组件与测试一起更方便维护。

## 4 测试用例注意事项

1. **清晰的目的和描述**：测试用例应该具有清晰的目的和描述，以便于理解和维护。用
   一个简洁但有意义的名称来描述该测试用例的功能或行为。
2. **单一功能和场景**：每个测试用例应该只关注一个功能或一个特定的场景。这有助于
   准确地定位和修复问题。
3. **确保环境一致性**：对于每个测试用例，提供必要的前提条件，确保测试环境的一致
   性。
4. **测试目标简单、完整**：尽量把业务代码的函数的功能单一化，简单化。如果一个函
   数的功能包含了十几个功能数十个功能，那应该对该函数进行拆分，从而更加有利于测
   试的进行。

# 使用 Vitest 测试 React 项目

## 1 安装相关工具

`pnpm i -D vitest js-dom @testing-library/react`

## 2 配置 vitest

Vitest 的主要优势之一是它与 Vite 的统一配置。如果存在，vitest 将读取你的根目录
vite.config.ts 以匹配插件并设置为你的 Vite 应用程序。

如果你已经在使用 Vite，请在 Vite 配置中添加 test 属性。你还需要使用
[三斜杠指令](https://link.juejin.cn?target=https%3A%2F%2Fwww.typescriptlang.org%2Fdocs%2Fhandbook%2Ftriple-slash-directives.html%23-reference-types- 'https://www.typescriptlang.org/docs/handbook/triple-slash-directives.html#-reference-types-')
在你的配置文件的顶部引用。

```tsx title:vite.config.ts
/// <reference types="vitest" />
import { defineConfig } from 'vite'

export default defineConfig({
  test: {
    globals: true,
    environment: 'jsdom',
  },
})
```

- globals: 默认情况下，vitest 不显式提供全局 API。如果你更倾向于使用类似 jest 中
  的全局 API，可以将 --globals 选项传递给 CLI 或在配置中添加 globals: true。
- environment: Vitest 中的默认测试环境是一个 Node.js 环境。如果你正在构建 Web 端
  应用程序，你可以使用
  [jsdom](https://link.juejin.cn?target=https%3A%2F%2Fgithub.com%2Fjsdom%2Fjsdom 'https://github.com/jsdom/jsdom')
  或
  [happy-dom](https://link.juejin.cn?target=https%3A%2F%2Fgithub.com%2Fcapricorn86%2Fhappy-dom 'https://github.com/capricorn86/happy-dom')
  这种类似浏览器 (browser-like) 的环境来替代 Node.js。

## 3 方法测试

测试独立的工具函数，例如测试斐波那契数列：

_@param_ 方法接受参数 num

_@return_ 返回值为斐波那契数列中第 n 个数字

```TS title:fibonacci.ts
export function fibonacci(num: number): number {
  if (num <= 1) {
    return num;
  }
  return fibonacci(num - 1) + fibonacci(num - 2);
}
```
