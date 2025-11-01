# 🔨 PHP-React Todo Manager 專案計畫
> 目標：使用 React 作為前端與 PHP 提供 REST API，實作一個簡易任務管理系統 (Todo Manager)

## 🌟 專案目標
- 建立單頁應用 (SPA)，支援任務的建立、編輯、完成及刪除  
- 使用 React 責志 UI 與狀態管理，PHP 作為 API 伺服器  
- 選用輕量框架（如 Slim、Lumen）或純 PHP 實作 REST API  
- 選擇性加入簡易身份驗證模組（登入 / 登出）  

## 🪛 系統功能模組

### 任務管理
- **GET** `/api/tasks`：列出所有任務  
- **POST** `/api/tasks`：新增任務  
- **PUT** `/api/tasks/{id}`：更新任務內容或狀態  
- **DELETE** `/api/tasks/{id}`：刪除任務  

### 使用者身份驗證（選擇性）
- **POST** `/api/login`：登入並回傳 token（JWT 或 session）  
- 驗證每個 API 呼叫的授權標頭  
- **POST** `/api/logout`：登出  

### 前端功能
- 使用 React Hooks (`useState`, `useEffect`) 讀取與更新任務列表  
- 使用 React Router 進行頁面切換（若有登入頁）  
- 使用 Context 或 Reducer 管理全域狀態（登入與任務）  
- 提供表單輸入與驗證，包含 loading 與錯誤提示  

### 後端實作
- 設計任務資料模型（如：`id`, `title`, `status`, `created_at`）  
- 定義 API 路由與處理函式  
- 設定 CORS，允許前端存取  
- （如採用身份驗證）實作簡易 JWT 或 session 驗證  

### 部署與測試
- 前端使用 Vite 進行開發與打包  
- 後端 PHP 可透過 Apache/Nginx 或內建伺服器啟動  
- 使用環境變數設定 API 根路徑  
- 可部署於 Render、Heroku 或自架伺服器  

## 📋 開發時程建議（1～2 週）

| Phase | 內容概述 |
| --- | --- |
| 1 – 需求確認與計畫 | 定義資料結構、API 規格、驗證需求 |
| 2 – 後端搭建 | 搭建 PHP API，實作 CRUD；如需加入身份驗證 |
| 3 – 前端搭建與讀取資料 | 建立 React 專案，實作任務列表與新增功能 |
| 4 – 功能完整化 | 加入任務編輯、刪除與狀態切換、錯誤處理 |
| 5 – 進階功能與優化 | （可選）加入登入/登出；用 Context 或 Reducer 管理狀態 |
| 6 – 部署與測試 | 本地整合測試，部署至雲端並驗證功能 |
