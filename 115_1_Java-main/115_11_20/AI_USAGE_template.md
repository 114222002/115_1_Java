# 第七週AI使用紀錄

本範本由Codex生成。另存當日日期目錄AI\_USAGE.md，刪除虛構範例後填本人紀錄。沒有使用真實AI也交，來源註明教師模擬，並填本人驗證；未完成就寫待補。

姓名／學號：A114222002/陳俊彰
工具及來源：gemini ai

## 精簡紀錄

|使用目的與Prompt摘要（註明來源:gemini）|採納／拒絕與理由|本人驗證：預期、實際、證據位置|最終修改與commit|
|-|-|-|-|
|【虛構填寫示範，非本人實測】教師模擬HeavyRover，父類別欄位private就再宣告一份|拒絕：getter讀父類別狀態，drill卻改另一份|示範情境：預期鑽探後12/3/1/1，錯誤版卻20/0/0/1；完整紀錄應引用LAB\_REPORT E|示範：刪重複欄位、用protected方法、補停止與計次，再重測；填本人的\[AI]與\[fix]commit|
|目的：實作 Rover 扣能源輔助方法與 HeavyRover 鑽探功能。<br />Prompt 摘要：貼上 Rover 與 HeavyRover 程式碼請求協助完成 TODO，並要求「註解不要刪掉」。|採納：AI 正確透過 protected 的 spendEnergy、addSamples、countAction 更新父類別狀態（未重複宣告欄位），且 drill() 有先用 isStopped() 檢查停止條件，並完整保留原檔註解。|預期：HeavyRoverTry 15 項測試全數「相符」（如鑽探後 12/3/1/1、能源不足維持 7/0/0/0）。<br />實際：編譯執行結果與預期完全一致（15 項皆相符）。<br />證據位置：LAB\_REPORT 執行輸出區。|依 AI 建議完成 Rover.java 與 HeavyRover.java 修改並保留註解；本地測試通過後執行 git commit（請填入你實際的 commit 訊息，例如 \[AI]\[feat] 完成 HeavyRover 鑽探與 Rover 重構）。|

真實AI對話另列一行，寫工具與採納理由，不把模擬回覆當成真實對話。記錄可引用LAB\_REPORT的完整輸出，不重抄十五行。不得上傳個資、帳號密碼或未授權程式。

## 反思

* 哪個案例讓我發現「回成功卻沒更新正確狀態」：在 HeavyRoverTry 的「鑽探（h.drill()）」與「鑽探後（12/3/1/1）」測試案例中可以觀察到此關鍵。如果像示範中的錯誤寫法（子類別重新宣告同名欄位或漏掉呼叫 countAction() / addSamples()），drill() 雖然會回傳「成功」，但後續用父類別的 getEnergy()、getSamples() 或 getActionCount() 查詢時，數值會停留在初始狀態或不同步（例如變成 20/0/0/1 而非 12/3/1/1）。
* 我保留或拒絕AI建議的理由：我保留了 AI 的實作建議，因為它嚴格遵守物件導向封裝原則：沒有在 HeavyRover 中重複宣告 energy、samples、actionCount，而是呼叫父類別提供的 protected 方法（spendEnergy、addSamples、countAction）來修改狀態；同時也先檢查 isStopped() 再執行扣款與計次，確保任務停止或能源不足時不會誤改狀態。此外，在第二次要求後也完整保留了原本的教學註解。
* 我仍無法解釋或尚未完成的部分：目前所有測試案例皆已通過且能理解 protected 繼承與狀態同步的機制，暫無無法解釋的部分（若有自己額外想測的邊界條件，例如：建構子傳入超過 20 的能源或負數樣本時未做防呆檢查，可在此補充說明這是依循類別「不自動修正不合法參數」的約定）。

