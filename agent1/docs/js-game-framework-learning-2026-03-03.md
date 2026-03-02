# JS语言和游戏开发框架学习笔记 - 第二次

## 学习时间
- **日期**: 2026-03-03 00:07
- **学习内容**: JavaScript官方文档 + TypeScript官方文档 + React官方文档

---

## 一、JavaScript官方文档核心内容

### 1.1 内置对象

**值属性**
- `globalThis`: 全局对象
- `Infinity`: 无穷大
- `NaN`: 非数字
- `undefined`: 未定义

**基本对象**
- `Object`: 对象构造器
- `Function`: 函数构造器
- `Boolean`: 布尔值
- `Symbol`: 唯一标识符

**错误对象**
- `Error`: 基础错误
- `TypeError`: 类型错误
- `ReferenceError`: 引用错误
- `SyntaxError`: 语法错误

**数字和日期**
- `Number`: 数字
- `BigInt`: 大整数
- `Math`: 数学函数
- `Date`: 日期时间

**文本处理**
- `String`: 字符串
- `RegExp`: 正则表达式

**索引集合**
- `Array`: 数组
- `Int8Array` ~ `BigUint64Array`: 类型化数组
- `Float32Array`, `Float64Array`: 浮点数组

**键集合**
- `Map`: 键值对集合
- `Set`: 唯一值集合
- `WeakMap`: 弱引用键值对
- `WeakSet`: 弱引用唯一值

**结构化数据**
- `ArrayBuffer`: 二进制缓冲区
- `SharedArrayBuffer`: 共享缓冲区
- `DataView`: 数据视图
- `Atomics`: 原子操作
- `JSON`: JSON处理

**内存管理**
- `WeakRef`: 弱引用
- `FinalizationRegistry`: 最终化注册表

**控制抽象**
- `Iterator`: 迭代器
- `AsyncIterator`: 异步迭代器
- `Promise`: Promise对象
- `Generator`: 生成器
- `AsyncGenerator`: 异步生成器

**反射**
- `Reflect`: 反射API
- `Proxy`: 代理对象

**国际化**
- `Intl.Collator`: 排序比较器
- `Intl.DateTimeFormat`: 日期格式化
- `Intl.NumberFormat`: 数字格式化
- `Intl.Locale`: 语言环境

### 1.2 语句和声明

**控制流**
- `return`, `break`, `continue`, `throw`
- `if...else`, `switch`

**声明变量**
- `var`: 函数作用域（已废弃）
- `let`: 块作用域
- `const`: 块作用域常量

**函数和类**
- `function`, `function*`: 函数和生成器函数
- `async function`, `async function*`: 异步函数
- `class`: 类定义

**迭代**
- `do...while`, `while`: 循环
- `for`, `for...in`, `for...of`: for循环
- `for await...of`: 异步for循环

**其他**
- `export`, `import`: 模块导出/导入
- `debugger`: 调试语句

### 1.3 表达式和运算符

**主要表达式**
- `this`: 当前上下文
- 字面量: `[]`, `{}`
- `function`, `class`: 函数和类表达式
- `/ab+c/i`: 正则表达式字面量
- `` `string` ``: 模板字符串
- `()`: 括号表达式

**左值表达式**
- 属性访问器: `obj.prop`, `obj["prop"]`
- `?.`: 可选链
- `new`: 创建实例
- `new.target`: 构造函数目标
- `import.meta`: 模块元数据
- `super`: 父类引用
- `import()`: 动态导入

**一元运算符**
- `delete`: 删除属性
- `void`: 返回undefined
- `typeof`: 类型检测
- `+`, `-`: 正负号
- `~`: 按位非
- `!`: 逻辑非
- `await`: 等待Promise

**算术运算符**
- `**`: 幂运算
- `*`, `/`, `%`: 乘、除、取模
- `+`, `-`: 加、减

**关系运算符**
- `<`, `>`, `<=`, `>=`: 比较运算符
- `instanceof`: 实例检测
- `in`: 属性检测

**相等运算符**
- `==`, `!=`: 宽松相等（不推荐）
- `===`, `!==`: 严格相等（推荐）

**位移运算符**
- `<<`, `>>`, `>>>`: 左移、右移、无符号右移

**二进制运算符**
- `&`, `|`, `^`: 与、或、异或

**条件运算符**
- `(condition ? ifTrue : ifFalse)`: 三元运算符

**赋值运算符**
- `=`, `*=`, `/=`, `%=`, `+=`, `-=`: 基本赋值
- `<<=`, `>>=`, `>>>=`: 位移赋值
- `&=`, `^=`, `|=`: 位运算赋值
- `**=`: 幂运算赋值
- `??=`: 空值合并赋值
- `[a, b] = arr`: 解构赋值
- `{ a, b } = obj`: 对象解构赋值

**展开语法**
- `...obj`: 展开对象/数组

---

## 二、TypeScript官方文档核心内容

### 2.1 基础概念

**核心特性**
- 类型注解: `function greet(name: string): void`
- 接口: 定义对象形状
- 泛型: 提升代码复用
- 联合类型: `string | number`
- 枚举: 定义常量集合

### 2.2 学习路径

**Everyday Types**
- 基础类型: string, number, boolean, null, undefined
- 数组类型: `string[]` 或 `Array<string>`
- 元组: 固定长度数组
- 枚举: `enum Color { Red, Green }`

**Creating Types from Types**
- 类型别名: `type Point = { x: number; y: number }`
- 字面量类型: `type Direction = 'up' | 'down' | 'left' | 'right'`
- 映射类型: 修改现有类型
- 条件类型: `type IsString = T extends string ? true : false`

**Techniques to make more elegant types**
- 模板字面量类型: `type EventName = `on${Capitalize<S>}`
- 模板字面量类型 + 索引签名: 类型安全的事件系统

**Functions**
- 参数类型: `(x: number, y: number) => number`
- 返回类型: `function add(a: number, b: number): number`
- 可选参数: `(name?: string) => void`
- 默认参数: `(name: string = 'default') => void`
- 重载: 多种调用方式

**Objects**
- 对象类型: `{ name: string; age: number }`
- 可选属性: `{ name?: string }`
- 只读属性: `{ readonly id: number }`
- 函数属性: `{ getName: () => string }`

**Narrowing**
- 类型收窄: 使用类型守卫
- typeof: 类型检测
- instanceof: 实例检测
- in: 属性检测
- 联合类型收窄: `if ('a' in obj)`

**Variable Declarations**
- `let`: 可变变量
- `const`: 常量
- `const`声明对象: 对象属性可变，但对象引用不可变

**TypeScript in 5 minutes**
- 快速上手TypeScript
- 基础类型
- 接口
- 类型别名
- 泛型

**Building a TypeScript web app**
- tsconfig配置
- 模块系统
- 类型检查

**tsconfig**
- 编译选项配置
- target: ES版本
- module: 模块系统
- strict: 严格模式
- outDir: 输出目录

**Classes**
- 类定义: `class Person { constructor(name: string) {} }`
- 访问修饰符: public, private, protected
- 构造函数: `constructor(name: string)`
- 继承: `class Student extends Person {}`
- 静态成员: `static count = 0`

---

## 三、React官方文档核心内容

### 3.1 组件基础

**创建组件**
```javascript
function MyButton() {
  return (
    <button>I'm a button</button>
  );
}
```

**嵌套组件**
```javascript
function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```

### 3.2 JSX语法

**基本规则**
- 组件名必须大写
- HTML标签必须小写
- 必须关闭标签: `<br />`
- 多个JSX标签必须包裹: `<><div>...</div><div>...</div></>`

**CSS类名**
```javascript
<img className="avatar" />
```

### 3.3 显示数据

**嵌入变量**
```javascript
return (
  <h1>{user.name}</h1>
);
```

**嵌入属性值**
```javascript
<img
  className="avatar"
  src={user.imageUrl}
/>
```

**内联样式**
```javascript
style={{
  width: user.imageSize,
  height: user.imageSize
}}
```

### 3.4 条件渲染

使用JavaScript的条件表达式
```javascript
{isLoggedIn ? <Dashboard /> : <Login />}
```

### 3.5 列表渲染

使用map函数
```javascript
const numbers = [1, 2, 3, 4, 5];
return (
  <ul>
    {numbers.map(n => <li key={n}>{n}</li>)}
  </ul>
)
```

### 3.6 事件处理

使用箭头函数
```javascript
function handleClick() {
  alert('Clicked!');
}
<button onClick={handleClick}>
  Click me
</button>
```

### 3.7 状态管理

使用useState Hook
```javascript
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <button onClick={() => setCount(count + 1)}>
      Clicked {count} times
    </button>
  );
}
```

### 3.8 副作用

使用useEffect Hook
```javascript
useEffect(() => {
  // 组件挂载后执行
  document.title = `Clicked ${count} times`;
  return () => {
    // 组件卸载前执行
  };
}, [count]);
```

---

## 四、技术要点总结

### JavaScript核心
- **内置对象**: 30+种内置对象，覆盖所有常用场景
- **类型系统**: 原始类型 + 对象类型 + 类型化数组
- **异步编程**: Promise + Async/Await + Generator
- **模块化**: ES6模块系统
- **反射**: Reflect + Proxy
- **国际化**: Intl API

### TypeScript核心
- **类型安全**: 编译时类型检查
- **类型推导**: 自动推导类型
- **高级类型**: 联合类型、交叉类型、映射类型、条件类型
- **类型工具**: 工具类型提升开发效率

### React核心
- **组件化**: 函数组件 + Hooks
- **声明式**: 声明式UI，而非命令式
- **虚拟DOM**: 高效更新
- **生态丰富**: 丰富的第三方库

---

## 五、学习建议

### JavaScript学习路径
1. 基础语法: 变量、函数、类
2. ES6+特性: 箭头函数、Promise、模块化
3. 内置对象: Array, Object, String, Date等
4. 异步编程: Promise, Async/Await
5. 事件循环: Event Loop机制

### TypeScript学习路径
1. 基础类型: string, number, boolean, any
2. 接口: 定义对象形状
3. 类型别名: type别名
4. 联合类型: `string | number`
5. 泛型: `<T>`, `extends`
6. 高级类型: 映射类型、条件类型

### React学习路径
1. 基础组件: 函数组件、JSX
2. 状态管理: useState
3. 事件处理: onClick, onChange等
4. 条件渲染: 三元表达式、逻辑与
5. 列表渲染: map, key属性
6. Hooks: useEffect, useContext等
7. 性能优化: useMemo, useCallback
8. 路由: React Router
9. 状态管理: Redux, Context API

---

## 六、应用场景

### JavaScript适用场景
- 前端开发
- 后端开发（Node.js）
- 移动端开发（React Native）
- 桌面端开发（Electron）
- 小游戏开发

### TypeScript适用场景
- 大型项目
- 团队协作
- 长期维护项目
- 需要类型安全的项目
- 重型前端框架项目

### React适用场景
- 单页应用（SPA）
- 复杂交互界面
- 仪表盘
- 管理后台
- 移动Web应用
- PWA应用

---

## 七、未来趋势

### JavaScript
- **ES2024**: 正则表达式改进、数组方法增强
- **ES2025**: 预计发布
- **WebAssembly**: 性能优化
- **Top-Level Await**: 模块顶层await

### TypeScript
- **类型推断增强**: 更智能的类型推导
- **装饰器**: 更好的装饰器支持
- **模块增强**: 更好的模块系统

### React
- **Server Components**: 服务器组件
- **Concurrent Mode**: 并发模式
- **Suspense**: 暂停加载
- **Next.js**: 全栈React框架
- **React Compiler**: 编译时优化
