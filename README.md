# Lab Training 2026

歡迎加入實驗室！👋

實驗室目前正處於從舊有專案結案、全面轉向 **ROS 2** 的拓荒期。

本專案是給 2026 屆新生的基礎訓練起點，目標是讓你熟悉：

1. **Git 版本控制與 GitHub Flow** — Pull Request 協作流程
2. **Docker 環境隔離** — 確保開發環境一致
3. **ROS 2 (Humble) 基礎通訊與 Turtlesim 模擬**

---

## 專案結構

```
lab-training-2026/
├── README.md              # 你正在讀的這份文件
├── CLAUDE.md              # 給 Claude Code 的專案指令
├── .gitignore
├── docker/
│   ├── Dockerfile         # ROS 2 Humble + turtlesim
│   └── docker-compose.yml # X11 forwarding + host network
└── students/
    ├── template.md        # 自我介紹範本
    └── <你的學號>.md      # ← 任務一要建立的檔案
```

---

## 任務一：Git 協作與破冰任務 🎯

這個任務的目的是讓你跑過一次完整的 **GitHub Flow**，並認識實驗室的其他夥伴。

### Step 1 — Fork 本專案

點擊 GitHub 頁面右上角的 **Fork**，把這個 repo fork 到你自己的帳號底下。

### Step 2 — Clone 到本機

```bash
git clone https://github.com/<你的 GitHub 帳號>/lab-training-2026.git
cd lab-training-2026
```

### Step 3 — 建立屬於你的 feature branch

請使用以下命名規則（`<學號>` 換成你自己的學號）：

```bash
git checkout -b feature/intro-<學號>
```

> 範例：`git checkout -b feature/intro-M11315001`

### Step 4 — 複製 template 並填寫自我介紹

```bash
cp students/template.md students/<學號>.md
```

打開 `students/<學號>.md`，填入以下欄位：

- 姓名 / 綽號
- 大學畢業校系
- 最常寫的程式語言
- 進實驗室最想學到的一個技術
- 一句想說的話

### Step 5 — Commit & Push

```bash
git add students/<學號>.md
git commit -m "docs(intro): add self-introduction for <學號>"
git push origin feature/intro-<學號>
```

### Step 6 — 發送 Pull Request

1. 回到 GitHub，進入你 fork 後的 repo 頁面，點擊 **Compare & pull request**。
2. PR 的 **base repository** 請選擇實驗室的原始 repo，**base branch** 選 `main`。
3. PR 模板會自動帶入勾選清單，請逐項確認後填寫描述。
4. **學長會被 CODEOWNERS 自動指派為 reviewer，無需手動指派**。
5. 等待 CI 綠燈（`Validate student introduction`）與學長 approve 後合併 🎉

> 💡 如果 CI 紅燈，請點開 Actions log 看錯誤訊息、在 **同一個分支** 修正後重新 push，**不要關閉 PR 重開**。詳細協作規範見 [CONTRIBUTING.md](CONTRIBUTING.md)。

---

## 任務二：Docker + Turtlesim（後續）

當你完成任務一之後，可以試著用 `docker/` 底下的設定啟動容器並執行 turtlesim。

> ⚠️ Turtlesim 是 **GUI 應用程式**，容器內的視窗必須透過 **X Server** 才能顯示到你的桌面。請依照你的作業系統先安裝 X Server。

### 前置作業：安裝 X Server

#### 🐧 Linux

Linux 桌面環境本身已內建 X Server，只需要在 host 端允許 Docker 容器連線：

```bash
xhost +local:docker
```

#### 🪟 Windows

安裝 **VcXsrv**：<https://vcxsrv.com/>

1. 下載並安裝 VcXsrv。
2. 啟動 **XLaunch**，依下列設定一路 Next：
   - Display settings: **Multiple windows**，Display number: `0`
   - Client startup: **Start no client**
   - Extra settings: **勾選 `Disable access control`**（允許 Docker 容器連線）
3. 確認右下角工作列出現 VcXsrv 圖示，並在 PowerShell 設定環境變數：
   ```powershell
   $env:DISPLAY = "host.docker.internal:0.0"
   ```
   > 💡 也可以用 [MobaXterm](https://mobaxterm.mobatek.net/) 或 WSL2 + WSLg（Windows 11 內建 X Server，免安裝）。

#### 🍎 macOS

安裝 **XQuartz**：<https://www.xquartz.org/>

1. 下載安裝後 **登出再登入**（讓系統載入 XQuartz）。
2. 啟動 XQuartz → **Preferences → Security**，勾選 **Allow connections from network clients**。
3. 終端機執行：
   ```bash
   xhost +localhost
   export DISPLAY=host.docker.internal:0
   ```

### 啟動容器

```bash
cd docker
docker compose up -d
docker compose exec ros2-lab bash

# 進入容器後
ros2 run turtlesim turtlesim_node
```

成功的話，你的桌面上會跳出一隻可愛的小烏龜 🐢。

詳細的 ROS 2 教學會在後續課程中逐步展開。

---

## 開發守則

- 所有的 ROS 2 教學與實作皆以 **Humble** 版本為主。
- 專案保持極簡，**不引入** Gazebo 等重型模擬器設定。
- 任何修改都透過 PR 進行，不要直接 push 到 `main`。

Happy hacking! 🚀
