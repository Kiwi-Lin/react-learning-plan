# 🌐 React 四週完整學習計畫
> 適用對象：具備 HTML、CSS、JavaScript（含 jQuery）、PHP 基礎者  
> 學習目標：建立現代前端開發能力，能獨立開發 React SPA 應用

---

## 🗓️ Week 1：React 核心與思維轉換
**目標**：理解 React 基礎概念與元件化思維，完成第一個互動式應用

### Day 1｜React 是什麼？思維轉換
- React 與 jQuery 的根本差異：宣告式 vs 命令式
- Virtual DOM 與狀態驅動畫面
- JSX 基本概念
```js
// jQuery 版本
$('#btn').click(() => $('#msg').text('Hello jQuery'));

// React 版本
function App() {
  const [msg, setMsg] = React.useState('');
  return (
    <div>
      <button onClick={() => setMsg('Hello React!')}>Click</button>
      <p>{msg}</p>
    </div>
  );
}
```

---

### Day 2｜建立 React 專案
- 使用 Vite 建立開發環境  
  ```bash
  npm create vite@latest my-react-app -- --template react
  cd my-react-app
  npm install
  npm run dev
  ```
- JSX 語法規則：`className`、表達式 `{}`、條件渲染

---

### Day 3｜Component 元件化思維
- Component = 函式 + 回傳 JSX
- Props 傳遞資料
```jsx
function Welcome(props) {
  return <h2>Hello, {props.name}!</h2>;
}
function App() {
  return (
    <div>
      <Welcome name="小明" />
      <Welcome name="小華" />
    </div>
  );
}
```

---

### Day 4｜State 與事件處理
- `useState()` 狀態管理
- 事件寫法 `onClick={}`
```jsx
function Counter() {
  const [count, setCount] = React.useState(0);
  return (
    <div>
      <p>目前計數：{count}</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
      <button onClick={() => setCount(0)}>重設</button>
    </div>
  );
}
```

---

### Day 5｜列表渲染與 key
- 使用 `map()` 動態渲染資料
- 每個項目需有唯一 key
```jsx
const fruits = ['🍎', '🍌', '🍒'];
<ul>{fruits.map((f, i) => <li key={i}>{f}</li>)}</ul>
```

---

### Day 6｜綜合練習：Todo List
- 新增 / 刪除項目  
- 使用狀態保存清單資料
- 延伸挑戰：加入 LocalStorage
```jsx
function TodoApp() {
  const [items, setItems] = React.useState([]);
  const [input, setInput] = React.useState('');
  const addItem = () => {
    if (!input.trim()) return;
    setItems([...items, input]);
    setInput('');
  };
  const removeItem = (i) =>
    setItems(items.filter((_, idx) => idx !== i));
  return (
    <div>
      <input value={input} onChange={(e) => setInput(e.target.value)} />
      <button onClick={addItem}>新增</button>
      <ul>
        {items.map((it, i) => (
          <li key={i} onClick={() => removeItem(i)}>{it}</li>
        ))}
      </ul>
    </div>
  );
}
```

---

### Day 7｜回顧與反思
- jQuery 改 DOM，React 改 State  
- 元件思維 = 模組化、重用性  
- 準備進入：資料流與 API 整合

---

## 🗓️ Week 2：資料流與 API 串接
**目標**：理解資料單向流、父子元件傳遞、useEffect 與 API 整合

### Day 1｜父子資料傳遞（Props Down, Events Up）
- Parent → Child：用 props 傳資料  
- Child → Parent：用 callback 通知
```jsx
function Child({ onAdd }) {
  return <button onClick={() => onAdd('新項目')}>Add</button>;
}
function Parent() {
  const [list, setList] = React.useState([]);
  const addItem = (item) => setList([...list, item]);
  return <Child onAdd={addItem} />;
}
```

---

### Day 2｜useEffect 與生命週期
- `useEffect()` ＝ componentDidMount + DidUpdate + WillUnmount
- 常見用途：API 讀取、事件監聽、計時器
```jsx
React.useEffect(() => {
  console.log('元件載入');
  return () => console.log('元件卸載');
}, []);
```

---

### Day 3｜API 串接練習
- 使用 `fetch()` 從 API 抓取資料  
- 加入 loading / error 狀態
```jsx
function Weather() {
  const [data, setData] = React.useState(null);
  React.useEffect(() => {
    fetch('https://api.open-meteo.com/v1/forecast?...')
      .then(res => res.json())
      .then(setData);
  }, []);
  if (!data) return <p>Loading...</p>;
  return <div>{data.temperature}</div>;
}
```

---

### Day 4｜表單處理與雙向綁定
- Controlled Components  
- 以 `value` + `onChange` 控制輸入框  
- 實作：登入表單元件  

---

### Day 5｜組件間資料流整合
- TodoApp 加上子元件 `<TodoItem />`
- 把邏輯與畫面分開（提早接觸 Container / Presentational pattern）

---

### Day 6｜綜合練習：天氣查詢應用
- 使用 OpenWeather API  
- 可輸入城市名稱查詢  
- 顯示溫度、天氣描述、圖示  

---

### Day 7｜回顧
- State 是資料核心  
- Props 控制資料流向  
- useEffect 負責「副作用」（資料請求、監聽）  

---

## 🗓️ Week 3：Routing 與模組化架構
**目標**：製作多頁式 SPA，建立頁面導覽結構與樣式管理

### Day 1｜React Router v6 基礎
- 安裝並設定路由
```bash
npm install react-router-dom
```
```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';
<BrowserRouter>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/about" element={<About />} />
  </Routes>
</BrowserRouter>
```

---

### Day 2｜動態路由與 Link
- `/user/:id` 參數傳遞  
- 使用 `useParams()` 取得路由參數  

---

### Day 3｜樣式管理與 Tailwind
- 建立共用 Layout  
- 導入 Tailwind CSS 或 CSS Module  

---

### Day 4｜資料結構分層
- 將專案分為：
  ```
  src/
   ├─ pages/
   ├─ components/
   ├─ services/
  ```
- 將 API 呼叫集中管理於 `services/`

---

### Day 5｜Context API 與全域狀態
- 建立 `UserContext` 管理登入狀態  
- 跨頁面資料共享  

---

### Day 6｜綜合練習：部落格 / 商品清單系統
- 首頁顯示列表  
- 點擊查看詳細頁  
- 使用 Router 切換畫面  

---

### Day 7｜回顧
- Router = 前端分頁  
- Context = 全域資料  
- 開始理解架構分層與重構的意義  

---

## 🗓️ Week 4：進階應用與部署
**目標**：製作可實際部署的前端專案，整合後端與最佳實踐

### Day 1｜Custom Hook
- 將重複邏輯抽出成 Hook  
```jsx
function useFetch(url) {
  const [data, setData] = React.useState(null);
  React.useEffect(() => {
    fetch(url).then(res => res.json()).then(setData);
  }, [url]);
  return data;
}
```

---

### Day 2｜整合 PHP / Node API
- 使用 `fetch('https://api.example.com/data.php')`  
- 處理 CORS 與 JSON  

---

### Day 3｜錯誤處理與最佳實踐
- try/catch 包裝 fetch  
- 將錯誤狀態分離管理  

---

### Day 4｜狀態管理延伸（Context + Reducer）
- 使用 `useReducer()` 管理複雜邏輯  
- 範例：購物車、登入登出  

---

### Day 5｜專案整合與優化
- 模組化資料夾結構  
- 代碼清理與註解規範  
- 測試頁面功能是否完整  

---

### Day 6｜部署實戰
- 使用 Vercel 或 Netlify 免費部署  
  ```bash
  npm run build
  ```
  上傳 `/dist` 目錄  

---

### Day 7｜總結與展望
- 你已能構建一個完整的 React SPA  
- 下一步建議：
  - 深入學習 Redux 或 Zustand 狀態管理  
  - 嘗試 Next.js（伺服端渲染）
  - 將 React 與你現有的 PHP 或 CI4 專案整合
