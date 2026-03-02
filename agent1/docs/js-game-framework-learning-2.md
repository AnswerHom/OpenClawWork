# JS语言和游戏开发框架学习笔记（第2次）

## 学习时间
- **日期**: 2026-03-02 22:07
- **学习内容**: JS最新特性 + TypeScript + React最新文档

---

## 一、JavaScript最新特性（MDN 2025-07-16更新）

### 1.1 内置对象更新

**新增内存管理对象**
```javascript
// 弱引用
const weakRef = new WeakRef(target);
const deref = weakRef.deref(); // 获取引用，可能为undefined

// 终结化注册表
const registry = new FinalizationRegistry(heldValue => {
  console.log('对象被回收:', heldValue);
});
registry.register(target, 'target-1');
```

**国际化增强**
```javascript
// 新的格式化选项
const segmenter = new Intl.Segmenter('zh-CN', { granularity: 'word' });
const segments = segmenter.segment('你好，世界！');
for (const { segment, isWordLike } of segments) {
  console.log(segment, isWordLike);
}
```

### 1.2 语法特性

**类字段**
```javascript
class Game {
  name = 'My Game';  // 公有类字段
  #privateField = 'private';  // 私有字段（#开头）

  constructor() {
    console.log(this.#privateField);
  }
}
```

**静态初始化块**
```javascript
class Config {
  static #data = null;

  static async load() {
    if (!Config.#data) {
      Config.#data = await fetch('/config.json').then(r => r.json());
    }
    return Config.#data;
  }
}
```

**尾后逗号**
```javascript
function gameLoop(
  deltaTime,
  player,
  enemies,
  particles,  // 尾后逗号
) {
  // ...
}
```

### 1.3 迭代协议

**异步生成器**
```javascript
async function* loadLevels() {
  yield 1;
  await delay(1000);
  yield 2;
  await delay(1000);
  yield 3;
}

for await (const level of loadLevels()) {
  console.log('Loading level', level);
}
```

**异步迭代器**
```javascript
async function* loadAssets() {
  yield fetch('/level1.json');
  yield fetch('/level2.json');
  yield fetch('/level3.json');
}

const response = await (await loadAssets().next()).value;
const data = await response.json();
```

---

## 二、TypeScript最新特性

### 2.1 类型工具

**从类型创建类型**
```typescript
// 类型映射
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

// 部分类型
type Partial<T> = {
  [P in keyof T]?: T[P];
};

// 必选类型
type Required<T> = {
  [P in keyof T]-?: T[P];
};

// Pick和Omit
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};

type Omit<T, K extends keyof T> = {
  [P in Exclude<keyof T, K>]: T[P];
};
```

### 2.2 函数类型

**函数重载**
```typescript
function loadResource<T>(url: string): Promise<T>;

function loadResource<T>(url: string, options?: LoadOptions): Promise<T>;

async function loadResource<T>(url: string, options?: LoadOptions): Promise<T> {
  // 实现
}
```

### 2.3 类类型

**类约束**
```typescript
interface Game {
  name: string;
  play(): void;
}

class UnityGame implements Game {
  name = 'Unity Game';
  play() {
    console.log('Playing in Unity');
  }
}
```

---

## 三、React最新特性（2025）

### 3.1 组件基础

**函数组件**
```javascript
function MyButton() {
  return <button>I'm a button</button>;
}

export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```

**JSX语法**
```javascript
// JSX比HTML更严格
function AboutPage() {
  return (
    <>
      <h1>About</h1>
      <p>Hello there.<br />How do you do?</p>
    </>
  );
}
```

### 3.2 数据显示

**变量嵌入**
```javascript
const user = {
  name: 'Hedy Lamarr',
  imageUrl: 'https://i.imgur.com/yXOvdOSs.jpg',
  imageSize: 90,
};

return (
  <>
    <h1>{user.name}</h1>
    <img
      className="avatar"
      src={user.imageUrl}
      alt={'Photo of ' + user.name}
      style={{
        width: user.imageSize,
        height: user.imageSize
      }}
    />
  </>
);
```

**条件渲染**
```javascript
function GameMenu({ isLoggedIn, user }) {
  if (!isLoggedIn) {
    return <LoginButton />;
  }

  return (
    <>
      <h1>Game Menu</h1>
      <Welcome user={user} />
    </>
  );
}
```

**列表渲染**
```javascript
function LevelList({ levels }) {
  return (
    <ul>
      {levels.map(level => (
        <li key={level.id}>
          Level {level.number}
        </li>
      ))}
    </ul>
  );
}
```

### 3.3 事件处理

**事件监听**
```javascript
function GameOver({ score, onRestart }) {
  return (
    <div>
      <h1>Game Over</h1>
      <p>Final Score: {score}</p>
      <button onClick={onRestart}>
        Play Again
      </button>
    </div>
  );
}
```

**状态管理**
```javascript
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </>
  );
}
```

---

## 四、游戏开发相关框架

### 4.1 React游戏框架

**React Three Fiber（3D游戏）**
```javascript
import { Canvas } from '@react-three/fiber';
import { OrbitControls } from '@react-three/drei';

function GameScene() {
  return (
    <Canvas>
      <OrbitControls />
      <GameCharacter />
      <Light />
    </Canvas>
  );
}
```

**Pixi.js（2D游戏）**
```javascript
import * as PIXI from 'pixi.js';

const app = new PIXI.Application();
document.body.appendChild(app.view);

const sprite = PIXI.Sprite.from('game-character.png');
sprite.x = 100;
sprite.y = 100;
app.stage.addChild(sprite);

app.ticker.add((delta) => {
  sprite.rotation += 0.01;
});
```

### 4.2 Vue游戏开发

**Vue + Phaser**
```javascript
import Vue from 'vue';
import Phaser from 'phaser';

new Vue({
  el: '#app',
  data() {
    return {
      game: null
    };
  },
  mounted() {
    this.game = new Phaser.Game({
      type: Phaser.AUTO,
      width: 800,
      height: 600,
      scene: MainScene
    });
  }
});
```

### 4.3 PWA游戏

**Service Worker**
```javascript
// sw.js
self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open('game-cache').then((cache) => {
      return cache.addAll([
        '/',
        '/game.js',
        '/game.css',
        '/assets/*.png'
      ]);
    })
  );
});

self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request).then((response) => {
      return response || fetch(event.request);
    })
  );
});
```

---

## 五、技术趋势

### 5.1 JavaScript
- **WebAssembly**: 性能优化，接近原生速度
- **ES2024/2025**: 新特性持续推出
- **模块化**: ESM标准普及

### 5.2 TypeScript
- **类型推断增强**: 更智能的类型推导
- **装饰器**: 语法糖增强
- **模块增强**: 更好的模块系统

### 5.3 React
- **并发模式**: 更流畅的UI更新
- **Server Components**: 服务端组件
- **Suspense**: 异步数据加载

### 5.4 游戏开发
- **WebGPU**: 浏览器GPU加速
- **跨平台**: 一次开发，多平台运行
- **AI辅助**: AI辅助游戏开发

---

## 六、学习总结

### 关键知识点
1. **JS最新**: WeakRef、FinalizationRegistry、异步生成器、类字段
2. **TypeScript**: 类型工具、函数重载、类约束
3. **React**: 函数组件、JSX、条件渲染、列表渲染、事件处理
4. **游戏框架**: React Three Fiber、Pixi.js、Vue + Phaser、PWA

### 适用场景
- **React Three Fiber**: 3D游戏、虚拟现实
- **Pixi.js**: 2D游戏、轻量级应用
- **Vue + Phaser**: 小型游戏、快速开发
- **PWA**: 休闲游戏、离线游戏

### 未来方向
- WebGPU性能优化
- React Server Components
- TypeScript类型系统增强
- AI辅助游戏开发
