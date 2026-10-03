# 鐵砧輸入框 API

[English](README.md) | **繁體中文**

給 Skript 使用的文字輸入框函式庫：開啟鐵砧介面讓玩家打字，並透過自訂事件 `on anvil input` 讓任何腳本接收輸入結果。純 Skript + skript-reflect，不需要額外插件。

> 本儲存庫包含同一個腳本的兩個版本：**繁體中文（zh-TW）** 是作者伺服器實際使用的原始版本；**English** 為完整英文翻譯版（指令、訊息與變數名稱皆為英文），功能相同。

<!-- BEGIN LIVE SCREENSHOTS -->

## 畫面預覽

![鐵砧文字輸入視窗](docs/images/anvil-input.png)

*執行 `/anvilinput` 開啟示範輸入框。視窗類型、標題與兩個紙張欄位皆為伺服器在 `open_window` / `window_items` 中送出的實際內容。*

> 這些是實機擷取後重繪的畫面，不是原生客戶端截圖。流程為：無頭客戶端登入實機 Paper 26.2 伺服器觸發腳本，再以官方 Minecraft 26.2 客戶端素材忠實重繪伺服器回傳的方塊／介面資料。Mojang/Microsoft 的圖像資產不屬於本專案程式碼授權範圍。

<!-- END LIVE SCREENSHOTS -->

## 功能特色

- `openAnvilInput(玩家, 識別字串, 預設文字, 標題)`：任何腳本都能呼叫
- 自訂事件 `on anvil input`，搭配 `anvilId(玩家)` / `anvilText(玩家)` 取得結果
- 可自訂視窗標題（支援 `&` 色碼）與預設文字
- 開啟時暫時給 1 級經驗，確保付得起改名費用；取消時自動扣回
- 打字用的紙張不會殘留在玩家背包
- `setAnvilTitle(玩家, 標題)` 可在開啟中更換標題
- 內建示範指令 `/anvilinput`

## 需求

- [Paper](https://papermc.io/) 伺服器（開發環境 Paper 26.2 / Minecraft 26.2）－使用了 Paper 專屬 API（`openAnvil`、`titleOverride`、Adventure）
- [Skript](https://github.com/SkriptLang/Skript)（開發環境 2.16.2）
- [skript-reflect](https://github.com/SkriptLang/skript-reflect)（開發環境 2.6.3）

## 安裝

1. 先安裝[需求](#需求)中列出的插件。
2. 下載**其中一個**版本：

   | 版本 | 檔案 |
   |---|---|
   | 繁體中文（原始版本） | [`zh-TW/anvil_input_api.sk`](zh-TW/anvil_input_api.sk) |
   | English（英文） | [`en/anvil_input_api.sk`](en/anvil_input_api.sk) |

3. 把 `.sk` 檔案放進伺服器的 `plugins/Skript/scripts/`。
4. 執行 `/sk reload anvil_input_api`（請換成你放入的檔名），或重新啟動伺服器。

> [!IMPORTANT]
> **只能安裝其中一個版本。** 兩個版本是同一個腳本的不同語言，同時載入會互相衝突或重複執行。

## 在其他腳本中使用

```
# 開啟輸入框（任何腳本皆可）
openAnvilInput(player, "nickname", "", "&9請輸入暱稱")

# 接收結果（任何腳本皆可）
on anvil input:
    if anvilId(player) is "nickname":
        set {_text} to anvilText(player)
        send "你輸入了：%{_text}%" to player
```

## 指令

| 指令（中文版） | 英文版 | 說明 | 權限 |
|---|---|---|---|
| `/anvilinput` | `/anvilinput` | 開啟示範輸入框並回顯輸入內容 | 所有人 |

## 設定

- 檔案最下方的範例監聽（`demo`）與 `/anvilinput` 測試指令可以刪除。

## 注意事項

- 建議保持檔名 `anvil_input_api.sk`（或任何排序在使用它的腳本之前的名稱），確保自訂事件先被載入。
- 兩個版本的函式名稱與事件完全相同，其他腳本搭配任一版本都能使用。

## 相關專案

- [skript-player-menu-gui](https://github.com/Im-Tim-mI/skript-player-menu-gui)－玩家選單 GUI

## 授權

**MIT + Commons Clause**，完整條款請見 [LICENSE](LICENSE)。

- ✅ 可自由使用、複製、修改與分享本腳本。
- ✅ 本授權明確允許在收費或營利的 Minecraft 伺服器上安裝與運行本插件（含修改版）。
- ❌ 禁止的僅限於直接或間接販售本插件本體、修改版本，或以付費方式取得其檔案或原始碼。

Copyright (c) 2026 廷廷小教室、廷廷的家（Tim945）
