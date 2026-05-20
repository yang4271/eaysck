# easyck

easyck 是一款基於 Java (Swing + JavaFX WebView) 開發的嵌入式多功能瀏覽器。本專案具備多分頁隔離、AES 加密虛擬檔案系統、雙快照備份機制、內建輕量型 API HttpServer，以及動態 JAR 插件載入架構，專為注重隱私安全與客製化擴充的環境而設計。

> [!WARNING]
> **執行環境要求**
> 本程式需在 JDK (或第三方 JRE) 21 (含) 以上版本方可正常執行。請確認您的 Java 執行環境符合此需求，否則可能導致啟動失敗或功能異常。
> **我們不保證本程式能在任何第三方修改、精簡或非官方發行的 Java 執行環境上穩定運作。**

## 核心功能

* **資料加密與安全**：啟動時強制進行密碼驗證，採用 PBKDF2WithHmacSHA256 進行密鑰衍生。書籤、Cookie、網站權限等使用者資料皆透過 AES/CBC/PKCS5Padding 加密儲存於本地 `data.sec` 檔案中。
* **Snapshot 雙快照保護**：內建守護執行緒（Daemon Thread）進行背景自動儲存。提供 `SNAPSHOT_1` 與 `SNAPSHOT_2` 雙重循環快照備份機制，防止因程式異常中斷導致的檔案損毀。
* **動態記憶體插件架構**：自訂 `MemoryClassLoader`，可直接從加密的虛擬檔案系統中動態讀取、解密並執行外掛的 `.jar` 插件。支援解析插件 Manifest 以動態建構 GUI 設定面板與 Webhook 事件綁定。
* **分頁隔離與資源控制**：支援多分頁瀏覽，各分頁可獨立配置記憶體上限（Memory Limit）以防止單一網頁導致系統 OOM，並支援虛擬硬體配額管理（GPU / NPU）。
* **內建 API 伺服器與權限核心**：基於 `com.sun.net.httpserver` 實現輕量級伺服器，支援動態路由、中介軟體（Middleware）及動態控制。同時透過網頁端腳本注入，嚴格攔截與控管鏡頭、麥克風、MIDI 存取及彈出視窗。
* **介面與體驗優化**：具備非同步初始化載入的啟動旋轉動畫，支援系統、亮色（Light）、暗色（Dark）主題切換與全分頁動態更新，並內建防自動化偵測機制（封鎖 WebDriver 標識與按鍵強制作業）。

## 技術棧

* 開發語言：Java
* 圖形介面：JavaFX (WebView, WebEngine) + Java Swing (JFrame, JTabbedPane)
* 網路與安全：Java Crypto API (AES/PBKDF2), Sun HttpServer, Java CookieHandler
* 專案維護者：
    * 開發者：yang
    * 測試人員：yang

## 說明

> [!NOTE]
> 本專案為不開源（Closed-Source）專案。

### 附帶檔案
請直接下載 `easyck_1.0.2.exe`。